---
title: "Creating average faces in Python 🙂"
date: 2019-09-11
layout: post
tag:
 - python
 - data science
 - image processing
 - tutorial
category: blog
author: john
name: john
image: assets/images/FaceAverages/Walmart-1.jpg
description: "Simple tutorial for creating face averages in Python"
---

This post explains how to make [face averages](/faces-of-fortune/) in Python using my [Facer](https://github.com/johnwmillr/Facer) package. Facer draws extensively on [this tutorial](https://www.learnopencv.com/average-face-opencv-c-python-tutorial/) from [Satya Mallick](https://github.com/spmallick). I had to update the code pretty heavily to get the package to work, so I thought I'd share my modifications.

# Installation
You have my 100% money-back guarantee that the most difficult part of using this package is installing the requirements. Once you've got OpenCV installed, the rest will be smooth sailing.

## 1. Install OpenCV
On Mac, use [`homebrew`](https://brew.sh) to install OpenCV.

```shell
brew install opencv
```

Installing OpenCV with `brew` did work for me, but it also broke my previous Python installation and all my virtual environments. So uhh, good luck with that. I don't have experience installing OpenCV on Windows, but you can try this [tutorial](https://opencv-python-tutroals.readthedocs.io/en/latest/py_tutorials/py_setup/py_setup_in_windows/py_setup_in_windows.html).

## 2. Clone the project repository
After installing OpenCV, we can clone the project repository from GitHub:

```shell
git clone https://github.com/johnwmillr/facer.git Facer
```

The `git clone` command will create a new folder, `./Facer`, and populate it with files from the GitHub repository. After cloning the repo, `cd` into the new directory.

## 3. Install the Python libraries
After installing OpenCV and cloning the project repository, we just need to add a few more helper libraries: `numpy`, `matplotlib`, and `dlib`.

```
pip install -r requirements.txt
```

## 4. Download the pre-trained detection model
The face landmark detection relies on a pre-trained model that must be downloaded separately from the `dlib` package itself.

```shell
wget http://dlib.net/files/shape_predictor_68_face_landmarks.dat.bz2
```

Unzip the compressed file after it finishes downloading and move it into the `./Facer/dlib` directory.

Congrats, you've installed everything you need to run Facer!

# Creating average faces

Having installed Facer (and completed the hardest parts of this tutorial!), we can begin creating average faces.

The process is actually quite straightforward. Here's how to load images from a directory and create an average face:


```python
from facer import facer

# Load face images
path_to_images = "./face_images"
images = facer.load_images(path_to_images)

# Detect landmarks for each face
landmarks, faces = facer.detect_face_landmarks(images)

# Use  the detected landmarks to create an average face
average_face = facer.create_average_face(faces, landmarks, save_image=True)

# View the composite image
plt.imshow(average_face)
plt.show()
```

That's it! The `facer.create_average_face` function will have saved a JPG image containing the average face output.

The Facer package also supports creating animated GIFs that display each face used to create an average:

```python
from facer import facer

# Load face images
path_to_images = "./face_images"
images = facer.load_images(path_to_images)

# Create the animated GIF
gif, average_face = facer.create_animated_gif(images)
```

{% include figure_link.html url="/assets/images/FaceAverages/AverageFace_Apple.gif" href="/assets/images/FaceAverages/AverageFace_Apple.gif" caption="Combining faces of Apple's executive leadership." width="90%" %}

Let me know if you have any questions! I'll be most responsive to new issues or pull requests on the [GitHub repository](https://github.com/johnwmillr/Facer).
