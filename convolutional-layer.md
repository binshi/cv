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

### ![](/assets/Screenshot 2019-10-30 at 4.39.09 PM.png)Hough Transform

[http://homepages.inf.ed.ac.uk/rbf/HIPR2/hough.htm](http://homepages.inf.ed.ac.uk/rbf/HIPR2/hough.htm)

![](/assets/Screenshot 2019-10-30 at 4.43.33 PM.png)![](/assets/Screenshot 2019-10-30 at 4.47.53 PM.png)![](/assets/Screenshot 2019-10-30 at 4.44.46 PM.png)OpenCV Hough space: [https://opencv-python-tutroals.readthedocs.io/en/latest/py\_tutorials/py\_imgproc/py\_houghlines/py\_houghlines.html](https://opencv-python-tutroals.readthedocs.io/en/latest/py_tutorials/py_imgproc/py_houghlines/py_houghlines.html)

### Haar  Cascades

[https://www.cs.cmu.edu/~efros/courses/LBMV07/Papers/viola-cvpr-01.pdf](https://www.cs.cmu.edu/~efros/courses/LBMV07/Papers/viola-cvpr-01.pdf)

### Features

Features and feature extraction is the basis for many computer vision applications. The idea is that any set of data, such as a set of images, can be represented by a smaller, simpler model made of a combination of visual features: a few colors and shapes. \(This is true with one exception: completely random data!\)

If you can find a good model for any set of data, then you can start to find ways to identify patterns in data based on similarities and differences in the features in an image. This is especially important when we get to deep learning models for image classification, which you'll see soon.

#### Types of Features

We've described features as measurable pieces of data in an image that help distinguish between different classes of images.

There are two main types of features:

1. Color-based and
2. Shape-based

Both of these are useful in different cases and they are often powerful together. We know that color is all you need should you want to classify day/night images or implement a green screen. Let's look at another example: say I wanted to classify a stop sign vs. any other traffic sign. Stop signs are_supposed_to stand out in color and shape! A stop sign is an octagon \(it has 8 flat sides\) and it is very red. It's red color is often enough to distinguish it, but the sign can be obscured by trees or other artifacts and the shape ends up being important, too.

As a different example, say I want to detect a face and perform facial recognition. I'll first want to detect a face in a given image; this means at least recognizing the boundaries and some features on that face, which are all determined by shape. Specifically, I'll want to identify the edges of the face and the eyes and mouth on that face, so that I can identify the face and recognize it. Color is not very useful in this case, but shape is critical.

#### A note on shape

Edges are one of the simplest shapes that you can detect; edges often define the boundaries between objects but they may not provide enough information to find and identify small features on those objects \(such as eyes on a face\) and in the next videos, we'll look at methods for finding even more complex shapes.

As you continue learning, keep in mind that selecting the right feature is an important computer vision task.

## Example Application: Lane Finding {#example-application-lane-finding}

You've already had some practice with this concept, but you can use feature/edge detection and color transforms to very effectively detect lane lines on a road. If you'd like to learn more about this technique, I suggest checking out: [https://towardsdatascience.com/teaching-cars-to-see-advanced-lane-detection-using-computer-vision-87a01de0424f](https://towardsdatascience.com/teaching-cars-to-see-advanced-lane-detection-using-computer-vision-87a01de0424f)



