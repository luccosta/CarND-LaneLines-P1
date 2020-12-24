# **Finding Lane Lines on the Road** 


The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[gray]: ./test_images_output/grayscale.png "Grayscale"
[blur]: ./test_images_output/blur_gray.png "Gaussian blur"
[edges]: ./test_images_output/edges.png "Edges"
[masked]: ./test_images_output/masked_edges.png "Region of Interest"
[line]: ./test_images_output/line_image.png "Lines"
[result]: ./test_images_output/lines_edges.png "Result"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps. First, I converted the images to grayscale.

![alt text][gray]

Then I applied Gaussian smoothing to supress noise and spurius gradients by averaging.

![alt text][blur]

 With the smoothed image I applied Canny edge detection.
 
 ![alt text][edges] 
 
 Defined the region of interest in the form of a four sided polygon mask.

 ![alt text][masked]

And applied Hough Line Transform to separete undesired points from the real lines.

![alt text][line]

Then drawned the lines on the image.

![alt text][result]

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by separating what lines are in each lane, taking the horizontal middle of the region of interest as treshold to separate, then I calculate the slope and the y-intercept of each line in a lane and average then to get the slope and the y-intercept of lane.

#### 1.1 Challenge

For the challenge I first modified the four sided polygon mask and other pixel quantitys making the sizes based on the proportions of the image.

Noticing that a lot of detected lines where false positives, the approach to select the lines that were lanes was find a range of slope values that usually fit the real lanes and discard lines with the slope out of this.


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when curved lanes appear, as the adopted line model is linear, the model can not represent that kind of lane and it cause an enourmous confusion on the algorithm.

Another shortcoming could be the possible confusion in what ir a left or right line, since is not that easy as define with a threshold, there are mistakes in this approach. including when dealing with the curved lanes already metioned.

Also, the use of cartesian space to find extrapolated lines may find infinite slope or y-intercept.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to use rough space in draw_lines() to extrapolate the line segments, and exclude problems with vertical lines and their infinite slopes.

Another potential improvement could be to adopt a more complex model of line, also adopting a new approach to separete lines in each side that considers the existance of curved lines.
