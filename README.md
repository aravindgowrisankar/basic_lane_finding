#**Finding Lane Lines on the Road** 
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

<img src="laneLines_thirdPass.jpg" width="480" alt="Combined Image" />

Setup instructions can be found [here](INSTALL.md)

## Reflections

I found it to be a challenging first assignment. 

I had fun learning about Hough Transform and Canny Edge Detection. I think I had some success with identifying lane segments but didn't get a chance to complete the extrapolation of the lines.

My approach was as follows:
1. Gray scale
2. Canny Edge Detection
3. Identify region of interest - Polygon determined proportional to size(room for improvement)
4. Hough Transform
5. Identifying Two Lanes using slope
I use slope to identify lines that are vertical in nature. I eliminate horizontal lines and threshold based on slope to identify lines.

I made some assumptions to simplify the problem which may not hold in the real world. I think my approach will have to be refined quite a bit to handle real world complexities. The first assumption I made is around the region of interest. After playing aroung with a triangular mask, I fixed the region of interest to be a polygon that is proportional to the image size. While this works okay for the problem in question, it may not work for different camera setups(e.g. mounted at a different height)

Another assumption here is that there will be some some markings on the image. 
For highways, this is okay but this approach may fail in neighborhoods or if the stretch of the road immediately in front of the camera doesn't have lane markings. In those cases, we may have to either extrapolate from the previous image(s) seen by the camera. Smoothing may make sense.

Overall, I enjoyed the assignment and wish I had spent more time on it! Thank you for the interesting material and the  project. I look forward to learning more.


