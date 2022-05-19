# CVImagePreprocessingTechniques
Road To Pixels
Welcome aboard. With the growing technologies out in the world, we have seen how important Image Processing has become. This repository provides a complete understanding of the practical implementation of all the concepts to be known for a developer to start their Image Processing journey.

Contents
Basics with Images
Successive Rotations
Interpolations
Interpolations-Inverse Mapping
Basic Transformations
Perspective Transofrmation
Estimating the Transformation
Log and Contrast Stretching
Shading Correction
Laplacian
Laplacian+Gaussian
Laplacian, Sobel, CannyEdge
Sobel-X and Y
Histogram Equalisation
Normalize Histogram
Image Temperature
Box Filter
GaussianFilter+Kernels
Morphological Processing
Morphological Text Processing
Morphological Fingerprint Processing
Morphological Outline
Capture Video Frames
Video background Subtraction
VideoCapture_GoogleColab
Contours-OpenCV
Fitting Polygons
Hough Lines
Adaptive+Gaussian Thresholding
OTSU Thresholding
Grabcut
Discrete Fourier Transformation
OpenCV KMeans
Object Movement Tracking
Live Hand Gesture Recognition
Before we jump into the concepts, let us once have a look at the definition of Image Processing.

A Glance into Image Processing
Image processing is often viewed as arbitrarily manipulating an image to achieve an aesthetic standard or to support a preferred reality. However, image processing is more accurately defined as a means of translation between the human visual system and digital imaging devices. The human visual system does not perceive the world in the same manner as digital detectors, with display devices imposing additional noise and bandwidth restrictions. Salient differences between the human and digital detectors will be shown, along with some basic processing steps for achieving translation. Image processing must be approached in a manner consistent with the scientific method so that others may reproduce, and validate one's results. This includes recording and reporting processing actions and applying similar treatments to adequate control images.Src

There are two types of methods used for image processing namely, analog and digital image processing. Analog image processing can be used for hard copies like printouts and photographs. Various fundamentals of interpretation are used by the Image Analysts along with the visual techniques. Digital image processing deals with the manipulation of digital images through a digital computer. It is a subfield of signals and systems but focuses particularly on images. The three general phases that all types of data have to undergo while using digital techniques are

Pre-processing
Enhancement and Display
Information Extraction.
Fundamental Steps in DIP Fundamental Steps in Digital Image Processing - Rafael Gonzalez - 4th Edition Src

Important point to note while going through any concept is that the image is considered on a greyscale since color increases the complexity of the model. One may want to introduce an image processing tool using gray level images because of the format of gray-level images because the inherent complexity of gray-level images is lower than that of color images. In most cases. after presenting a gray-level image method, it can be extended to color images.

For getting deeper insights into any of the concepts, I suggest going through Digital Image Processing, Rafael C. Gonzalez • Richard E. Woods, 4th Edition

From here on I will be referring Digital Image Processing as DIP.

Disclaimer: I am not the original author of the images used. They have been taken from various Image Processing sites. I have mentioned all of the referenced sites in resources. Pardon if I missed any.

The following is the order I suggest to look into the concepts.

1. Basics with Images - Averaging Images
Image averaging is a DIP technique that is used to enhance the images which are corrupted with random noise. The arithmetic mean of the intensity values for each pixel position is computed for a set of images of the same view field. The basic formula behind it is.
Image Averaging over set of N images

2. Successive Rotations - Code
The images are rotated using the self-defined code for rotation instead of the OpenCV inbuilt function. When an image is rotated by 45 degrees for 8 times, it does not produce the same result as when it is rotated by 90 degrees for 4 times. This is because, when an image is rotated 45 degrees, during the rotation more pixels values for the new position of the pixels are to be calculated. And calculating these new pixel positions and their intensities uses interpolation which is an approximation method. So when an image is rotated by 90 degrees there is a smoother transition since fewer no of approximations are to be made for the new pixel positions and their intensities.

A clear example is shown below

Rotated by 45 deg - 8 times	Rotated by 90 deg - 4 times
	
3. Interpolations - Code
Interpolation is used in tasks such as zooming, shrinking, rotating, and geometrically correcting digital images. It is the process of using known data to estimate values at unknown locations. So for giving the chance to estimate values, we will do some transformation, here it is a rotation by 45 degrees. The 3 interpolations we see here are:

Nearest Neighbour	Bilinear	Bicubic
		
Here you can see a slight variation between the 3 images. The smoothness gets better from left to right. Since Bicubic interpolation uses a higher-order equation it can capture features in-depth.

4. Interpolation-Inverse Mapping - Code
As mentioned here, there are two methods of mapping, the first, called forward mapping, scans through the source image pixel by pixel, and copies them to the appropriate place in the destination image. The second, reverse mapping, goes through the destination image pixel by pixel and samples the correct pixel from the source image. The most important feature of inverse mapping is that every pixel in the destination image gets set to something appropriate. In the forward mapping case, some pixels in the destination might not get painted and would have to be interpolated. We calculate the image deformation as a reverse mapping.

Original	Nearest Neighbour - Inverse Mapping
	
5. Basic Transformations - Code
We have seen the basic transformations like rotation and scaling. Now let's see one more basic transformation known as translation.

Original	Translation
	
6. Perspective Transformation - Code
The perspective transformation deals with the conversion of a 3D image into a 2D image for getting better insights about the required information. The 3D object co-ordinates are changed into the co-ordinates wrt world frame of reference and according to camera coordinate frame reference then continued by changing into Image Plane 2D coordinates and then to the pixel coordinates.

Distorted Image	OpenCV - Perspective Transf Function	Manual Correction
		
7. Est. Transformation - Code
This is just an example of using custom transformations for the required purpose. In the below example I have tried to extract the root part from the image.

Original	Transformed
	
8. Log and Contrast Stretching - Code
One of the grey-level transformations is Logarithmic Transformation. It is defined as s = c*log(r+1) , where 's' and 'r' are the pixel values of the output and the input image respectively and 'c' is a constant.

Original	Log-Transformed
	
Contrast Stretching is a simple image enhancement technique that attempts to improve the contrast in an image by stretching the range of intensity values it contains to span a desired range of values.

Original	Contrast Stretched
	
9. Shading Correction - Code
Shading Correction is used for correcting the parts of an image which are having some faults due to multiple reasons like, camera light obstruction. So correcting the image for the required purpose is essential. So in this example, we have used a faulty image of a chessboard and corrected the image. Gaussian Blur is used to correct the shading in the corner of the image.

Original	Corrected Image
	
10. Laplacian - Code
A Laplacian filter is an edge detector which computes the second derivatives of an image, measuring the rate at which the first derivatives change. That determines if a change in adjacent pixel values is from an edge or continuous progression. A laplacian filter or kernel looks like this:
[0, 1, 0]
[1, -4, 1]
[0, 1, 0]

But a point to note is that Laplacian is very sensitive to noise. It even detects the edges for the noise in the image.

Original	Laplacian Filter
	
11. Laplacian+Gaussian - Code
As you can see from the above example, the Laplacian kernel is very sensitive to noise. Hence we use the Gaussian Filter to first smoothen the image and remove the noise. And then the Laplacian Filter is applied for better results.

Laplacian	Gaussian and Laplacian
	
12. Laplacian, Sobel, CannyEdge - Code
The Sobel filter is used for edge detection. It works by calculating the gradient of image intensity at each pixel within the image. There are two sobel filters- SobelX and SobelY
SobelX | SobelY
[-1, 0, 1] [-1, -2, -1]
[-2, 0, 2] [ 0, 0, 0]
[-1, 0, 1] [ 1, 2, 1]

Original	SobelX	SobelY
		
But the important thing to note here is, we have to pad the image before applying these filters to preserve the features of the image at the edges. I have used zero-padding here to pad the image on the four sides.

Canny Edge Detection is a multi-stage algorithm consisting of the following:

Noise Reduction - Since edge detection is susceptible to noise in the image, the first step is to remove the noise in the image with a 5x5 Gaussian filter.
Intensity Gradient - Smoothened image is then filtered with a Sobel kernel in both horizontal and vertical directions to get the first derivative in the horizontal direction (Gx) and vertical direction (Gy). 
Non-Maximum Suppression - After getting gradient magnitude and direction, a full scan of an image is done to remove any unwanted pixels which may not constitute the edge. For this, at every pixel, the pixel is checked if it is a local maximum in its neighborhood in the direction of the gradient.
Hysteresis Thresholding - This stage decides which are all edges are edges and which are not. For this, we need two threshold values, minVal and maxVal. Any edges with an intensity gradient more than maxVal are considered to be edges and those below minVal are considered to be non-edges, so discarded. Those who lie between these two thresholds are classified edges or non-edges based on their connectivity. If they are connected to "sure-edge" pixels, they are considered to be part of edges. Otherwise, they are also discarded. This is an excerpt from OpenCV Canny Edge Detection.
Original	Canny Edge
	
13. Sobel-X and Y - Code
As we have seen Laplacian previously, let's compare it with the Sobel Filters.

Laplacian	SobelX	SobelY
		
Because of the second-order derivatives in Laplacian, this gradient operator is more sensitive to noise than first-order gradient operators. Also, the thresholded magnitude of the Laplacian operator produces double edges. For these reasons, together with its inability to detect the edge direction, the Laplacian as such is not a good edge detection operator. Better utilization of it is to use its zero-crossing to detect the edge locations.

14. Histogram Equalisation - Code
A histogram of an image is nothing but the graphical representation of the intensity distribution of an image, quantifying the number of pixels for each intensity value. Histogram Equalization a method that improves the contrast in an image, to stretch out the intensity range.

As per OpenCV Documentation:

Equalization implies mapping one distribution (the given histogram) to another distribution (a wider and more uniform distribution of intensity values) so the intensity values are spread over the whole range.

To accomplish the equalization effect, the remapping should be the cumulative distribution function (CDF) (more details, refer to Learning OpenCV). For the histogram H(i), its cumulative distribution H′(i) is: 

So, here I take an example image, plot its histogram and then equalize it.

Original Hist	Equalized Hist
	
How the image looks after equalizing the histogram.



15. Normalize Histogram - Code
Image Normalization is a process in which we change the range of pixel intensity values to make the image more familiar or normal to the senses. Often image normalization is used for increasing contrast and removing noise. In a normalized image Mean = 0 and Variance = 1. In the following example, there is a very slight change, which may or may not be visible to us at times. But the main concept behind normalization is to bring the intensity values to a normal level which can be used for further processing.

Equalized Hist	Normalized Hist
	
16. Image Temperature - Code
To increase the temperature of an image, I have used the Look-up Table(LUT) and Univariate Spline. A LUT transformation assigns a new pixel value to each pixel in the input image according to the values given by a table. In this table, the index represents the input intensity value and the content of the cell given by the index represents the corresponding output value. A Univariate Spline is a one-dimensional smoothing spline that fits a given set of data points.

Original	Temperature Increase
	
17. Box Filter - Code
By convolving the image with a normalized box filter, it takes the average of all the pixels under the kernel area and replaces the central element with this average. Either of cv2.blur() or cv2.boxFilter() can be used for the same.

Original	Box Filter
	
18. GaussianFilter+Kernels - Code
Instead of a box filter consisting of equal filter coefficients, a Gaussian kernel is used before applying the other edge-detection kernels for better results. Gaussian Filter is very effective in removing the Gaussian noise and improves the accuracy of the other kernels like Laplacian and Sobel. To show the exact working of Laplacian and Sobel, I had used Gaussian Filter in the previous implementations. Because those kernels are not effective without Gaussian Blurring, I haven't shown that.

19. Morphological Processing -Code
Morphological transformations are some simple operations based on the image shape. And they are performed on binary images with the help of kernels which decide the nature of the operation. Some of the most used operations are:

Erosion - It erodes the boundaries of the foreground object. All the pixels near boundary will be discarded depending upon the size of the kernel
Dilation - It is just the opposite of erosion. It increases the white region in the image or the size of the foreground object increases.
Opening - Erosion followed by dilation is called opening.
Closing - Dilation followed by Erosion is called closing.
Morphological Gradient - Difference between Dilation and erosion of an image.
Erosion	Dilation
	
Opening	Closing
	
20. Morphological Text Processing - Code
I have used multiple combinations of the above mentioned morphological operations to enhance an image of text. I am mentioning some of the processed images here. For more images, please got to the Code here.

Original	Processed 1	Processed 2
		
21. Morphological Fingerprint Processing - Code
In this example too, I have tried out different combinations possible with various kernel sizes to give better insights into the morphological operations and their effects on an image.

Original	Improved
	
22. Morphological Outline - Code
It is the difference between dilation and erosion of an image.

drawing

23. Capture Video Frames - Code
OpenCV function for capturing video frames is vid = cv2.VideoCapture. Using vid.read() we can fetch each fram from the video.

24. Video background Subtraction - Code
For subtracting a static background from the vido0 frames I have used multiple methods. The first one is to iteratively subtract the background image from each frame and then display it on the screen. The other method consists of using cv2.createBackgroundSubtractorMOG2() in OpenCV and creating a mask with that background subtractor. After background subtraction, I have used various thresholding methods for enhancing the objects entering into the video frames(since every time the background gets subtracted, the new objects get highlighted). I have used Adaptive thresholding, Inverse Binary thresholding, and drew contours on them for extra effects.

25. VideoCapture_GoogleColab - Code
This is a script for enthusiasts working in various projects in Google Colab which uses the webcam. Since Google Colab has no access to our hardware, we need to use this script for enabling webcam. This is not my code and has been taken from here for better reach.

26. Contours-OpenCV - Code
Contours are nothing but simple curves that join all the continuous points along the boundary of an object which have similar characteristics like color or intensity. It is very helpful for object shape analysis, object recognition and, etc. For better accuracy, we use binary images. So before finding contours, we should apply threshold or canny edge detection.

The cv2.findContours function has three arguments, the first one is the source image, the second is contour retrieval mode, third is the contour approximation method. And it outputs a modified image, the contours, and hierarchy. I have used this function and traced out the contours on the following images. We can also find the largest contour of all contours in an image by doing a max of it.

Original	Color-Contours	Contours-GreyScale
		
27. Fitting Polygons - Code
The approach we would be used to detect the shape of a given polygon will be based on classifying the detected shape based on the number of sides it has. For example, if the detected polynomial has 3 sides, then it could be considered as a triangle, if the polynomial has 4 sides then it could be classified as a square or a rectangle.

I have used the cv2.approxPolyDP function. I have counted the contours with 3 sides, hence counting the number of triangles present in the image.

Original	Polygons Fitted
	
28. Hough Lines - Code
Hough Line Transform is used to detect straight lines in an image. Before applying the transform it is prescribed to perform an edge detection pre-processing. For detailed explanation go here.

OpenCV implements two kinds of Hough Line Transforms:

Standard Hough Transform - cv2.HoughLines()
Probabilistic Hough Transform - cv2.HoughLinesP() I have used the first one here. The explanation of the hough line derivation is out of the scope of this repo and I recommend looking over the above-mentioned site for further in-depth details.
Original	Hough Transformed
	
29. Adaptive+Gaussian Thresholding - Code
In simple thresholding, the threshold value is global, hence is the same for all the pixels in the image. Adaptive thresholding, on the other hand is the method where the threshold value is calculated for smaller regions and therefore, there will be different threshold values for different regions of the image. In OpenCV, you can perform Adaptive threshold operation on an image using the method cv2.adaptiveThreshold() of the Imgproc class.

Original	Global Thresholding	Adaptive Thresholding
		
30. OTSU Thresholding - Code
Otsu's method is a global thresholding technique. It uses the histogram of the image for the threshold searching process. It maximizes "between class variance" of the segmented classes. Otsu proves that Minimizing "within-class variance" is the same as maximizing "between class variance" of the segmented classes. And maximizing "between class variance" is computationally less expensive than minimizing "within-class variance".

Original	Otsu Thresholding
	
31. Grabcut - Code
Grabcut is a foreground extraction algorithm with minimal user interaction. It requires the user to draw a rectangle around the foreground region. Then the algorithm segments it iteratively. Giving strokes on the image will make the algorithm understand that the marked area should be considered as foreground.

 Src

Original	Grabcut
	
32. Discrete Fourier Transformation - Code
Discrete Fourier transformation will transform an image from its spatial domain to its frequency domain. It is based on the idea that any function can be approximated with the sum of infinite sines and cosines. 

f is the image value in its spatial domain and F in its frequency domain. The result of the transformation is complex numbers.

Original	DFT
	
33. OpenCV KMeans - Code
The function kmeans implements a k-means algorithm that finds the centers of cluster_count clusters and groups the input samples around the clusters.
The input parameters given to the function are samples, K(no of clusters), criteria, attempts, flags. In the below example, I have used two criteria at the same time(cv2.TERM_CRITERIA_EPS + cv2.TERM_CRITERIA_MAX_ITER). To know more about these criteria go through the documentation mentioned below once.
The output parameters are compactness, labels, and centers where compactness is the sum of the squared distance from each point to their corresponding centers.

Original	K = 3	K = 5
		
To know more about the KMeans algorithm and usage in terms of OpenCV, check it out here.

34. Object Movement Tracking - Code
Here we try to detect the presence of a colored ball using computer vision techniques and then track the ball as it moves around in the video frames, drawing its previous positions as it moves. I have taken the reference for this particular topic from here. It is a great blog written by Adrian Rosebrock.

Resources
I am mentioning some of the resources which I found very useful during my learning stage.

OpenCV Documentation
PyImageSearch Image Processing Archives
OpenCV Python Tutorials
Rich Radke Channel - Youtube
