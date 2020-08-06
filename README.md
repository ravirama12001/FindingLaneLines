1
# **Finding Lane Lines on the Road** 
2
​
3
##Project Report
4
​
5
**Finding Lane Lines on the Road**
6
​
7
The goals / steps of this project are the following:
8
* Make a pipeline that finds lane lines on the road
9
* Reflect on your work in a written report
10
​
11
[image1]: ./examples/grayscale.jpg "Grayscale"
12
​
13
---
14
​
15
### Reflection
16
​
17
###1. Pipeline Description
18
​
19
This is a simple pipeline to find road lanes. 
20
The pipeline has the following steps:
21
​
22
    1. Convert the original image to grayscale
23
    ![Greyscale Image] ./test_images_output/step1.jpg
24
    2. Apply Gaussian blur to the grayscaled image, and get a blurred image
25
    ![blurred] ./test_images_output/step2.jpg
26
    3. Apply Canny edge detector to the blurred image, and  get a black image with white adgesApply
27
    ![Canny edges] ./test_images_output/step3.jpg
28
    4. ROI (region of interest) mask to the edges image to remove all edges outside ROI
29
    ![Region of interest] ./test_images_output/step4.jpg
30
    5. Apply Hough transform to the masked edges image, get a list of line points as output
31
    6. Transform the Hough lines into left and right lane lines:
32
        * Discard lines with slopes close to 0 (slopes in range from -0.3 to 0.3)
33
        * Separate remaining lines in two groups by the sign of the slope
34
        * Average out slopes and intercepts for each group
35
        * Return average slopes and intercepts for the left and right lane lines
36
    7. Draw average lane lines on the original image, such that they are only show inside ROI
37
    ![FinalImage] ./test_images_output/step6-7.jpg
38
    8. Save the image
39
​
40
I have modified the draw_lines() function to get single line on left and right lanes:
41
​
42
    1. Separating Hough lines in two groups by slope (nagative and positive)
43
    2. Removing lines with abnormal slopes (absolute value below 0.5 and above 1.5)
44
    3. Averaging slopes and intercepts for each group
45
    4. For average slope and intercepts, calculating the start and end points, such that lines are only drawn inside ROI
46
    5. Adding lines to the original image
47
​
48
The most challenging parts were:
49
​
50
    * finding accurate parameters for blur-Canny-Hough transformation
51
    * how to draw a single line for the left and the right lane lines
52
    
53
### 2. Potential Shortcomings of Current Pipeline
54
​
55
1. This solution does not work for rain and dust
56
2. This solution will have issues with Region of interest with curved roads
57
3. This solution does not work so well when there are a lot of different color marked lanes
58
4. This solution does not work well at night (it's dark)
59
5. This solution does not work well when light is shining right at the vehicle
60
6. Thos solution does not work well when other vehicles, cars, bikes, people are covering the lanes.
61
​
62
​
63
### 3. Possible Improvements of Pipeline
64
​
65
Need to choose best parameters automatically.
66
​
67
Another improvement would be to dynamically change ROI depends on the lany curve and visibility of the lanes
68
​
