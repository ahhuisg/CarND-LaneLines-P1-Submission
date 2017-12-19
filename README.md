# **Finding Lane Lines on the Road** 

## Overview

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image_step1]: ./test_images_output/step1.png "Step1"
[image_step2]: ./test_images_output/step2.png "Step2"
[image_step3]: ./test_images_output/step3.png "Step3"
[image_step4]: ./test_images_output/step4.png "Step4"
[image_step5]: ./test_images_output/step5.png "Step5"


### Reflection

### 1. The Pipeline

My pipeline consisted of 5 steps:

* Convert the images to grayscale and apply Gaussian smoothing / blurring on it

![alt text][image_step1]

* Find the canny edges based on lower and upper threshold

![alt text][image_step2]

* Extract edges from the image based on region of interest

![alt text][image_step3]

* Extract Hough lines and draw on the image with a single thicken red line on both left and right lanes

![alt text][image_step4]

	In order to draw a single line on the left and right lanes, I modified the draw_lines() function by finding the start and end points of both left and right lanes:

	a. Exclude those lines whose absolute value of the slope is less than 0.5

	b. Group x values and y values of the  into 2 corresponding list

	c. Use numpy.polyfit with 1 degree for x and y values to find the coefficent of the straight lines

	d. Calculate the crossing points of the lines with our region of interest, which are the starting and end points of the straight line respectively

	e. Draw a single thicken red line based on the starting and end points derived from the above


* Combine the images by overlaying the thicken and colored line on the original image

![alt text][image_step5]

### 2. Potential Shortcomings with the current pipeline

* The first potential shortcoming would be when the Lane Lines are not straight enough. For example, if there are very curly lanes or there are sharp or U turns on road

* The second shortcoming could be the quality of the frames of the video are not consistent and it is impossile to have one pair of constant Canny threshold values to extract the edges. For example, there are many trees on the roadside and the shadows of the trees blurs the lane lines for some frames

* The third shortcoming could be that the region of interest for the frames of the video changes from frame to frame due to traffic condition


### 3. Possible improvements to the current pipeline

* A possible improvement would be to change the construction of the drawing line to cater for both straight and curly lane lines. For example, make use of numpy.polyfit with 2 degrees 

* The second potential improvement could be to dynamically calculate the region of interest for each frame

* The third otential improvement could be find some way to dynamicaly set the value of Canny lower and upper values so that we are able to extract the edges clearly
