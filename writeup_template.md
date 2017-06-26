# **Finding Lane Lines on the Road**


---

The goals / steps of this project are the following:
  
* Make a pipeline that finds lane lines on the road  
* Reflect on your work in a written report


[//]: # (Image References)
[image1]: ./writeup-images/1_grayscale_whiteCarLaneSwitch.jpg "Grayscale"
[image2]: ./writeup-images/2_blur_whiteCarLaneSwitch.jpg "Blur"
[image3]: ./writeup-images/3_canny_whiteCarLaneSwitch.jpg "Canny"
[image4]: ./writeup-images/4_region_whiteCarLaneSwitch.jpg "Region of Interest"
[image5]: ./writeup-images/5_hough_whiteCarLaneSwitch.jpg "Hough Space"
[image6]: ./test_images/processed_whiteCarLaneSwitch.jpg "Final"

---

## Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

**My pipeline consisted of a number of steps:**  
Convert the image to grayscale
![alt text][image1]
Apply some Gaussian Blur to smooth out any outliers in the image
![alt text][image2]
Use Canny edge detection to build an array of edges in the image
![alt text][image3]
Subset the detected edges to just the trapezoidal region of interest making further operations more computationally efficient
![alt text][image4]
Convert the detected edges into Hough space where line segments can be detected and drawn onto a layer
![alt text][image5]
Overlay the identified lines onto the original image
![alt text][image6]  

**In order to draw a single line on the left and right lanes, I modified the draw_lines() function by**:  

- The overall premise was to divide the lines in the image into left lane lines and right lane lines then process them as necessary  
- This splitting of left and right lane lines was performed by looking at the gradient. Lines with a positive gradient are Right lane lines and those with a negative gradient are Left  
- The start and end points of each of the lines were collected in arrays r_line and l_line and then averaged over the number of left and right lane lines that were identified  
- Following this coordinate geometry was used to find the overall lane line, specifically the Equation of a Line Using One Point and the Gradient  
- These lines were then drawn in blue and green on the image and video feed  





## 2. Identify potential shortcomings with your current pipeline
- The algorithm does not work well when the image becomes noisy with lots of "edges" distributed throughout the region of interest
- Nor does it work well when presented with corners as the line matching program is linear
- Also, for some reason the right lane line always seems to be longer than the left and I am not sure why?


## 3. Suggest possible improvements to your pipeline

- The algorithm's performance could be improved on corners by using a spline instead of a linear equation to join the line segments
