# **Finding Lane Lines on the Road** 


---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./pipeline_output/solidWhiteCurve_1_gray.png "Grayscale"
[image2]: ./pipeline_output/solidWhiteCurve_2_blur.png "Blur"
[image3]: ./pipeline_output/solidWhiteCurve_3_edges.png "Edges"
[image4]: ./pipeline_output/solidWhiteCurve_4_mask.png "Mask"
[image5]: ./pipeline_output/solidWhiteCurve_5_line.png "Lines"
[image6]: ./pipeline_output/solidWhiteCurve_6_final.png "Final"

---

### Reflection

### 1. Description of pipeline. As part of the description, explain how you modified the draw_lines() function.

According to the pipeline() function, it takes three input params and return the final image:
* image: numpy array image.
* is_save: if true, function will save the temp jpg file of the pipline to local disk. if false, function will not save
* title: file name of the temp jpg to save

My pipeline consisted of 6 steps:
* Grayscale the image
* Gaussian smoothing the image
* Use Canny edges
* Create an interest region mask on the image
* Use Hough Transform to detect lines
* Draw lane lines on the image

In order to draw a single line on the left and right lanes, I modified the draw_lines() function:
* calculate the slope of each line in an image: slope = (y2 - y1) / (x2 - x1)
* calculate the average point of each line in an image: x_average = (x1 + x2) / 2, y_average = (y1 + y2) / 2
* find a good range of slope for left lane line [-0.9, -0.4], and right line [0.4, 0.9]
* calculate average slope and average point of left line in an image
* calculate left top point and left bottom point with left average slope and left average point
* draw left single line with left average slope, left top point and left bottom in an image
* calculate average slope and average point of right line in an image
* calculate right top point and right bottom point with right average slope and right average point
* draw right single line with right average slope, right top point and right bottom in an image

Here is how the pipeline works: 

![alt text][image1]
![alt text][image2]
![alt text][image3]
![alt text][image4]
![alt text][image5]
![alt text][image6]


### 2. Potential shortcomings with the current pipeline

* sometimes no left or right lane line detected in some frame when the mask region is not good enough to cover both lane lines
* sometimes single left or right lane line doesn't match perfect when the mask region is not good enough that with some noises lines


### 3. Suggest possible improvements to my pipeline

* A possible improvement would be to detect the noises lines and remove them from mask region
* Another potential improvement could be to create a reference quadrilateral to match the region a car can drive
