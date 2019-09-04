# Q. 21 - 30


## Q.21. Histogram Normalization

### Detail：Implement histogram normalization.

It can be seen that the histogram has a bias. For example, if there are many pixels close to 0, the image will be dark overall, and if there are many pixels close to 255, the image will be bright. The local bias of the histogram is expressed as a **narrow dynamic range** . Therefore, processing such as normalization and flattening of the histogram is necessary to make the image easy to be viewed by the human eye.

This histogram normalization is called **gray-scale transformation,** and can be realized by the following equation when converting an image having pixel values of [c, d] into a range of [a, b]. This time, *imori_dark.jpg* is converted to the range of [0, 255] respectively.

```bash
xout = { 
          a                         (xin < c)
         (b-a)/(d-c) * (xin-c) + a  (c <= xin <= d)
          b                         (d < xin)
        }
```

|Input (imori_dark.jpg)|Output (answer_21_1.jpg) |Histogram (answer_21_2.png)|
|:---:|:---:|:---:|
|![](imori_dark.jpg)|![](answer_21_1.jpg)|![](answer_21_2.png)|

Answer >> [21_Histogram_Normalization.py](./21_Histogram_Normalization.py)

## Q.22. Histogram Operation

Operate the mean value of the histogram so that $m_0$ = 128 and the standard deviation $s_0$ = 52.

This is not a change in the dynamic range of the histogram but an operation to change the histogram to be flat. To achieve this, the conversion is performed according to the following equation.

```bash
xout = s0/s s * (xin - m) + m0
```

|Input (imori.jpg)|Output (answer_22_1.jpg) |Histogram (answer_22_2.png)|
|:---:|:---:|:---:|
|![](imori.jpg)|![](answer_22_1.jpg)|![](answer_22_2.png)|

Answer >>[22_Histogram_Operation.py](./22_Histogram_Operation.py)

## Q.23. Histogram Equalization

### Detail: Implement histogram flattening.

Histogram flattening is an operation for changing the histogram to be flat, and is an operation for balancing the histogram values without requiring the above-mentioned average value or standard deviation.

This is defined by the following equation. 

- S: total number of pixel values
- Zmax: maximum value of pixel values
- h (z): frequency of density z

```bash
Z' = Zmax / S * Sum{i=0:z} h(z)
```

|Input (imori.jpg)|Output (answer_23_1.jpg) |Histogram (answer_23_2.png)|
|:---:|:---:|:---:|
|![](imori.jpg)|![](answer_23_1.jpg)|![](answer_23_2.png)|

Answer >> [23_Histogram_Equalization.py](./23_Histogram_Equalization.py)


## Q.24. Gamma Correction

### Detail: *Perform* gamma correction (c = 1, g = 2.2) on *imori_gamma.jpg* .

Gamma correction is correction when pixel values are converted non-linearly via a device such as a camera. When an image is displayed as it is on a display or the like, the screen becomes dark. **Therefore, it is an object of gamma correction to perform image display excluding the characteristics of the display by increasing the values of RGB in advance.**

The non-linear transformation is shown in the following equation. 

- x: is normalized to [0, 1]. 
- c: constant
- g: gamma characteristic (usually 2.2)

```bash
x' = c * Iin ^ g
```

Therefore, gamma correction is performed by the following equation.

```bash
Iout = (1/c * Iin) ^ (1/g)
```

![](question_24_1.jpg) ![](question_24_2.jpg)

|Input (imori_gamma.jpg)|Output (answer_24.jpg)|
|:---:|:---:|
|![](imori_gamma.jpg)|![](answer_24.jpg)|

Answer >> [24_Gamma_Correction.py](./24_Gamma_Correction.py)


## Q.25. Nearest Neighbor Interpolation

### Detail: Enlarge the image 1.5 times by nearest neighbor interpolation.

Nearest neighbor interpolation is a method of using the nearest pixel as it is when enlarging an image. Simple and fast processing speed, but the image quality is significantly degraded.

Interpolated by the following equation. 

- I ': the image after enlargement,
- I: the image before enlargement
- a: the magnification
- []: rounding off

```bash
I'(x,y) = I([x/a], [y/a])
```
|Input (imori.jpg)|Output (answer_25.jpg)|
|:---:|:---:|
|![](imori.jpg)|![](answer_25.jpg)|

Answer >> [25_Nearest_Neighbor_Interpolation.py](./25_Nearest_Neighbor_Interpolation.py)

## Q.26. Bi-linear Interpolation

### Detail：Enlarge the image 1.5 times with Bi-linear interpolation.

Bi-linear interpolation is a method of complementing by weighting the four surrounding pixels according to the distance. Although the processing time is increased as the amount of calculation is large, deterioration of the image quality can be suppressed.

1. The coordinates (x’, y’ ) of the magnified image are divided by the magnification ratio a to obtain floor (x '/ a, y' / a).
2. Four pixels around (x '/ a, y' / a) of the original image, I (x, y), I (x + 1, y), I (x, y + 1), I (x + 1, y + 1)

```bash
I(x,y)    I(x+1,y) 
     * (x'/a,y'/a)
I(x,y+1)  I(x+1,y+1)
```

3. The distance d between each pixel and (x '/ a, y' / a) is determined and weighted. w = d / Sum d
4. The pixel (x ′, y ′) of the enlarged image is determined by the following equation. dx = x '/ a-x, dy = y' / a-y
```bash
I'(x',y') = (1-dx)(1-dy)I(x,y) + dx(1-dy)I(x+1,y) + (1-dx)dyI(x,y+1) + dxdyI(x+1,y+1)
```

|Input (imori.jpg)|Output (answer_26.jpg)|
|:---:|:---:|
|![](imori.jpg)|![](answer_26.jpg)|

Answer >> [26_Bi-linear_Interpolation.py](./26_Bi-linear_Interpolation.py)

## Q.27. Bi-cubic Interpolation

### Detail: Enlarge the image 1.5 times by Bi-cubic interpolation.

Bi-cubic interpolation is an extension of Bi-linear interpolation, and performs interpolation from surrounding 16 pixels.

```bash
I(x-1,y-1)  I(x,y-1)  I(x+1,y-1)  I(x+2,y-1)
I(x-1,y)    I(x,y)    I(x+1,y)    I(x+2,y)
I(x-1,y+1)  I(x,y+1)  I(x+1,y+1)  I(x+2,y+1)
I(x-1,y+2)  I(x,y+2)  I(x+1,y+2)  I(x+2,y+2)
```

The distance to each pixel is determined as in the following equation.

```bash
dx1 = x'/a - (x-1) , dx2 = x'/a - x , dx3 = (x+1) - x'/a , dx2 = (x+2) - x'/a
dy1 = y'/a - (y-1) , dy2 = y'/a - y , dy3 = (y+1) - y'/a , dy2 = (y+2) - y'/a
```

The weight is determined by the distance according to the following function: a is often -1.

```bash
h(t) = { (a+2)|t|^3 - (a+3)|t|^2 + 1    (when |t|<=1)
         a|t|^3 - 5a|t|^2 + 8a|t| - 4a  (when 1<|t|<=2)
         0                              (when 2<|t|) 
```

Using these pixels and weights, the pixels of the enlarged image are calculated by the following equation. The sum of each pixel multiplied by the weight is divided by the sum of the weights.

```bash
I'(x', y') = (Sum{i=-1:2}{j=-1:2} I(x+i,y+j) * wxi * wyj) / Sum{i=-1:2}{j=-1:2} wxi * wyj
```

|Input (imori.jpg)|Output (answer_27.jpg)|
|:---:|:---:|
|![](imori.jpg)|![](answer_27.jpg)|

Answer >>[27_Bi-cubic_Interpolation.py](./27_Bi-cubic_Interpolation.py)

## Q.28.  Affine Transformation (Translation)

Translate the image by +30 in the x direction and -30 in the y direction using affine transformation.

Affine transformation is an operation that transforms an image using a 3 × 3 matrix.

The conversion is (1) translation (Q. 28) (2) scaling (Q. 29) (3) rotation (Q. 30) (4) skew (Q. 31).

The original image is (x, y), and the converted image is (x ', y'). The scaling of the image is expressed by the following equation.

```bash
[ x' ] = [a b][x]
  y'      c d  y
```

On the other hand, parallel movement is expressed by the following equation.

```bash
[ x' ] = [x] + [tx]
  y'      y  +  ty
```

Summarizing the above into one equation, we obtain the following equation, which is an affine transformation.

```bash
  x'       a b tx    x
[ y' ] = [ c d ty ][ y ]
  1        0 0  1    1
```

The following equation is used for parallel movement.

```bash
  x'       1 0 tx    x
[ y' ] = [ 0 1 ty ][ y ]
  1        0 0  1    1
```

|Input (imori.jpg)|Output (answer_28.jpg)|
|:---:|:---:|
|![](imori.jpg)|![](answer_28.jpg)|

Answer >> [28_Affine_Transformation_Translation](./28_Affine_Transformation_Translation.py)

## Q.29. Affine Transformation (Scaling)

(1) Resize 1.3 times in x direction 

(2) 0.8 times in y direction using affine transformation.

Also, in addition to the conditions of (2) and (1), simultaneously realize parallel movement of +30 in the x direction and -30 in the y direction.

|Input (imori.jpg)|Output (1) (answer_29_1.jpg)|Output (2) (answer_29_2.jpg)|
|:---:|:---:|:---:|
|![](imori.jpg)|![](answer_29_1.jpg)|![](answer_29_2.jpg)|

Answer >> [29_Affine_Transformation_Scaling](./29_Affine_Transformation_Scaling.py)

## Q.30. Affine Transformation (Rotation)

(1) Rotate 30 degrees counterclockwise using affine transformation.

(2) Use the affine transformation to create an image that can be seen in the entire image rotated counterclockwise by 30 degrees. (However, if a simple affine transformation is performed, the image will be cut off, so some ingenuity is required.)

In the affine transformation, when rotating counterclockwise by A degrees, the following equation is obtained.

```bash
  x'       cosA -sinA tx    x
[ y' ] = [ sinA  cosA ty ][ y ]
  1         0     0    1    1
```

|Input (imori.jpg)|Output (1) (answer_30_1.jpg)|Output (2) (answer_30_2.jpg)|
|:---:|:---:|:---:|
|![](imori.jpg)|![](answer_30_1.jpg)|![](answer_30_2.jpg)|

Answer >> [30_Affine_Transformation_Rotation_1](./30_Affine_Transformation_Rotation_1.py),  [30_Affine_Transformation_Rotation_2](./30_Affine_Transformation_Rotation_2.py)
