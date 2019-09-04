# Q. 41 - 50

## Q.41.  Canny Edge Detection (Step. 1) Edge Magnitude

Q.41-43 is the theory of Canny method, which is one of the edge detection methods.

The Canny method is

1. Apply Gaussian filter
2. Apply Sobel filters in the x and y directions and find edge magnitude and edge slope from them
3. Thinning the edge by Non-maximum suppression from the value of edge gradient
4. Perform threshold processing with hysteresis

By the above, it is the method of extracting an edge part from an image.

Here, the processing of 1 and 2 is implemented.

The procedure is

1. Grayscale the image
2. Apply Gaussian filter (5x5, s = 1.4)
3. A sobel filter is applied in the x direction and the y direction to obtain the gradient image fx, fy of the image, and the gradient magnitude and the gradient angle are determined by the following equations.

```bash
Gradient Magnitude = sqrt(fx^2 + fy^2)
Slope angle tan = arctan(fy / fx)
```

4. The gradient angle is quantized according to the following equation.

```bash
angle = {   0  (if -0.4142 < tan <= 0.4142)
           45  (if  0.4142 < tan < 2.4142)
           90  (if  |tan| >= 2.4142)
          135  (if -2.4142 < tan <= -0.4142)
```

However, when padding filtering, use numpy.pad () and pad with the edge value.

|Input (imori.jpg) |Output(Gradient Magnitude) (answers/answer_41_1.jpg)|Output(Gradient Angle) (answers/answer_41_2.jpg)|
|:---:|:---:|:---:|
|![](./answers/imori.jpg)|![](answers/answer_41_1.jpg)|![](answers/answer_41_2.jpg)|

Answer >> [answers/41_Canny_Edge_Detection_1_Edge_Strength.py](./answers/41_Canny_Edge_Detection_1_Edge_Strength.py)

## Q.42. Canny Edge Detection (Step 2) Thinning

Non-maximum suppression is performed from the gradient angle determined in Q. 41, and the edge line is thinned (thin line).

Non-maximum suppression (NMS) is a general term for the work of removing other than non-maximum values. (This name often goes well with other tasks)

Here, three gradient strengths of adjacent pixels in the direction normal to the gradient angle at the point of interest are compared, and if the maximum value is used, the value is unchanged and if it is not the maximum value, the intensity is 0.

That is, while focusing on the gradient strength edge (x, y), edge (x, y) is changed by the gradient angle angle (x, y) as in the following equation.

```bash
if angle (x, y) = 0
  if edge (x, y) is not the maximum at if edge (x, y), edge (x-1, y), edge (x + 1, y) 
  then edge (x, y) = 0
if angle (x, y) = 45
  if edge (x, y), edge (x-1, y + 1), edge (x + 1, y-1) edge (x, y) is not the largest
  then edge (x, y) = 0
if angle (x, y) = 90
  if edge (x, y), edge (x, y-1), edge (x, y + 1) edge (x , y) is not the maximum
  then edge (x, y) = 0
if angle (x, y) = 135
  if edge (x, y), edge (x-1, y-1), edge (x + 1, edge) edge (x, y) is not the largest
  then edge (x, y) = 0
```

|Input (imori.jpg) |Output (answers/answer_42.jpg)|
|:---:|:---:|
|![](./answers/imori.jpg)|![](answers/answer_42.jpg)|

Answer >> [answers/42_Canny_Edge_Detection_2_Thinning.py](answers/42_Canny_Edge_Detection_2_Thinning.py)

## Q.43. Canny Edge Detection (Step. 3) Hysteresis Thresholding

We will implement 4 here. This is the end of the Canny method.

Here, the gradient strength is binarized by the threshold, but in the Canny method, two thresholds (HT: high threshold and LT: low threshold) are used.

First of all,

1. Edge (x, y) = 255 if the gradient strength edge (x, y) is larger than HT
2. Edge (x, y) = 0 if smaller than LT
3. When LT <edge (x, y) <HT, edge (x, y) = 255 if there is a value larger than HT with gradient intensity of 8 pixels around

Here, HT = 100 and LT = 30. Incidentally, the value of the threshold can only be determined while looking at the result.

The Canny method is performed by the above algorithm.

|Input (imori.jpg) |Output (answers/answer_43.jpg)|
|:---:|:---:|
|![](./answers/imori.jpg)|![](answers/answer_43.jpg)|

Answer >> [answers/43_Canny_Edge_Detection_3_Hysteresis_Thresholding.py](answers/43_Canny_Edge_Detection_3_Hysteresis_Thresholding.py)

## Q.44. Hough Transform / Line Detection (Step. 1) Hough Transform

In Q.44-46, straight line detection using Hough transform is performed.

The Hough transform is a method of detecting a constant shape such as a straight line or a circle along an equation by converting coordinates from rectangular coordinates to polar coordinates. When converted to polar coordinates, a straight point intersects at a constant r, t. The point is a parameter representing a straight line to be detected, and the equation of the straight line can be obtained by inversely transforming this parameter.

As a method

1. Perform Hough transform from edge image to edge pixels.
2. Take a histogram of the values after Hough transform, and select the maximum point.
3. The values of r and t at the maximum point are Hough inverse transformed to obtain the parameters of the detected straight line.

It becomes.

Here, a Hough transform of 1 is performed to create a histogram.

The algorithm is

1. Find the diagonal length rmax of the image
2. Perform Hough transform according to the following equation while changing t once at t = 0-179 at the edge location (x, y)

```bash
r = x * cos(t) + y * sin(t)
```
3. Prepare a table of size 180 x rmax and add 1 to table (t, r) obtained in 1.

This is, in other words, voting (boarding), and voting concentrates on certain points.

This time, use *torino.jpg* to illustrate the *boarded* table. Use Canny's parameters with gaussian filter (5x5, s = 1.4), HT = 100, LT = 30.

|Input (thorino.jpg) |Output (answers/answer_44.jpg)|
|:---:|:---:|
|![](./answers/thorino.jpg)|![](answers/answer_44.jpg)|

Answer >> [answers/44_Hough_Transform_Line_Detection_1_Hough_Transform.py](./answers/44_Hough_Transform_Line_Detection_1_Hough_Transform.py)

## Q.45. Hough Transform / Line Detection (Step. 2) NMS

We will implement 2 here.

In the table obtained in Q.44, many votes are cast near a certain place. Here, the operation to extract the local maximum value is performed.

This time, draw out the top 10 places with a lot of boarding, and draw them.

NMS algorithm is

1. In the table, if the number of votes for the pixel of interest is greater than the eight surrounding squares (near eight), it remains unchanged.
2. Set to 0 if the value of the pixel of interest is small.

|Input (thorino.jpg) |Output (answers/answer_45.jpg)|
|:---:|:---:|
|![](./answers/thorino.jpg)|![](answers/answer_45.jpg)|

Answer >> [answers/45_Hough_Transform_Line_Detection_2_NMS.py](./answers/45_Hough_Transform_Line_Detection_2_NMS.py)

## Q.46.  Hough Transform / Line Detection (Step. 3) Hough Inverse Transform

Here, the maximum value obtained in Q. 45 is Hough inverse transformed to draw a straight line. This completes the straight line detection by the Hough transform.

The algorithm is

1. The local maximum point (r, t) is inversely transformed by the following equation.

```bash
y = - cos(t) / sin(t) * x + r / sin(t)
x = - sin(t) / cos(t) * y + r / cos(t)
```

2. Perform inverse transformation of 1 at y = 0-H -1, x = 0-W-1 for each local maximum point, and draw a detected straight line in the input image. However, red line (R, G, B) = (255, 0, 0) is to be drawn.

|Input (thorino.jpg) |Output (answers/answer_46.jpg)|
|:---:|:---:|
|![](./answers/thorino.jpg)|![](answers/answer_46.jpg)|

Answer >> [answers/46_Hough_Transform_Line_Detection_3_Hough_Inverse_Transform.py](answers/46_Hough_Transform_Line_Detection_3_Hough_Inverse_Transform.py)

## Q.47. Morphological Processing (Dilatation)

*Imori.jpg* is Otsu's binarized, and expansion can be performed twice by morphological processing.

The morphological process is a process of expanding a white (255) mass portion of a binarized image to four neighborhoods (one upper and lower left and right squares) or shrinking it by one mass.

By repeating this expansion and contraction many times, it is possible to erase the white squares present in only one square (Q. 49. Opening process), or combine the white squares that you want to be connected originally (Q. 50. closing process) .

The dilation algorithm for morphological processing is as follows: I (x, y-1), I (x-1, y), I (x + 1, y), I at the target pixel I (x, y) = 0 If any one of (x, y + 1) is 255, then I (x, y) = 255.

That is, if the above process is performed twice, it can be expanded by two squares.

For example, if the sum of [[0,1,0], [1,0,1], [0,1,0]] after filtering is 255 or more, it is considered as dilation.

|Input (imori.jpg) |Otsu’s Binarization (answers/answer_4.jpg)|Output (answers/answer_47.jpg)|
|:---:|:---:|:---:|
|![](./answers/imori.jpg)|![](answers/answer_4.jpg)|![](answers/answer_47.jpg)|

Answer >> [answers/47_Morphological_Processing_Expansion.py](answers/47_Morphological_Processing_Expansion.py)

## Q.48. Morphology Processing (Erosion)

*Imori.jpg* is Otsu's *binarized* and can be shrunk twice by morphological processing.

The shrinkage algorithm (Erosion) algorithm for morphological processing is as follows: I (x, y-1), I (x-1, y), I (x + 1, y), I If any one of (x, y + 1) is 0, then I (x, y) = 0.

For example, consider a contraction if the filtered sum of [[0,1,0], [1,0,1], [0,1,0]] is less than 255 * 4.

|Input (imori.jpg) |大津の二値化(answers/answer_4.jpg)|Output (answers/answer_48.jpg)|
|:---:|:---:|:---:|
|![](./answers/imori.jpg)|![](answers/answer_4.jpg)|![](answers/answer_48.jpg)|

Answer >> [answers/48_Morphology_Processing_Erosion.py](answers/48_Morphology_Processing_Erosion.py)

## Q.49. Opening Process

**After Otsu's binarization** , an opening process (N = 1) can be performed.

The opening process is a process in which expansion is performed N times after the shrinkage of the morphology process is performed N times.

By the opening process, it is possible to delete one extra pixel and the like.

|Input (imori.jpg) |大津の二値化(answers/answer_4.jpg)|Output (answers/answer_49.jpg)|
|:---:|:---:|:---:|
|![](./answers/imori.jpg)|![](answers/answer_4.jpg)|![](answers/answer_49.jpg)|

Answer >> [answers/49_Opening_Process.py](answers/49_Opening_Process.py)

## Q.50. Closing Process

**After Canny detection** , closing processing (N = 1) can be performed.

The closing process is a process in which contraction is performed N times after expansion of the morphology process is performed N times.

By the closing process, it is possible to combine interrupted pixels.

|Input (imori.jpg) |Canny(answers/answer_43.jpg)|Output (answers/answer_50.jpg)|
|:---:|:---:|:---:|
|![](./answers/imori.jpg)|![](answers/answer_43.jpg)|![](answers/answer_50.jpg)|

Answer >> [answers/50_Closing_Process.py](answers/50_Closing_Process.py)
