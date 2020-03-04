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

## Numerical vs. Categorical {#numerical-vs-categorical}

Let's learn a little more about labels. After visualizing the image data, you'll have seen that each image has an attached label: "day" or "night," and these are known as**categorical values**.

Categorical values are typically text values that represent various traits about an image. A couple examples are:

* An "animal" variable with the values: "cat," "tiger," "hippopotamus," and "dog."
* A "color" variable with the values: "red," "green," and "blue."

Each value represents a different category, and most collected data is labeled in this way!

These labels are descriptive for us, but may be inefficient for a classification task. Many machine learning algorithms do not; they require that all output be numerical. Numbers are easily compared and stored in memory, and for this reason, we often have to convert categorical values into**numerical labels**. There are two main approaches that you'll come across:

1. Integer encoding
2. One hot-encoding

### Integer Encoding {#integer-encoding}

Integer encoding means to assign each category value an integer value. So, day = 1 and night = 0. This is a nice way to separate binary data, and it's what we'll do for our day and night images.

### One-hot Encoding {#one-hot-encoding}

One-hot encoding is often used when there are more than 2 values to separate. A one-hot label is a 1D list that's the length of the number of classes. Say we are looking at the animal variable with the values: "cat," "tiger," "hippopotamus," and "dog." There are 4 classes in this category and so our one-hot labels will be a list of length four. The list will be all 0's and one 1; the 1 indicates which class a certain image is.

For example, since we have four classes \(cat, tiger, hippopotamus, and dog\), we can make a list in that order: \[cat value, tiger value, hippopotamus value, dog value\]. In general, order does not matter.

If we have an image and it's one-hot label is`[0, 1, 0, 0]`, what does that indicate?

In order of \[cat value, tiger value, hippopotamus value, dog value\], that label indicates that it's an image of a tiger! Let's do one more example, what about the label`[0, 0, 0, 1]`?

## Average Brightness {#average-brightness}

Here were the steps we took to extract the average brightness of an image.

1. Convert the image to HSV color space \(the Value channel is an approximation for brightness\)
2. Sum up all the values of the pixels in the Value channel
3. Divide that brightness sum by the area of the image, which is just the width times the height.

This gave us one value: the average brightness or the average Value of that image.

In the next notebook, make sure to look at a variety of day and night images and see if you can think of an average brightness value that will separate the images into their respective classes!

The next step will be to feed this data into a classifier. A classifier might be as simple as a conditional statement that checks if the average brightness is above some threshold, then this image is labeled as 1 \(day\) and if not, it’s labeled as 0 \(night\).

On your own, you can choose to create more features that help distinguish these images from one another, and we’ll soon learn about testing the accuracy of a model like this.

  


