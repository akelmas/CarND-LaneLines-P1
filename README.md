# **Finding Lane Lines on the Road** 

---


[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I applied **Gaussian Blur** with `kernel_size=5`. That yields a smoother color transitions between image pixels. Then, I went with **Canny Edge Detection** with `low_threshold=50` and `high_threshold=100`. The output of the canny function is an image with lines appearing only, which is then clipped to extract lines located in the meaningful area, by using **Region of Interest** function.  Boundaries are determined based the image size to make the function usable over variable image sizes. Now, it is time to detect lines using **Hough Transform**. Parameters are again variable based on the image size. For example, A video with 720p resolution will processed with different parameters. Finally, outcomes are combined using `cv2.addWeighted` to represent results visually.


In order to draw a single line on the left and right lanes, I modified the draw_lines() function by following a logic like this: 
```
foreach line in detected lines using hough transform:
    - based on the slope, lines are grouped whether it tends to left or right
    - the coordinates are cumulated by their sum, then average coordinates are calculated
    - based on average coordinates, average slope and line equation are defined.
finally:
    to represent full extent of the line, 2 coordinates for each line is calculated
    using line equation, and painted over the image using `cv2.line` function
```

### Potential shortcomings


One potential shortcoming would be what would happen when the horizontal lines appears in region of interest. Also, when the line colors are lost.


### Suggestions

A possible improvement would be to handle the region of interest in a different manner. 
