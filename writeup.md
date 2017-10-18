# **Finding Lane Lines on the Road** 



---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report




---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I apply the guassian blur with kernel size of 5.
I then used canny edge detection with low threshold as 50 and high threshold as 150 to detect large change in gradients.

The fourth step is to select a area of interest with value of y axis as 320.
The fifth step is to use the ouput from canny edge detect lines on the image. The value of the parameter are:
hough_rho = 2
hough_theta=1
hough_threshold=15
hough_min_line_len=25
hough_max_line_gap= 45

This gives us all the line on the left and right lane markings. But the number of line vary with image and lanes.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function to extract all the point of the left lane and all the points on the right lane and fit a linear regression model on both the lanes.

we then use thos model to make prediction on all the x axis points on left lane varing from 0 to 475 and from right lanes from 500 to 960.
We then filter the points pair with only those points that has y values between  320 and 540.

This draws a single line on left and right lane..

 

### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when there are other car closer to us. The hough tranform might detect boundaries of the car.

Another shortcoming could be when we are in the curves. as we have only detected straight lines right now


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to choose better parameters for hough transform

Another potential improvement could be to fitting a polynomial degree curve instead of a straigh line
