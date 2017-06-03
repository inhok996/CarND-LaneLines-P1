#**Finding Lane Lines on the Road** 

##Writeup Template

###You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

For all images, my pipeline has five steps as described below. 
1. images are converted to grayscale images by grayscale function.
2. grayscale images are converted to blurred iamges by gausian_blur function.
3. canny images are made with 50 of low threshold and 80 of high threshold.
4. After make appropriate square information, region of interest is applied to the canny images.
5. lines are found through hough transformation in the function 'hough_lines'.

Actually, I didn't changed draw_lines function, but I added one function called vote_lines.
'vote_lines' function is called by hough_lines before it calls draw_lines function.

"""
def vote_lines(lines,flag,img_height,img_width):
"""

precondition:
parameter 'lines' should be the list of specific points(returned from HoughLinesP function)
parameter img_height, img_width should be the height and width of the image for drawing lines.

postcondition:
new_lines is filled with appropriate value.(type: np.array())

return:
This function returns newly made list of points when flag is 2(integer), lines(not pharsed) when flag is 1.

formula : y = mx + c
To determine a line, this function gets appropriate m(gradient) and c(coefficient).
This function first devide points in the 'lines' parameter into left side and right side.
Then it calculate the gradient of each line and add the line when it's gradient meets certain value.
I hard coded it ranging from 0.55,0.85 for the right side, and -0.85,-0.5 for the left side.
Since not all gradient value are the same, this function calculate the average of the gradients.
To determine the c, I use the lines selected above,choosing only x value and calculate average x.
After determine the line, the function select four points in the line with the same height.
Finally,they are loaded into the np.array container and returned. 


![alt text][image1]


###2. Identify potential shortcomings with your current pipeline

One potential shortcoming would be what would happen when the challenge-like situation.

The lines are really shaking when shadow appears.

Second potential shortcoming is that my pipeline doesn't determine curvature since I didn't change draw line function.

###3. Suggest possible improvements to your pipeline

A possible improvement would be to erase more unrelated lines in HoughTransform function.

I think It has to have different parameter values when it meets shadow.

