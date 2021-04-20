# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps. 
Since images were of the same shape no cropping or resizing was required.
1. Convert RGB image to grayscale 
2. Do a gaussian blur with a kernel size of 5
3. Do a Canny transofrm
4. Identify and crop the image for region of interest only
5. Run a hough transform for the region of interest
6. Draw lines for continuous line segments identified through hough and overlay it on the orignal image prior to saving the final image

Tuning values for canny, hough and deciding vertices took some work. I did use baseline as what were used in the previous lessoons.
Draw lines function was tricky:
1. I first tried using left side pixels and right side pixels to identify left lane and right lane lines: this did not work well
2. I went through some of the comments in the knowledge section and understood that the line slopes can be used to distinguish between left (slope > 0) and right lane (slope less than 0)
3. I aggregated the x and y values that will qualify for based on positive values > 0.5 and less than 0.5 to limit noise and did a fit to get the coefficients for left lane and right lane.
4. I used the coefficients to get the start and end points with respect to the ends of the cropped iamge to draw lines
5. Tuning the vertices: took some time and setting a noise factor for slope took some iterations as well.
If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when images or videos are not of the same dimension or resolution and are not centered

Another shortcoming could be curved lane lines: current concept only does y= mx+c level of fit and can't really be used for curved lane markers or lines.


### 3. Suggest possible improvements to your pipeline

Using a 2 fit or a higher degree polynomial fit
