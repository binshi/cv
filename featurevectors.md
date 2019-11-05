### Corners and Object Detection

Features alone and together: Now, you've seen examples of shape-based features, like corners, that can be extracted from images, but how can we actually uses the features to detect whole objects? Say we want a way to detect this mountain in other images, too. A single corner will not be enough to identify this mountain in any other images, but, we can take a set of features that define the shape of this mountain, group them together into an array or vector, and then use that set of features to create a mountain detector!

### ![](/assets/Screenshot 2019-11-04 at 5.38.36 PM.png)**ORB\(Oriented fast and Rotated Brief\)**

### ![](/assets/Screenshot 2019-11-04 at 5.47.14 PM.png)![](/assets/Screenshot 2019-11-04 at 5.47.43 PM.png)

### FAST\(**Features from Accelerated Segments Test\):**

Given a pixel p in an array fast compares the brightness of p to surrounding 16 pixels that are in a small circle around p. Pixels in the circle is then sorted into three classes \(lighter than p, darker than p or similar to p\). If more than 8 pixels are darker or brighter than p than it is selected as a keypoint. So keypoints found by fast gives us information of the location of determining edges in an image.![](/assets/Screenshot 2019-11-04 at 5.51.46 PM.png)

### BRIEF\(Binary Robust Independent Elementary Features\)

![](/assets/Screenshot 2019-11-04 at 6.18.39 PM.png)

### Scale And Rotation Invariance![](/assets/Screenshot 2019-11-04 at 6.13.42 PM.png)![](/assets/Screenshot 2019-11-04 at 6.15.28 PM.png)

### Feature Matching

![](/assets/Screenshot 2019-11-05 at 3.24.05 PM.png)![](/assets/Screenshot 2019-11-05 at 3.25.23 PM.png)

### HOG\(Histogram of Oriented Gradients\)

![](/assets/Screenshot 2019-11-05 at 6.25.03 PM.png)

![](/assets/Screenshot 2019-11-05 at 6.26.22 PM.png)

