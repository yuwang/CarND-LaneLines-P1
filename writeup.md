# **Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

[//]: # (Image References)

[image_solidWhiteCurve]: ./test_images/solidWhiteCurve.jpg "solidWhiteCurve"
[image_solidWhiteRight]: ./test_images/solidWhiteRight.jpg "solidWhiteRight"
[image_solidYellowCurve]: ./test_images/solidYellowCurve.jpg "solidYellowCurve"
[image_solidYellowCurve2]: ./test_images/solidYellowCurve2.jpg "solidYellowCurve2"
[image_solidYellowLeft]: ./test_images/solidYellowLeft.jpg "solidYellowLeft"
[image_whiteCarLaneSwitch]: ./test_images/whiteCarLaneSwitch.jpg "whiteCarLaneSwitch"
[image_solidWhiteCurve_output]: ./test_images_output/solidWhiteCurve.jpg "solidWhiteCurveOutput"
[image_solidWhiteRight_output]: ./test_images_output/solidWhiteRight.jpg "solidWhiteRightOutput"
[image_solidYellowCurve_output]: ./test_images_output/solidYellowCurve.jpg "solidYellowCurveOutput"
[image_solidYellowCurve2_output]: ./test_images_output/solidYellowCurve2.jpg "solidYellowCurve2Output"
[image_solidYellowLeft_output]: ./test_images_output/solidYellowLeft.jpg "solidYellowLeftOutput"
[image_whiteCarLaneSwitch_output]: ./test_images_output/whiteCarLaneSwitch.jpg "whiteCarLaneSwitchOutput"

---

## Reflection

## 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps.  I will show you how each of these steps works using the provided **solidWhiteCurve.jpg** image.

1. Convert the images to grayscale.
2. Apply Gaussian blur on the gray image.
3. Get canny lines from the blurred image. In this step I have to tune the low and high threshold.
4. Get the masked image. In this step, I have to define the region of the point of interests, create a blank mark, filling the POI region with color and then apply bit wise to the canny lines.
5. Get the averaged left line and aver] right line. In this step, I first have to define the hough lines parameter then apply them to the hough line method to get all the lines detected. Then I sorted all the left lines and right lines into two category, and found the poly fit line that is close to all of them on each side. Also I have to define the vision horizon region for the end positions for both lines.
6. Finally draw the left and right line on the initial image. I have to modify the original draw_lines() function to use addWeight() so that the lines looks semi-transparent. Also I have to fill out the invalid lines.

Below are the test images and what they looks like after the processing.
| Original | Processed |
| -------------------------------------- | -------------------------------------- |
|![solidWhiteCurve][image_solidWhiteCurve]|![solidWhiteCurveOutput][image_solidWhiteCurve_output]|
|![solidWhiteRight][image_solidWhiteRight]|![solidWhiteRightOutput][image_solidWhiteRight_output]|
|![solidYellowCurve][image_solidYellowCurve]|![solidYellowCurveOutput][image_solidYellowCurve_output]|
|![solidYellowCurve2][image_solidYellowCurve2]|![solidYellowCurveOutput2][image_solidYellowCurve2_output]|
|![solidYellowLeft][image_solidYellowLeft]|![solidYellowLeftOutput][image_solidYellowLeft_output]|
|![whiteCarLaneSwitch][image_whiteCarLaneSwitch]|![whiteCarLaneSwitchOutput][image_whiteCarLaneSwitch_output]|

## 2. Identify potential shortcomings with your current pipeline

One potential shortcoming would be when the lane is worn off too much and the white/yellow color becomes barely visible,
my pipeline won't be able to recognize the lane.

Another shortcoming could be if the lane suddenly changed direction too abruptly (with absolute slope of less than 0.5), it won't handle that.

## 3. Suggest possible improvements to your pipeline

A possible improvement would be to first get the POI region from the gray blurred image, then apply canny to get the lines,
this will theoretically reduce the calculation canny has to do.

Another potential improvement could be to turning the canny low and high threshold so that we can handle the first shortcomings mentioned in #2 better.
