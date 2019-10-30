### Processing pipeline![](/assets/Screenshot 2019-10-29 at 7.49.46 AM.png)Color Spaces![](/assets/Screenshot 2019-10-29 at 11.10.13 AM.png)HSV![](/assets/Screenshot 2019-10-29 at 11.12.55 AM.png)

## Filters {#filters}

Now, we’ve seen how to use color to help isolate a desired portion of an image and even help classify an image!

In addition to taking advantage of color information, we also have knowledge about patterns of grayscale intensity in an image. Intensity is a measure of light and dark similar to brightness, and we can use this knowledge to detect other areas or objects of interest.  
For example, you can often identify the edges of an object by looking at an abrupt change in intensity which happens when an image changes from a very dark to light area.

To detect these changes, you’ll be using and creating specific image filters that look at groups of pixels and detect big changes in intensity in an image. These filters produce an output that shows these edges.

### High and low frequency {#high-and-low-frequency}

Similarly, frequency in images is a**rate of change**. But, what does it means for an image to change? Well, images change in space, and a high frequency image is one where the intensity changes a lot. And the level of brightness changes quickly from one pixel to the next. A low frequency image may be one that is relatively uniform in brightness or changes very slowly. This is easiest to see in an example.

![](/assets/Screenshot 2019-10-30 at 7.25.54 AM.png)

