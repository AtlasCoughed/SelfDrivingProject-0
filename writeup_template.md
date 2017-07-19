Finding Lane Lines on the Road

The goals / steps of this project are the following:

Make a pipeline that finds lane lines on the road
Reflect on your work in a written report
Reflection

#Description of Pipeline

The first portion of my pipeline is the analysis and setup parameters. We have to first read the images size and determine the size of the image. We tried to create my pipeline so that it was somewhat dynamic, allowing a wider range of image size. This certainly could be improved upon. This is what would become our field of concentration.

The first step to our image processing begins with grayscaling our image. This is it reduce the amoung of 'noise' in our image, allowing us to find edges more accurately. Since we are looking for lanes specifically, we should isolate the image for the colors, white and yellow. We filter everything out except pixels matching our target colors.

![greyscale](https://user-images.githubusercontent.com/11032490/28350624-161c8cf6-6bff-11e7-9470-973216a27122.png)

Now, we can apply a Gaussian blur (also known as Gaussian smoothing) to our image. It is a widely used effect in graphics software, typically to reduce image noise and reduce detail, by averaging the pixels.

![redoverlay](https://user-images.githubusercontent.com/11032490/28350626-177bc562-6bff-11e7-9f4f-c33bef5818a2.png)

This is where we can finally apply our Canny Line Detection - edge detection algorithm.
In essence, the library (canny()) pulls out the pixels values according to their gradient (directional derivative). The remainder of the image are the edges, exactly what we are lookign for. These edges are found where there is a large deviation in at least one direction.

Now, remember our field of concentration, we pair our mask to only focus on the area where there should be lane lines.

Finally, we apply our Hough transformation. Thhis algorithm determines if there is enough evidence of a straight line at that pixel. Once we have our two master lines, we can average our line image with the original, unaltered image of the road to have a nice, smooth overlay. complete = cv2.addWeighted(initial_img, alpha, line_image, beta, lambda).

[![FinalOverlay](https://user-images.githubusercontent.com/11032490/28350648-4cd24808-6bff-11e7-8aaf-53c796e796be.png)](https://youtu.be/-PijZN-qmTs)

Watch Video, by clicking on image above.

------------------------------------------------------------------------------------------------------------------------
2. Identify potential shortcomings with your current pipeline

One potential shortcoming would be what would happen when the car is driving in on roads with construction. A good example is the 101 near Palo Alto right now. The road has different lane markers. Also, the asphalt changes color and height, which could affect the edge detection.

Another shortcoming could be weather conditions. The lack thereof reducundancy sensors. 

------------------------------------------------------------------------------------------------------------------------

3. Suggest possible improvements to your pipeline

A possible improvement would be to take into consideration weather, or different light conditions.

Another potential improvement could be to extrapolate the lane direction, by using the edge of the road, the lane's average width over the last 30 minutes, and use it to measure from the left edge. This would have another set of overlaid lines, acting a secondary guide.
