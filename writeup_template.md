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

[//]: # (two_masks)

[image2]: ./test_images_output/output_two_mask_challenge2.jpg 

[//]: # (v_transform)

[image3]: ./test_images_output/output_color_trans_challenge2.jpg 

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I apply Canny Edges detection to the grayscale image. After that I apply gaussian blur to the cann image. Then I mask the image with vertices selected by relative coordinates not the absolute coordinates. After that I use hough transform to detect lines and then draw the lines back to the original image.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function to use linear regression based on the line vertices produced in hough transform. It will predict slope and intersact based on the line points from hough transform

In the challenge question, the issue is the gray road becomes a huge noise to the yellow and white lines. So I though about two procedure:

First is to use specific mask to keep out as much background as possible. But this procedure is not general. So I did not go further. But I do generate really good result, which can be found under ./test_images_output:

![alt text][image2]

Then I though about ways to filter out unwanted color. Then I looked up cv2.cvtColor. And I found there are many other color transforms besides RGB2GRAY. And I found RGB2HSV and RGB2HLS works equally fine in this case.

Here is a result I got:

![alt text][image3]

### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when there are too much gap between lane sections. In worst case, my draw_line function will not be able to extrapolate any line. 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to use higher order extrapolation method. Instead of typical linear regression, I can try to use higher-order curve fitting suchas numpy.polyfit with degree of 2 or 3 or even higher.

Another potential improvement could be to use matrix multiplcation instead of using for loops
