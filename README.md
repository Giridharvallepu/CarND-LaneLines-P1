# **Finding Lane Lines on the Road** 
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

<img src="examples/laneLines_thirdPass.jpg" width="480" alt="Combined Image" />

Overview
---

When we drive, we use our eyes to decide where to go.  The lines on the road that show us where the lanes are act as our constant reference for where to steer the vehicle.  Naturally, one of the first things we would like to do in developing a self-driving car is to automatically detect lane lines using an algorithm.

In this project, we detect lane lines in images using Python and OpenCV.  

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


### 1. Project Pipeline.

My pipeline consists of 5 steps. 
1. Convert the images to grayscale and apply the GaussianBlur function to the images in order to depress noise. 
2. Canny Edge Detection algorithm to detect the edges for images. 
3. Apply a region mask defined by the vertices of a quadrilateral to crop the images. 
4. Hough Transform to detect lines for the cropped images, and use the draw_lines() function to draw the left and right straight lane lines. 
5. Using cv2.addWeighted() function to draw the lane lines on the original images.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by seperating line segments by their slope (y2-y1)/(x2-x1) and their center coordinate to decide which line segments are part of the line vs. the right line. Then take average of the position and slope of each of the line segments and extrapolate to the top and bottom of the lane.

By using this pipeline I can successfully detect lane lines in the "solidWhiteRight.mp4" and "solidYellowLeft.mp4" videos.

But the same didn't work for "challenge.mp4" video.So I modified the pipeline to overcome this obstacle.In the optional "challenge.mp4" video, to overcome the different lightness and shadow obstacle, I used the HLS color space instead of RGB color space, Saturation channel data instead of grayscaled image and modified the vertices of region mask because the video resolution is higher than others to successfully detect the lane lines.


### 2. Shortcomings with current pipeline


One potential shortcoming would be the pipeline could draw some strange lane lines when there are some shadows of trees or others in the test images.

Another shortcoming could be the pipeline might sometimes miss the yellow lane lines when the lightness vary. 


### 3. Improvements to pipeline

A possible improvement would be to use advanced OpenCV techniques.

Another potential improvement could be to use convolutional neural networks.

