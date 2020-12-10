# **Finding Lane Lines on the Road** 

## ChangYuan Liu

### This document is a brief summary and reflection on the project.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:

* Make a pipeline that finds lane lines on the road

* Reflect on the work in a written report


[//]: # (Image References)

[image1]: ./writeup_images/1.png "step 1"
[image2_1]: ./writeup_images/2_1.png "step 2-1"
[image2_2]: ./writeup_images/2_2.png "step 2-2"
[image3]: ./writeup_images/3.png "step 3"
[image4]: ./writeup_images/4.png "step 4"
[image5]: ./writeup_images/5.png "step 5"
---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps: 

(1) Converting color image into grayscale image;
![alt text][image1]

(2) Applying GaussianBlur and Canny to detect edges;
![alt text][image2_1]
![alt text][image2_2]

(3) Specifying the region of interest;
![alt text][image3]

(4) Applying Hough Tranform to find lane lines and draw them in the complete left and right lane lines in the image;
![alt text][image4]

(5) Combining the lane lines with the original image.
![alt text][image5]

In order to draw a single line on the left and right lanes, I tried different approaches in the draw_lines() function:
First, I separate the line segments into left and right based on the slope value and x value. The following approaches have been tried to find a overall slope and one average point (x,y) for left and right, respectively. Here is the different approaches to find them:

(1) Averaging all the slopes in each line segments to get the overall slope, and averaging all the (x,y) to get the average (x,y);

(2) Performing a linear regression on all the (x,y) to get the overall slope, and averaging all the (x,y) to get the average (x,y);

(3) Locating the longest line segment, using its slope as the overall slope, and using its middle point as the average (x,y).

I left the last implementation in the submission as it seemed more reliable.
Then, the last step is to extrapolate the line based on the the overall slop, the average (x,y), and y1 and y2 from vertices.


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be the program wouldn't correctly identify the lane lines when the driving environment changes over time, such as road surface, light conditions, etc. Just like the situation in the challenge video.

Another shortcoming is that the tuning of GuassianBlur, Canny, Hough Transform, and the vertices of the region of interest are all done in trial-and-error. This requires a steep learning curve for someone not familiar with computer vision.


### 3. Possible improvements to my pipeline

A possible improvement would be to fine tuning the paramters for GuassianBlur, Canny, Hough Transform.

Another potential improvement could be to improve the method extrapolating lane lines.
