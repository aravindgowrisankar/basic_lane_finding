#**Finding Lane Lines on the Road** 
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

<img src="./test_images/laneLines_thirdPass.jpg" width="480" alt="Combined Image" />

Setup instructions can be found [here](INSTALL.md)

## Files

Writeup of Report

[This file](README.md)

Source Code

[P1.ipynb](P1.ipynb)

Video Output

1. [White Lane Video](white.mp4)
2. [Yellow Lane Video](yellow.mp4)
3. [Challenge Video](extra.mp4)


## Reflections

I found it to be a challenging first assignment. 

I had fun learning about Hough Transform and Canny Edge Detection. I think I had some success with identifying lane segments.

My approach was as follows:
1. Gray scale
2. Canny Edge Detection
3. Identify region of interest - Polygon determined proportional to size(room for improvement)
4. Hough Transform
5. Identifying Two Lanes using slope and extrapolating them
6. Smoothing

### Hough Transform Parameters
   rho = 2
   theta = np.pi/180
   threshold = 50
   min_line_length  = 100
   max_line_gap = 160
 
### Canny Parameters
    low_threshold = 50
    high_threshold = 150

### Lane Extrapolation
1. Filter out non vertical lines. I apply a threshold slope of 0.25(+ve or -ve depending on the lane line)
2. Group remaining lines into positive and negative slope.
3. Extrapolate each line segment.
4. Average line segments for the positive slope and negative slope.

### Smoothing
There were some frames in the yellow lane video where my pipeline would not detect one of the lane lines. To address this I used smoothing of the lane lines from the past  three time frames(including current one).


### Assumptions Made and Real world challenges

I made some assumptions to simplify the problem which may not hold in the real world. I think my approach will have to be refined quite a bit to handle real world complexities. 

The first assumption I made is around the region of interest. After playing aroung with a triangular mask, I fixed the region of interest to be a polygon that is proportional to the image size. While this works okay for the problem in question, it may not work for different camera setups(e.g. mounted at a different height)

Another assumption here is that there will be some some markings on the image. 
For highways, this is okay but this approach may fail in neighborhoods or if the stretch of the road immediately in front of the camera doesn't have lane markings. In those cases, we may have to either extrapolate from the previous image(s) seen by the camera. Smoothing using the data from the past few images may help solve this problem.

A third assumption is about the slope of the two lanes. I use a fixed threshold which will break when the lines are different or when they curve!.

Overall, I enjoyed the assignment and wish I had spent more time on it! Thank you for the interesting material and the  project. I look forward to learning more.


Other comments:
I briefly tried hsv colorspace(Saturation values) instead of grayscale. I was hoping it would offset the lighting issues. But I noticed that the thresholds that worked for grayscale(Canny and Hough) no longer worked for HSV.
