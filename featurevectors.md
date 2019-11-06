### Corners and Object Detection

Features alone and together: Now, you've seen examples of shape-based features, like corners, that can be extracted from images, but how can we actually uses the features to detect whole objects? Say we want a way to detect this mountain in other images, too. A single corner will not be enough to identify this mountain in any other images, but, we can take a set of features that define the shape of this mountain, group them together into an array or vector, and then use that set of features to create a mountain detector!

### ![](/assets/Screenshot 2019-11-04 at 5.38.36 PM.png)**ORB\(Oriented fast and Rotated Brief\)**

The ORB algorithm is used to quickly create feature vectors from keypoints in an image. FAST and BRIEF are feature detection and vector creation algorithms resp. ![](/assets/Screenshot 2019-11-04 at 5.47.14 PM.png)![](/assets/Screenshot 2019-11-04 at 5.47.43 PM.png)

### FAST\(**Features from Accelerated Segments Test\):**

Detect keypoints in a given image. FAST compares the brightness of a pixel\(Ip\) with 16 surrounding pixels and is sorted into brighter\(Ip+h\), darker\(Ip-h\) and similar to p.FAST is fast as the same  results can be oobtained by comparing to only 4\(1,5,9,13\) surrounding pixels instead of 16.Keypoints detect the  edges of the image like below. These keypoints only give us the location of the edge and not the direction of the change in intensity.

![](/assets/Screenshot 2019-11-05 at 7.15.13 PM.png)

Given a pixel p in an array fast compares the brightness of p to surrounding 16 pixels that are in a small circle around p. Pixels in the circle is then sorted into three classes \(lighter than p, darker than p or similar to p\). If more than 8 pixels are darker or brighter than p than it is selected as a keypoint. So keypoints found by fast gives us information of the location of determining edges in an image.![](/assets/Screenshot 2019-11-04 at 5.51.46 PM.png)

### 

### BRIEF\(Binary Robust Independent Elementary Features\)

Convert the keypoints detected by FAST and convert them into feature vectors\(binary feature vector\).Binary feature is stored easily in memory and  can be computed fast and can be run with devices with limited memory. Starts by smoothing with a gaussian kernel so that it is not too sensitive to noise. For a pixel, BRIEF selects random pair of pixels in a defined neighborhood called patch which is a square around a pixel.The second pixel is selected from the neighborhood defined by the gaussian distribution with  std deviation sigma. If first pixel is brighter than second pixel then 1 is added else 0 is added  to the vector. Then  2  other random variables are selected.For a 256 bit vector BRIEF repeats it 256 times.

![](/assets/Screenshot 2019-11-04 at 6.18.39 PM.png)

### Scale And Rotation Invariance:

Image pyramid is a multi-scale representation of an image with different resolutions. Then FAST runs to identify the keypoints in the ORB calculates the intensity centroid\(average intensity of a pixel\) in a given patch.  The angle is then calculated by measuring the orientation from the keypoint to  the centroid. It  then repeats for  each different  resolution image without reducing the patch size. This results in keypoints with different sizes. The circles illustrate the sizes of the different keypoints.  Then ORB uses rBrief\(rotation aware BRIEF\) to generate the feature vector. rBrief starts of as regular BRIEF with 256 pixels. It then randomly rotates these pixels according to the orientation angle of the keypoint to align with  the orientation angle of the keypoint. Then rBrief compares the brightness of these pixels and assigns 1s and 0s to make the feature vector. The set of all keypoints is known as the ORB descriptor.  ![](/assets/Screenshot 2019-11-04 at 6.13.42 PM.png)![](/assets/Screenshot 2019-11-04 at 6.15.28 PM.png)![](/assets/Screenshot 2019-11-06 at 8.03.22 AM.png)

### 

### Feature Matching

![](/assets/Screenshot 2019-11-05 at 3.24.05 PM.png)![](/assets/Screenshot 2019-11-05 at 3.25.23 PM.png)

### HOG\(Histogram of Oriented Gradients\)

The HOG algorithm works by creating histograms of the distribution of gradient orientations in an image and then normalizing them in a very special way. This special normalization is what makes HOG so effective at detecting the edges of objects even in cases where the contrast is very low. These normalized histograms are put together into a feature vector, known as the HOG descriptor, that can be used to train a machine learning algorithm, such as a Support Vector Machine \(SVM\), to detect objects in images based on their boundaries \(edges\). Due to its great success and reliability, HOG has become one of the most widely used algorithms in computer vison for object detection.

![](/assets/Screenshot 2019-11-05 at 6.35.25 PM.png)

### The HOG Algorithm

As its name suggests, the HOG algorithm, is based on creating histograms from the orientation of image gradients. The HOG algorithm is implemented in a series of steps:

1. Given the image of particular object, set a detection window \(region of interest\) that covers the entire object in the image \(see Fig. 3\).

2. Calculate the magnitude and direction of the gradient for each individual pixel in the detection window.

3. Divide the detection window into connected\_cells\_of pixels, with all cells being of the same size \(see Fig. 3\). The size of the cells is a free parameter and it is usually chosen so as to match the scale of the features that want to be detected. For example, in a 64 x 128 pixel detection window, square cells 6 to 8 pixels wide are suitable for detecting human limbs.

4. Create a Histogram for each cell, by first grouping the gradient directions of all pixels in each cell into a particular number of orientation \(angular\) bins; and then adding up the gradient magnitudes of the gradients in each angular bin \(see Fig. 3\). The number of bins in the histogram is a free parameter and it is usually set to 9 angular bins.

5. Group adjacent cells into_blocks_\(see Fig. 3\). The number of cells in each block is a free parameter and all blocks must be of the same size. The distance between each block \(known as the stride\) is a free parameter but it is usually set to half the block size, in which case you will get overlapping blocks \(_see video below_\). The HOG algorithm has been shown empirically to work better with overlapping blocks.

6. Use the cells contained within each block to normalize the cell histograms in that block \(see Fig. 3\). If you have overlapping blocks this means that most cells will be normalized with respect to different blocks \(_see video below_\). Therefore, the same cell may have several different normalizations.

7. Collect all the normalized histograms from all the blocks into a single feature vector called the HOG descriptor.

8. Use the resulting HOG descriptors from many images of the same type of object to train a machine learning algorithm, such as an SVM, to detect those type of objects in images. For example, you could use the HOG descriptors from many images of pedestrians to train an SVM to detect pedestrians in images. The training is done with both positive a negative examples of the object you want detect in the image.

9. Once the SVM has been trained, a sliding window approach is used to try to detect and locate objects in images. Detecting an object in the image entails finding the part of the image that looks similar to the HOG pattern learned by the SVM.

![](/assets/Screenshot 2019-11-05 at 6.25.03 PM.png)

### ![](/assets/Screenshot 2019-11-05 at 6.26.22 PM.png)Learning to Find Features

Now that you've seen a number of feature extraction techniques, you should have a good understanding of how different objects and areas in an image can be identified by their unique shapes and colors.

Convolutional filters and ORB and HOG descriptors all rely on patterns of intensity to identify different shapes \(like edges\) and eventually whole objects \(with feature vectors\). You've even seen how k-means clustering can be used to group data without any labels.

