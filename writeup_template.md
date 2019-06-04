# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
1) identify the lane lines on the road accurately for a variety of lines like solid, curved, dashed etc.

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of the following steps:
1) I performed Gaussian Smoothing with a kernel size of 7 (7 because this to the naked eye this seemed to eliminate noise more effectively)
2) Next I performed Canny Edge detection on the above smoothed image to obtain the edges. A low to high threshold of 0.5 (this falls between the recommended 0.3 to 0.5 range by canny) was chosen
3) I then applied Hough transform to the above Canneyed image, the output of which is an array of lines
4) I selected a quadrilateral region of interest and the coordinates were selected by observing the max y coordinates and the center of the image
5) Since the image in CV falls in the 3rd qudrant, the slope of the left lane will be negative and that of the right lane will be positive. By using the coordinates of the lines obtained from Hough transform i used the slope to distinguish between the left and right lanes.
6) Finally I overlayed the lines above on the original image by using the cv2.AddWeighted function

### 2. Identify potential shortcomings with your current pipeline
Currently the shortcoming in my result are as follow:
1) I need to tune my parameters better to provide a consistent result for all images
2) My current code will not work on a curve with a larger radius of curvature
3) In the presence of shadows, the binary image created will not be accurate

### 3. Suggest possible improvements to your pipeline
My ideas to oimprove my result are as follows:
1) To account for a larger radius of curvature, I think we should the equation of a curve (binomial i.e. to the power of 2)
2) To discard the effect of shadows, I should implement a code to recognize shadows. On researching, I found bradley thresholding to be promising.
