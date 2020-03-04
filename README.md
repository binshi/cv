# Computer Vision

![](/assets/Screenshot 2020-03-04 at 8.56.15 AM.png)

## Images as Numerical Data {#images-as-numerical-data}

Every pixel in an image is just a numerical value and, we can also change these pixel values. We can multiply every single one by a scalar to change how bright the image is, we can shift each pixel value to the right, and many more operations!

**Treating images as grids of numbers is the basis for many image processing techniques.**

Most color and shape transformations are done just by mathematically operating on an image and changing it pixel-by-pixel.

OpenCV

[OpenCV](http://opencv.org/) is a popular computer vision library that has meany built in tools for image analysis and understanding!

\_Note:\_In the example above and in later examples, I'm using my own Jupyter notebook and sets of images stored on my personal computer. You're encouraged to set up a similar environment and use images of your own to practice! You'll also be given some code quizzes \(coming up next\), with images provided, to practice these techniques.

#### Why BGR instead of RGB? {#why-bgr-instead-of-rgb}

OpenCV reads in images in BGR format \(instead of RGB\) because when OpenCV was first being developed, BGR color format was popular among camera manufacturers and image software providers. The red channel was considered one of the least important color channels, so was listed last, and many bitmaps use BGR format for image storage. However, now the standard has changed and most image software and cameras use RGB format, which is why, in these examples, it's good practice to initially convert BGR images to RGB before analyzing or manipulating them.

### Color Selection {#color-selection}

To select the most accurate color boundaries, it's often useful to use a[color picker](https://www.w3schools.com/colors/colors_picker.asp)and choose the color boundaries that define the region you want to select!

### Why do we need labels? {#why-do-we-need-labels}

\_You \_can tell if an image is night or day, but a computer cannot unless we tell it explicitly with a label!

This becomes especially important when we are testing the accuracy of a classification model.

A classifier takes in an image as input and should output a`predicted_label`that tells us the predicted class of that image. Now, when we load in data, like you’ve seen, we load in what are called the`true_labels`which are the\_correct\_labels for the image.

To check the accuracy of a classification model, we compare the predicted and true labels. If the true and predicted labels match, then we’ve classified the image correctly! Sometimes the labels do not match, which means we’ve misclassified an image.

### Accuracy {#accuracy}

After looking at many images, the accuracy of a classifier is defined as the number of correctly classified images \(for which the predicted\_label matches the true label\) divided by the total number of images. So, say we tried to classify 100 images total, and we correctly classified 81 of them. We’d have 0.81 or 81% accuracy!

We can tell a computer to check the accuracy of a classifier only when we have these predicted and true labels to compare. We can also learn from any mistakes the classifier makes, as we’ll see later in this lesson.

### Numerical labels {#numerical-labels}

It’s good practice to use numerical labels instead of strings or categorical labels. They're easier to track and compare. So, for our day and night, binary class example, instead of "day" and "night" labels we’ll use the numerical labels: 0 for night and 1 for day.

Okay, now you’re familiar with the day and night image data AND you know what a label is and why we use them; you’re ready for the next steps. We’ll be building a classification pipeline from start to end!

Let’s first brainstorm what steps we’ll take to classify these images.

## Distinguishing and Measurable Traits {#distinguishing-and-measurable-traits}

When you approach a classification challenge, you may ask yourself: how can I tell these images apart? What traits do these images have that differentiate them, and how can I write code to repent their differences. Adding on to that, how can I ignore irrelevant or overly similar parts of these images?

You may have thought about a number of distinguishing features: day images are much brighter, generally, than night images. Night images also have these really bright small spots, so the brightness over the whole image varies a lot more than the day images. There is a lot more of a gray/blue color palette in the day images.

There are lots of measurable traits that distinguish these images, and these measurable traits are referred to as**features**.

A feature a measurable component of an image or object that is, ideally, unique and recognizable under varying conditions - like under varying light or camera angle. And we’ll learn more about features soon.

### Standardizing and Pre-processing {#standardizing-and-pre-processing}

But we’re getting ahead of ourselves! To extract features from any image, we have to pre-process and standardize them!

Next we’ll take a look at the standardization steps we should take before we can consistently extract features.

