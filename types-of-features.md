## Types of Features

**Edges**: Areas in an image where the intensity abruptly changes\(Areas with high intensity gradient\)

**Corners**:  At the intersection of two edges\(Most repeatable feature between similar images\)

**Blobs**:  Region based features; areas of extreme brightness or unique textures

**Corner Detectors**

![](/assets/Screenshot 2019-11-03 at 9.39.27 AM.png)![](/assets/Screenshot 2019-11-03 at 9.43.50 AM.png)![](/assets/Screenshot 2019-11-03 at 9.44.00 AM.png)![](/assets/Screenshot 2019-11-03 at 9.49.19 AM.png)![](/assets/Screenshot 2019-11-03 at 9.38.50 AM.png)the magnitude should be calculated as the sum of the Gx\(Sobel x\) and Gy\(Sobel y\) components.`rho = sqrt(Gx^2 + Gy^2)`.

## Dilation and Erosion {#dilation-and-erosion}

Dilation and erosion are known as **morphological operations**. They are often performed on binary images, similar to contour detection. Dilation enlarges bright, white areas in an image by adding pixels to the perceived boundaries of objects in that image. Erosion does the opposite: it removes pixels along object boundaries and shrinks the size of objects.

Often these two operations are performed in sequence to enhance important object traits!

