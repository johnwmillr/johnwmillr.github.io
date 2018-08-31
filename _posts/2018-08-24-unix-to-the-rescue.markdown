---
title: "Unix to the rescue!"
date: 2018-08-20
layout: post
tag:
- python
- data science
category: blog
author: john
description: Using Unix to process 200k+ files
---

I'm currently working on a data science project involving food recipes scraped from the Internet. One dataset floating around the web contains over 200,000 recipes scraped from [Allrecipes](http://allrecipes.com/). I found two versions of the dataset: one stored in a cleaned, JSON format, the other in raw HTML. In their least-compressed form (containing the raw HTML for each of the 200k+ recipes), the data take up roughly 40 gigabytes.

What's odd about this dataset is that 60% of the 200k+ recipes are all identical. For whatever reason, there are over 120,000 copies of the [*Johnsonville Three Cheese Italian Style Chicken Sausage Skillet Pizza*](https://www.allrecipes.com/recipe/219661/johnsonville-three-cheese-italian-style-chicken-sausage-skillet-pizza/) recipe.

{% include figure.html url="https://images.media-allrecipes.com/userphotos/720x405/995905.jpg" caption="The Chicken Sausage Skillet Pizza, presented without comment." width="80%" %}

Why there are so many copies of this recipe (or, for that matter, why the dish was ever created in the first place) is beyond me. I was more concerned with how all the duplicate recipes would affect my analysis.

## The task at hand
As part of my food recipes project, I'm interested in parsing out the ingredients from many different recipes for the same type of food (e.g. chocolate chip cookies) and comparing how combinations and amounts of ingredients vary between recipes. To properly compare the ingredients between different recipes, I need to know how many servings each recipe is supposed to make. For example, two different cookie recipes may both require a cup of sugar, but you'll end up with completely different cookies if the first recipe is for a batch of ten while the second makes three dozen.

{% include figure.html url="/assets/images/lotsOfFiles.gif" caption="Files for days!" width="100%" %}

Unfortunately, the recipes in the cleaned JSON dataset did not contain serving size information. The raw HTML files did contain serving sizes, but I would have to iterate through each of the 200k+ files to extract the information. I knew my work would be considerably faster if I could throw out the duplicate *Johnsonville* recipes and reduce the size of my dataset by 60%.

## Python approach
My first instinct was to write a simple Python script to iterate through the HTML files and delete any that contained the *Johnsonville* recipe. Well, as I learned, the process gets a bit tricky when you're iterating through hundreds of thousands of files.

The code itself was easy enough to piece together. I quickly had a Jupyter notebook going that looped through the HTML files and deleted any that contained the *Johnsonville* recipe. The code also estimated its remaining time.

```python
# Loop through the HTML recipe files, deleting the Johnsonville duplicates
import os
import time

def calcTimeRemaining(elapsed, n, total):
    return (total-n)/(n/elapsed)

htmlFiles = os.listdir('./Data/Recipes/O2/recipes_html/')
numFiles = len(htmlFiles)
start = time.time()
last = time.time() - start

for n, filename in enumerate(htmlFiles):
    with open(filename, 'r') as infile:
        html = infile.read()

    if 'italian style chicken sausage skillet pizza' in html:
        os.remove(filename)

    if (time.time() - last)/60 > 0.05:  # Print a progress update
        last = time.time()
        elapsed = (time.time() - start)/60
        print("File ({n}/{t}) | Remaining: {r:.2f} min | Files/min: {fpm:.2f}".format(
            n=n+1,
            t=numFiles,
            r=calcTimeRemaining(elapsed, n+1, numFiles),
            fpm=(n+1)/elapsed))
```

After letting the Jupyter notebook run for a few minutes, I was shocked to see an estimated 12 hours remaining. There had to be a better way!

## Unix to the rescue
My moment of clarity came while I was listening to DataCamp's *DataFramed* [Podcast](https://www.datacamp.com/community/podcast/kaggle-future-data-science) in the shower. Hugo Bowne-Anderson, the show's enthusiastic host and interviewer, was doing a *Language Corner* interlude with Spencer Boucher about the often overlooked utility of Unix in data science. Hugo and Spencer stressed a few key advantages command-line tools have over full programming languages for data science:

- Rich APIs, optimized for the "80% use case" (i.e. there's probably already a single Unix command for one-off tasks)
- Available in nearly all scientific computing environments, even when full programming languages aren't
- Unix tools can be easily chained together to create powerful, sophisticated commands
- Unix tools avoid loading entire datasets into memory for processing
- Easily parallelizable

During Spencer's call to action for Unix tools (especially while cleaning data) it hit me -- I could use Unix to delete the *Johnsonville* recipes! After a quick Google search, I ended up on a Stack Overflow [post](https://stackoverflow.com/questions/4529134/delete-files-with-string-found-in-file-linux-cli) that recommended piping the output of `grep` into the `awk` command, creating an executable `.sh` file that would then delete the *Johnsonville* recipes.

Because the directory I was working in contained so many files, I kept running into an "`argument list too long`" error. Unix has a limited buffer for the length of any given command, and so it was unable to string together the roughly 120,000 names of files containing the *Johnsonville* recipe.

## The solution
After playing with the commands in a test directory with fewer files and visiting a few more Stack Overflow forums, I ended up with a chain of commands that did the trick:
```shell
$grep -rl . -e 'Italian Style Chicken Sausage Skillet Pizza' | awk '{print "rm -v "$1}' > deleteRecipes.sh
$source deleteRecipes.sh
```

The Unix code I ended up using makes use of a couple of really helpful command-line tools:

[`grep`](https://www.computerhope.com/unix/ugrep.htm)

 The `grep` tool uses [regular expressions](https://en.wikipedia.org/wiki/Regular_expression) to parse and print text within the command line. In the command above, I'm telling `grep` to search the current directory for any files containing the "Skillet Pizza" text and print the names of any files containing the specified text.

 The `-rl` option tells `grep` to search recursively and print the matched file names, rather than the actual matched text. The `e` option is used to specify the regular expression to search for. The `.` tells `grep` to search within the current directory.

[`|`](http://www.linfo.org/pipes.html) and [`>`](http://www.westwind.com/reference/os-x/commandline/pipes.html#redir-output)

The `|` character in-between the `grep` and `awk` commands is a *pipe* and is used to send the output from one command into another. The `>` character redirects the output of a command to be stored as text in a file (and vice versa). In my example above, the output from `grep` (a list of filenames) is piped into the `awk` command whose output (a list of `rm` commands) is then redirected into the `deleteRecipes.sh` file. Be careful with `>` as it will overwrite any existing files with the same name. The `>>` operator is a safer alternative that appends to rather than overwrites existing files.

[`awk`](http://linuxcommand.org/lc3_adv_awk.php)

The `awk` command is actually calling an entire programming language (named AWK) that is helpful for filtering text, especially data stored in a columnar format (e.g. `CSV`). Serendipitously, my friend [Micah](http://micahjon.com/) sent me a [helpful article](https://gregable.com/2010/09/why-you-should-know-just-little-awk.html) while I was working on this post that makes a case for learning AWK and provides a few useful examples.

In my command above, I am using `awk` to generate a line of text, `rm -v FILENAME.html`, for each *Johnsonville* recipe identified by `grep`. The `$1` is a variable in `awk` that will take on the file names piped in from `grep`. The `rm` statement deletes the specified file, and `-v` makes the command verbose.

Outputting the `rm` commands to a file to be executed later (rather than maintaining a list of all the `rm` within the command line buffer) is what allowed me to get around the "`argument list too long`" error I was seeing before.

Finally, I call use the [`source`](https://bash.cyberciti.biz/guide/Source_command) command to run the `rm` commands and delete the offending *Johnsonville* recipes.

## Summary
The whole process of identifying and deleting the culprit recipes took about 1.5 hours with the Unix code above, nearly 90% faster than the estimated time for my Python code! There are bound to be better solutions to this problem than the ones I've described here. I'm sure there's a proper way to solve this sort of problem in Python, and I'd love to hear in the comments below what approach that may be.

But for me, this was a great opportunity to try out a new technique and expand my set of data science skills ever so slightly. The next time I'm tackling a 40 GB list of unruly HTML files, I'll be less likely to chuck my keyboard across the room in frustration and more quick to pull this powerful `grep` `awk` combo from my data science tool belt.

A big thanks to Hugo and Spencer from the [*DataFramed*](https://www.datacamp.com/community/podcast) Podcast. If you aren't already listening to *DataFramed*, I strongly recommend checking it out. Each episode covers a different area of data science, and Hugo is an engaging, articulate interviewer.
