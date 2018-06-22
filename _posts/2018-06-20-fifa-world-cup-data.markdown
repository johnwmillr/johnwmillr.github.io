---
title: "2018 FIFA World Cup :soccer:"
date: 2018-06-20
layout: post
tag:
- python
- data science
- API
category: blog
author: john
image: assets/images/step_counts_monthly.png
description: Visualizations of player data from the 2018 FIFA World Cup
---

We're in the midst of the 2018 FIFA World Cup. I've wanted to play with some sort of sports-related data for a while, so I figured now is as good as a time as any to start.

# Collecting the data
I've been trying to get more practice interfacing with APIs, so I was hoping to find a soccer API rather than simply a precompiled dataset. After doing some Googling for World Cup APIs, I came across the [Sportradar API](https://developer.sportradar.com/io-docs). Sportradar provides 15 APIs for soccer data alone. Luckily, they [provide a free tier](https://developer.sportradar.com/member/register) for the APIs that allows for 1,000 queries each month.

The code below provides a simple interface with the Sportradar Soccer INTL Trial v3 API using the Python `requests` library. I have started writing a Python package for the Sportradar API which is [available here](https://github.com/johnwmillr/SportradarAPIs).

```python
import requests
import json

class SportRadarAPI(object):
    """Interface with the Sportradar Soccer INTL API"""
    # Really this should be a super class from which the specific INTL API would inherit
    
    _BASE_URL = "https://api.sportradar.us/soccer-t3/intl/en"
    
    def __init__(self, api_key, format='json'):
        self._FORMAT = "." + format.strip(".")
        self._KEY = api_key
        
    def _make_get_request(self, partial_uri):
        """Make a GET request to the SportRadar API"""
        URI = self._BASE_URL + "/" + partial_uri + self._FORMAT
        response = requests.get(URI, params={'api_key': self._KEY})
        assert response.status_code == 200, "Error in API request. Status: {}".format(response.status_code)       
        return response
    
    def get_tournaments(self):
        """Provides the list of International Soccer tournaments"""
        URI = "tournaments"
        return self._make_get_request(URI)
    
    def get_tournament_info(self, tournament_id):
        """Provides information for International Soccer tournaments"""
        URI = "tournaments/{_id}/info".format(_id=tournament_id)
        return self._make_get_request(URI)
    
    def get_team_profile(self, team_id):
        """Team information, including player roster information"""
        URI = "teams/{_id}/profile".format(_id=team_id)
        return self._make_get_request(URI)
        
    def get_player_profile(self, player_id):
        """"""
        URI = "players/{_id}/profile.{_format}".format(_id=player_id)
        return self._make_get_request(URI)
```

The code below demonstrates how to create an instance of the class and start downloading data from the API.

```python
# Create an instance of the SportRadar API class
sportsradar = SportRadarAPI("paste your api key here")

# Get a list of all tournaments
tournaments = sportsradar.get_tournaments().json()

# Get info on the 2018 World Cup (Teams, Rounds, etc.)
worldcup = sportsradar.get_tournament_info(tournaments['tournaments'][4]['id']).json()

# Get more information on each team in the World Cup
teams = []
team_counter = 0
for group in worldcup['groups']:
    for team in group['teams']:
        team_counter += 1
        team_id = team['id']
        team_name = team['name']
        print("({}): {}, {}".format(team_counter, team_name, team_id))
        try:
            teams.append(sportsradar.get_team_profile(team_id).json())
        except Exception as e:
            print("Error: {}".format(e))
        time.sleep(5) # wait 5 seconds before next API call
        
# Save the team data to a .json file
print("Saving the data...", end="", flush=True)
with open("world_cup_team_data.json", "w") as outfile:
    json.dump(teams, outfile)
print(" Done.")
```

And now we have the data we need!

---
# Visualizations
Below are some of the plots I've made using the World Cup data. My post demonstrating the height distributions for each position received over 10,000 upvotes on [/r/dataisbeautiful](https://www.reddit.com/r/dataisbeautiful/comments/8sg3ok/distributions_of_height_for_the_different/)! For all of the box-whisker plots, the middle line indicates the median of the team's height distribution. The edges of the boxes extend to the first and third quartiles of the data. The whiskers extend to show the range of the data, excluding any extreme outliers.

### Distributions of player height sorted by country
{% include figure_link.html url="/assets/images/nations_by_height.png" href="https://www.reddit.com/r/dataisbeautiful/comments/8s7cso/distributions_of_height_for_each_team_in_the_2018/" caption="Box-whisker plots of player height for each team in the 2018 FIFA World Cup. Box colors correspond to the base color of the team's home jersey." width="100%" %}

### Distributions of player height sorted by position
This is an interactive plot. Move your mouse over the scatter plot points to see details on each player.
{% include mpld3_height_by_position.html %}

### Height vs. weight by player position
{% include figure_link.html url="/assets/images/height_vs_weight_by_position.png" href="/assets/images/height_vs_weight_by_position.png" caption="Height and weight values for each player in the 2018 FIFA World Cup (n=735)." width="100%" %}