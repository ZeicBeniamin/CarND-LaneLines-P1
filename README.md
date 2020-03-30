
# **Finding Lane Lines on the Road** 

[//]: # (Image References)

[image1]: ./examples/gui_tool.png "gui_tool"


### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consists of roughly 5 steps, that are: grayscale, blur, canny edge detection, mask, hough line finding. In order to find the optimal parameters for each of those steps, I built a mini graphical tool that allowed tweaking parameters while updating the image. 
After setting the initial values for the parameters, and noticing problems in the videos, I built another mini tool (not included in this repo), that allowed me to iterate throuhg every frame of the video and save the problematic ones to disk for futher investigation.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by averaging the slopes of the detected lines. Unfortunately, this method didn't work, so I used np.polyfit to fit a line over each of the lanes. This worked a lot more better, but still had some problems, so I wrote another function, for averaging the coordinates of the lane line over a few frames.

The gui tool for adjusting parameters
![][image1]


### 2. Identify potential shortcomings with your current pipeline


This pipeline is clearly suited only for straight lane lines. As I could see from the challenge video, no version of my code could cope with the curved lane. Moreover, the contrast is very weak on some segments of the lane, such that even canny edge detection and hough transform could not be applied with success. Maybe a colour filter would work better in this situations.


### 3. Suggest possible improvements to your pipeline

The pipeline could be improved by making it ready for managing right or left turns. In order to accomplish this, identification of the lanes should be performed using other methods than canny and hough transform (maybe a color filter or, much better, an adaptive color filter). The function that draws the lanes must be modified too, in order to handle curved lines and model them as polynomial curves.
