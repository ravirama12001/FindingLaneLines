# **Finding Lane Lines on the Road** 

##Project Report

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:

* Make a pipeline that finds lane lines on the road

* Reflect on your work in a written report

[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

![image] (/examples/grayscale.jpg)

### Reflection

### Pipeline Description

This is a simple pipeline to find road lanes. 

The pipeline has the following steps:

    1. Convert the original image to grayscale
    .[//]: # (Image References)
    .[step0]: ./test_images_output/step0.jpg "Original Image"

    2. Apply Gaussian blur to the grayscaled image, and get a blurred image

    ![blurred] ./test_images_output/step2.jpg

    3. Apply Canny edge detector to the blurred image, and  get a black image with white adgesApply

    ![Canny edges] ./test_images_output/step3.jpg

    4. ROI (region of interest) mask to the edges image to remove all edges outside ROI

    ![Region of interest] ./test_images_output/step4.jpg

    5. Apply Hough transform to the masked edges image, get a list of line points as output

    6. Transform the Hough lines into left and right lane lines:

        * Discard lines with slopes close to 0 (slopes in range from -0.3 to 0.3)

        * Separate remaining lines in two groups by the sign of the slope

        * Average out slopes and intercepts for each group

        * Return average slopes and intercepts for the left and right lane lines

    7. Draw average lane lines on the original image, such that they are only show inside ROI

    ![FinalImage] ./test_images_output/step6-7.jpg

    8. Save the image


I have modified the draw_lines() function to get single line on left and right lanes:

    1. Separating Hough lines in two groups by slope (nagative and positive)

    2. Removing lines with abnormal slopes (absolute value below 0.5 and above 1.5)

    3. Averaging slopes and intercepts for each group

    4. For average slope and intercepts, calculating the start and end points, such that lines are only drawn inside ROI

    5. Adding lines to the original image

The most challenging parts were:

    * finding accurate parameters for blur-Canny-Hough transformation

    * how to draw a single line for the left and the right lane lines

### Potential Shortcomings of Current Pipeline

1. This solution does not work for rain and dust

2. This solution will have issues with Region of interest with curved roads

3. This solution does not work so well when there are a lot of different color marked lanes

4. This solution does not work well at night (it's dark)

5. This solution does not work well when light is shining right at the vehicle

6. Thos solution does not work well when other vehicles, cars, bikes, people are covering the lanes.

### Possible Improvements of Pipeline

Need to choose best parameters automatically.

Another improvement would be to dynamically change ROI depends on the lany curve and visibility of the lanes
