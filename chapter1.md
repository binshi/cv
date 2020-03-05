### Processing pipeline![](/assets/Screenshot 2019-10-29 at 7.49.46 AM.png)Color Spaces![](/assets/Screenshot 2019-10-29 at 11.10.13 AM.png)HSV![](/assets/Screenshot 2019-10-29 at 11.12.55 AM.png)

## Filters {#filters}

Now, we’ve seen how to use color to help isolate a desired portion of an image and even help classify an image!

In addition to taking advantage of color information, we also have knowledge about patterns of grayscale intensity in an image. Intensity is a measure of light and dark similar to brightness, and we can use this knowledge to detect other areas or objects of interest.  
For example, you can often identify the edges of an object by looking at an abrupt change in intensity which happens when an image changes from a very dark to light area.

To detect these changes, you’ll be using and creating specific image filters that look at groups of pixels and detect big changes in intensity in an image. These filters produce an output that shows these edges.

### High and low frequency {#high-and-low-frequency}

Similarly, frequency in images is a**rate of change**. But, what does it means for an image to change? Well, images change in space, and a high frequency image is one where the intensity changes a lot. And the level of brightness changes quickly from one pixel to the next. A low frequency image may be one that is relatively uniform in brightness or changes very slowly. This is easiest to see in an example.

![](/assets/Screenshot 2019-10-30 at 7.25.54 AM.png)Most images have both high-frequency and low-frequency components. In the image above, on the scarf and striped shirt, we have a high-frequency image pattern; this part changes very rapidly from one brightness to another. Higher up in this same image, we see parts of the sky and background that change very gradually, which is considered a smooth, low-frequency pattern.

**High-frequency components also correspond to the edges of objects in images**, which can help us classify those objects.

### Fourier Transform

**The Fourier Transform \(FT\) is an important image processing tool which is used to decompose an image into its frequency components**. The output of an FT represents the image in the frequency domain, while the input image is the spatial domain \(x, y\) equivalent. In the frequency domain image, each point represents a particular frequency contained in the spatial domain image. So, for images with a lot of high-frequency components \(edges, corners, and stripes\), there will be a number of points in the frequency domain at high frequency values.

Take a look at how FT's are done with OpenCV, [https://docs.opencv.org/3.0-beta/doc/py\_tutorials/py\_imgproc/py\_transforms/py\_fourier\_transform/py\_fourier\_transform.html](https://docs.opencv.org/3.0-beta/doc/py_tutorials/py_imgproc/py_transforms/py_fourier_transform/py_fourier_transform.html)

![](/assets/Screenshot 2019-10-30 at 7.32.06 AM.png)This decomposition is particularly interesting in the context of bandpass filters, which can isolate a certain range of frequencies and mask an image according to a low and high frequency threshold.

The frequency components of an image can be displayed after doing a Fourier Transform \(FT\). An FT looks at the components of an image \(edges that are high-frequency, and areas of smooth color as low-frequency\), and plots the frequencies that occur as points in spectrum. FT treats patterns of intensity in an image as sine waves with a particular frequency, and you can look at an interesting visualization of these sine wave components [https://plus.maths.org/content/fourier-transforms-images](https://plus.maths.org/content/fourier-transforms-images)

![](/assets/Screenshot 2019-10-30 at 7.43.17 AM.png)Low frequencies are at the center of the frequency transform image.

The transform images for these example show that the solid image has most low-frequency components \(as seen by the center bright spot\).

The stripes tranform image contains low-frequencies for the areas of white and black color and high frequencies for the edges in between those colors. The stripes transform image also tells us that there is one dominating direction for these frequencies; vertical stripes are represented by a horizontal line passing through the center of the frequency transform image.

Next, let's see what this looks like applied to a real-world image.

![](/assets/Screenshot 2019-10-30 at 7.48.14 AM.png)

Notice that this image has components of all frequencies. You can see a bright spot in the center of the transform image, which tells us that a large portion of the image is low-frequency; this makes sense since the body of the birds and background are solid colors. The transform image also tells us that there are **two **dominating directions for these frequencies; vertical edges \(from the edges of birds\) are represented by a horizontal line passing through the center of the frequency transform image, and horizontal edges \(from the branch and tops of the birds' heads\) are represented by a vertical line passing through the center.

![](/assets/Screenshot 2020-03-05 at 9.32.38 AM.png)

### Edge Handling {#edge-handling}

Kernel convolution relies on centering a pixel and looking at it's surrounding neighbors. So, what do you do if there are no surrounding pixels like on an image corner or edge? Well, there are a number of ways to process the edges, which are listed below. It’s most common to use padding, cropping, or extension. In extension, the border pixels of an image are copied and extended far enough to result in a filtered image of the same size as the original image.

**Extend**  
The nearest border pixels are conceptually extended as far as necessary to provide values for the convolution. Corner pixels are extended in 90° wedges. Other edge pixels are extended in lines.

**Padding**  
The image is padded with a border of 0's, black pixels.

**Crop**  
Any pixel in the output image which would require values from beyond the edge is skipped. This method can result in the output image being slightly smaller, with the edges having been cropped.

Unfortunately, while low-pass filtering smooths out noise, high-pass filtering does just the opposite: itamplifies noise. You can get away with this if the original image is not too noisy; otherwise the noise will overwhelm the image. MaxIm DL includes a very useful "range-restricted filter" option; you can high-pass filter only the brightest parts of the image, where the signal-to-noise ratio is highest.

High-pass filtering can also cause small, faint details to be greatly exaggerated. An over-processed image will look grainy and unnatural, and point sources will have dark donuts around them. So while high-pass filtering can often improve an image by sharpening detail, overdoing it can actually degrade the image quality significantly.

### ![](/assets/Screenshot 2019-10-30 at 8.18.23 AM.png)![](/assets/Screenshot 2019-10-30 at 8.19.02 AM.png)Gradients

Gradients are a measure of intensity change in an image, and they generally mark object boundaries and changing area of light and dark. If we think back to treating images as functions,_F\(x, y\)_, we can think of the gradient as a derivative operation_F**’**\(x, y\)_. Where the derivative is a measurement of intensity change.

## Sobel filters {#sobel-filters}

The Sobel filter is very commonly used in edge detection and in finding patterns in intensity in an image. Applying a Sobel filter to an image is a way of **taking \(an approximation\) of the derivative of the image **in the x or y direction. The operators forSobel\_x​ and Sobel\_y​, respectively, look like this:

![](/assets/Screenshot 2019-10-30 at 12.19.39 PM.png)

### ![](/assets/Screenshot 2019-10-30 at 12.25.12 PM.png) {#span-classmathquill-ud-mathxspan-vs-span-classmathquill-ud-mathyspan}

### x vs. y {#span-classmathquill-ud-mathxspan-vs-span-classmathquill-ud-mathyspan}

In the above images, you can see that the gradients taken in both the x and the y directions detect the edges of the brain and pick up other edges. Taking the gradient in the x direction emphasizes edges closer to vertical. Alternatively, taking the gradient in the y direction emphasizes edges closer to horizontal.

![](/assets/Screenshot 2019-10-30 at 12.25.30 PM.png)![](/assets/Screenshot 2019-10-30 at 12.25.24 PM.png)

Open CV filtering: [https://opencv-python-tutroals.readthedocs.io/en/latest/py\_tutorials/py\_imgproc/py\_filtering/py\_filtering.html](https://opencv-python-tutroals.readthedocs.io/en/latest/py_tutorials/py_imgproc/py_filtering/py_filtering.html)

#### **Low pass filter**![](/assets/Screenshot 2019-10-30 at 12.47.34 PM.png)Averaging filter![](/assets/Screenshot 2019-10-30 at 12.48.27 PM.png)

#### Gaussian  filter![](/assets/Screenshot 2019-10-30 at 12.46.12 PM.png)



