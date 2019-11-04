## Types of Features

**Edges**: Areas in an image where the intensity abruptly changes\(Areas with high intensity gradient\)

**Corners**:  At the intersection of two edges\(Most repeatable feature between similar images\)

**Blobs**:  Region based features; areas of extreme brightness or unique textures

**Corner Detectors**

![](/assets/Screenshot 2019-11-03 at 9.39.27 AM.png)![](/assets/Screenshot 2019-11-03 at 9.43.50 AM.png)![](/assets/Screenshot 2019-11-03 at 9.44.00 AM.png)![](/assets/Screenshot 2019-11-03 at 9.49.19 AM.png)![](/assets/Screenshot 2019-11-03 at 9.38.50 AM.png)the magnitude should be calculated as the sum of the Gx\(Sobel x\) and Gy\(Sobel y\) components.`rho = sqrt(Gx^2 + Gy^2)`.

## Dilation and Erosion {#dilation-and-erosion}

Dilation and erosion are known as **morphological operations**. They are often performed on binary images, similar to contour detection. Dilation enlarges bright, white areas in an image by adding pixels to the perceived boundaries of objects in that image. Erosion does the opposite: it removes pixels along object boundaries and shrinks the size of objects.

Often these two operations are performed in sequence to enhance important object traits!

### Dilation {#dilation}

To dilate an image in OpenCV, you can use the`dilate`function and three inputs: an original binary image, a kernel that determines the size of the dilation \(None will result in a default size\), and a number of iterations to perform the dilation \(typically = 1\). In the below example, we have a 5x5 kernel of ones, which move over an image, like a filter, and turn a pixel white if any of its surrounding pixels are white in a 5x5 window! We’ll use a simple image of the cursive letter “j” as an example.

```
# Reads in a binary image
image = cv2.imread(‘j.png’, 0) 

# Create a 5x5 kernel of ones
kernel = np.ones((5,5),np.uint8)

# Dilate the image
dilation = cv2.dilate(image, kernel, iterations = 1)
```

### Erosion {#erosion}

To erode an image, we do the same but with the`erode`function.

```
# Erode the image
erosion = cv2.erode(image, kernel, iterations = 1)
```

### ![](/assets/Screenshot 2019-11-03 at 12.20.06 PM.png)Opening

As mentioned, above, these operations are often\_combined\_for desired results! One such combination is called**opening**, which is**erosion followed by dilation**. This is useful in noise reduction in which erosion first gets rid of noise \(and shrinks the object\) then dilation enlarges the object again, but the noise will have disappeared from the previous erosion!

To implement this in OpenCV, we use the function`morphologyEx`with our original image, the operation we want to perform, and our kernel passed in.

```
opening = cv2.morphologyEx(image, cv2.MORPH_OPEN, kernel)
```

### ![](/assets/Screenshot 2019-11-03 at 12.21.22 PM.png)Closing

**Closing**is the reverse combination of opening; it’s**dilation followed by erosion**, which is useful in\_closing\_small holes or dark areas within an object.

Closing is reverse of Opening, Dilation followed by Erosion. It is useful in closing small holes inside the foreground objects, or small black points on the object.

```
closing = cv2.morphologyEx(img, cv2.MORPH_CLOSE, kernel)
```

### ![](/assets/Screenshot 2019-11-03 at 12.22.13 PM.png)Image Segmentation

Now that we are familiar with a few simple feature types, it may be useful to look at how we can group together different parts of an image by using these features. Grouping or segmenting images into distinct parts is known as image segmentation.

The simplest case for image segmentation is in background subtraction. In video and other applications, it is often the case that a human has to be isolated from a static or moving background, and so we have to use segmentation methods to distinguish these areas. Image segmentation is also used in a variety of complex recognition tasks, such as in classifying every pixel in an image of the road.

A couple ways to segment an image:

1. using contours to draw boundaries around different parts of an image, and
2. clustering image data by some measure of color or texture similarity.

### **Contouring**

![](/assets/Screenshot 2019-11-04 at 7.43.48 AM.png)[https://opencv-python-tutroals.readthedocs.io/en/latest/py\_tutorials/py\_imgproc/py\_contours/py\_table\_of\_contents\_contours/py\_table\_of\_contents\_contours.html](https://opencv-python-tutroals.readthedocs.io/en/latest/py_tutorials/py_imgproc/py_contours/py_table_of_contents_contours/py_table_of_contents_contours.html)

### K-means clustering![](/assets/Screenshot 2019-11-04 at 8.07.54 AM.png)



