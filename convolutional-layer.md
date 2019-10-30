### Convolutional Layer![](/assets/Screenshot 2019-10-30 at 3.40.44 PM.png)Canny Edge Detection

1. **Filters out noise** using Gaussian blur\(Low pass filter\)

2. **Finds the strength and direction of edges** using Sobel filters\(High pass filters\)

3. **Applies non-maximum suppression** to isolate the striongest edges and thin them to one pixel wide lines

4. Uses **hysteresis to isolate the best edges**. Hysteresis is a double thresholding process.

![](/assets/Screenshot 2019-10-30 at 3.47.00 PM.png)

### Edge Detection

Now that you've seen how to define and use image filters for smoothing images and detecting the edges \(high-frequency\) components of objects in an image, let's move one step further. The next few videos will be all about how we can use what we know about pattern recognition in images to begin identifying unique shapes and then objects.

### Edges to Boundaries and Shapes {#edges-to-boundaries-and-shapes}

We know how to detect the edges of objects in images, but how can we begin to find unifying boundaries around objects? We'll want to be able to do this to separate and locate multiple objects in a given image. Next, we'll discuss the Hough transform, which transforms image data from the x-y coordinate system into Hough space, where you can easily identify simple boundaries like lines and circles.

The Hough transform is used in a variety of shape-recognition applications, as seen in the images pictured below. On the left you see how a Hough transform can find the edges of a phone screen and on the right you see how it's applied to an aerial image of farms \(green circles in this image\).

  


