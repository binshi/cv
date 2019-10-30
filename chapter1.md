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

The Fourier Transform \(FT\) is an important image processing tool which is used to decompose an image into its frequency components. The output of an FT represents the image in the frequency domain, while the input image is the spatial domain \(x, y\) equivalent. In the frequency domain image, each point represents a particular frequency contained in the spatial domain image. So, for images with a lot of high-frequency components \(edges, corners, and stripes\), there will be a number of points in the frequency domain at high frequency values.

Take a look at how FT's are done with OpenCV, [https://docs.opencv.org/3.0-beta/doc/py\_tutorials/py\_imgproc/py\_transforms/py\_fourier\_transform/py\_fourier\_transform.html](https://docs.opencv.org/3.0-beta/doc/py_tutorials/py_imgproc/py_transforms/py_fourier_transform/py_fourier_transform.html)

![](/assets/Screenshot 2019-10-30 at 7.32.06 AM.png)This decomposition is particularly interesting in the context of bandpass filters, which can isolate a certain range of frequencies and mask an image according to a low and high frequency threshold.

The frequency components of an image can be displayed after doing a Fourier Transform \(FT\). An FT looks at the components of an image \(edges that are high-frequency, and areas of smooth color as low-frequency\), and plots the frequencies that occur as points in spectrum. FT treats patterns of intensity in an image as sine waves with a particular frequency, and you can look at an interesting visualization of these sine wave components [https://plus.maths.org/content/fourier-transforms-images](https://plus.maths.org/content/fourier-transforms-images)

