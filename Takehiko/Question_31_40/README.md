# Q. 31 - 40

## Q.31. Affine Transformation (Skew)

1. Create an X-sharing (dx = 30) image like output (1) by using affine transformation.
2. Create a Y-sharing (dy = 30) image such as output (2) by using affine transformation.
3. Create a geometrically transformed (dx = 30, dy = 30) image such as output (3) by using affine transformation.

Such an image is called a skewed image and is obtained by extending an image in an oblique direction.

In the case of output (1), the image stretched by dx in the x direction is called X-sharing.

In the case of output (2), the image stretched by dy in the y direction is called Y-sharing.

It an be realized by affine transformation of the following formulas. However, it is assumed that the size of the original image is h, x, w.

```bash
(1) X-sharing                  (2) Y-sharing
   a = dx / h                     a = dy / w

  x'       1 a tx    x           x'       1 0 tx    x
[ y' ] = [ 0 1 ty ][ y ]       [ y' ] = [ a 1 ty ][ y ]
  1        0 0  1    1           1        0 0  1    1
```

|Input (imori.jpg)|Output (1) (answer_31_1.jpg)|Output (2) (answer_31_2.jpg)|Output (3) (answer_31_3.jpg)|
|:---:|:---:|:---:|:---:|
|![](imori.jpg)|![](answer_31_1.jpg)|![](answer_31_2.jpg)|![](answer_31_3.jpg)|

answer >> [31_Affine_Transformation(Skew).py](./31_Affine_Transformation(Skew).py)

## Q.32. Fourier Transform

### Detail: 

	1. Implement two-dimensional Discrete Fourier Transform (DFT) and display the power spectrum of the frequency of *imori.jpg* grayscale. 
 	2. Then restore the image with two-dimensional Inverse Discrete Fourier transform (IDFT).

The two-dimensional Discrete Fourier transform (DFT) is a processing method for Fourier transform of an image.

Usually the  Fourier transform is a calculation process for obtaining a frequency component of a one-dimensional object with continuous value such as an analog signal or voice.

The two-dimensional Discrete Fourier transform (DFT) is calculated by the following equation.

```bash
K = 0:W, l = 0:H, input image as I
G(k,l) = Sum_{y=0:H-1, x=0:W-1} I(x,y) exp( -2pi * j * (kx/W + ly/H)) / sqrt(H * W)
```

Here you can grayscale the image and then perform two-dimensional Discrete Fourier transform.

The power spectrum is to find the absolute value of G since G is represented by a complex number. 

Scale the power spectrum to [0, 255] when displaying images only this time.

The two-dimensional  Inverse Discrete Fourier transform (IDFT) is a method of restoring the original image from the frequency component G and is defined by the following equation.

```bash
x = 0:W, y = 0:H  
I(x,y) = Sum_{l=0:H-1, k=0:W-1} G(k,l) exp( 2pi * j * (kx/W + ly/H)) / sqrt(H * W)
```

| Input (imori.jpg) | Grayscale (imori_gray.jpg) | Output (answer_32.jpg) | Power spectrum (answer_32_ps.py) |
| :---------------: | :------------------------: | :--------------------: | :------------------------------: |
|  ![](imori.jpg)   |    ![](imori_gray.jpg)     |   ![](answer_32.jpg)   |      ![](answer_32_ps.jpg)       |

answer >> [32_Fourier_Transform.py](./32_Fourier_Transform.py)

## Q.33. Fourier Transform and Low Pass Filter

Use DFT for *imori.jpg* grayscale, and then restore the image using IDFT through a low pass filter.

Frequency components obtained by DFT include lower frequency components as they are closer to the upper left, upper right, lower left, and the higher frequency components as they are closer to the center.

The high frequency component in the image indicates a portion where the color is changed (noise, outline, etc.), and the low frequency component indicates the portion where the color has not changed much (such as the gradation of the sunset).

In this case, implement a **low pass filter** that cuts high frequency components and only passes low frequency components .

Here, if the distance from the center of the low frequency to the high frequency is r, components less than 0.5r are passed.

|Iuput (imori.jpg)|Grayscale (imori_gray.jpg)|Output (answer_33.jpg)|
|:---:|:---:|:---:|
|![](imori.jpg)|![](imori_gray.jpg)|![](answer_33.jpg)|

answer >> [33_Fourier_Transform_and_Low_Pass_Filter.py](./33_Fourier_Transform_and_Low_Pass_Filter.py)

## Q.34. Fourier Transform and High Pass Filter

Use DFT for *imori.jpg* grayscale, and then restore the image using IDFT through a high pass filter.

In this case, implement a **high-pass filter** that cuts low frequency components and only passes high frequency components .

Here, if the distance from the center of the low frequency to the high frequency is r, components greater than 0.2r are passed.

|Input (imori.jpg)|Grayscale (imori_gray.jpg)|Output (answer_34.jpg)|
|:---:|:---:|:---:|
|![](imori.jpg)|![](imori_gray.jpg)|![](answer_34.jpg)|

answer >> [34_Fourier_Transform_and_High_Pass_Filter.py](./34_Fourier_Transform_and_High_Pass_Filter.py)

## Q.35. Fourier Transform and Band Pass Filter

Use DFT for *imori.jpg* grayscale, and then restore the image using IDFT through a band pass filter.

In this case, implement a **band pass filter** that only passes intermediate frequency components between low-frequency and high-frequency components .

Here, if the distance from the center of the low frequency to the high frequency is r, components from 0.1r to 0.5r are passed.

|Input (imori.jpg)|Grayscale (imori_gray.jpg)|Output (answer_35.jpg)|
|:---:|:---:|:---:|
|![](imori.jpg)|![](imori_gray.jpg)|![](answer_35.jpg)|

answer >> [35_Fourier_Transform_and_Band_Pass_Filter.py](./35_Fourier_Transform_and_Band_Pass_Filter.py)

## Q.36. JPEG Compression (Step 1) Discrete Cosine Transform

*Grayscale imori.jpg* to perform discrete cosine transform and inverse discrete cosine transform.

Discrete Cosine Transformation (DCT) is one of the frequency transformations defined by the following equation.

```bash
T = 8
F(u,v) = 1 / T * C(u)C(v) * Sum_{y=0:T-1} Sum_{x=0:T-1} f(x,y) cos((2x+1)u*pi/2T) cos((2y+1)v*pi/2T)
```

Inverse Discrete Cosine Transformation (IDCT) is the inverse (decoding) of discrete cosine transform and is defined by the following equation.

```bash
f(x,y) = 1 / T * C(x)C(y) * Sum_{u=0:T-1} Sum_{v=0:T-1} F(u,v) cos((2x+1)u*pi/2T) cos((2y+1)v*pi/2T)
```

Here, the image is divided into 8 × 8 areas, and the above DCT and IDCT are applied to the jpeg repeatedly in each area. 

This time, it is similarly divided into 8x8 areas, and DCT and IDCT can be performed.

|Input (imori.jpg)|Grayscale (imori_gray.jpg)|Output (1) (answer_36.jpg)|
|:---:|:---:|:---:|
|![](imori.jpg)|![](imori_gray.jpg)|![](answer_36.jpg)|

answer >> [36_JPEG_Compression_1_Discrete_Cosine_Transform](./36_JPEG_Compression_1_Discrete_Cosine_Transform.py)

## Q.37. PSNR

If the DCT coefficient used in IDCT is not 8 but 4 the image is degraded. Determine the PSNR of the input image and the IDCT image. Also find the bit rate by IDCT.

The peak signal to noise ratio (PSNR) is called signal-to-noise ratio, and indicates how much the image has deteriorated.

A larger PSNR indicates that the image is not degraded and is defined by the following equation. MAX is the maximum value that can be taken. If [0, 255] is displayed, then MAX = 255. Also, MSE is called Mean Squared Error (mean squared error), and indicates the average value of the squares of differences between two images.


```bash
PSNR = 10 * log10(MAX^2 / MSE)
MSE = Sum_{y=0:H-1} Sum_{x=0:W-1} (I1(x,y) - I2(x,y))^2 / (HW)
```

The bit rate is defined by the following equation when DCT is performed at 8 × 8 and coefficients of K × K are used in IDCT.

```bash
bitrate = 8 * K^2 / 8^2
```

|Input (imori.jpg)|Grayscale|Output (answer_37.jpg) (PSNR = 27.62, Bitrate=2.0)|
|:---:|:---:|:---:|
|![](imori.jpg)|![](imori_gray.jpg)|![](answer_37.jpg)|

answer >> [37_PSNR](./37_PSNR.py)

## Q.38. JPEG Compression (Step 2) DCT + Quantization

Quantize the DCT coefficients and restore with IDCT. Also compare the capacity of the image at that time.

Quantizing DCT coefficients is a method used in coding to make a jpeg image.

Quantization is an operation of roughly rounding a value into predetermined sections, and is a calculation similar to floor, ceil, round and the like.

In a JPEG image, DCT coefficients are quantized according to a quantization table represented below. This quantization table was taken from the specifications of the jpeg group. In quantization, divide the 8x8 coefficient by Q and round off. It is then done by multiplying Q. All coefficients are used in IDCT.

```bash
Q = np.array(((16, 11, 10, 16, 24, 40, 51, 61),
              (12, 12, 14, 19, 26, 58, 60, 55),
              (14, 13, 16, 24, 40, 57, 69, 56),
              (14, 17, 22, 29, 51, 87, 80, 62),
              (18, 22, 37, 56, 68, 109, 103, 77),
              (24, 35, 55, 64, 81, 104, 113, 92),
              (49, 64, 78, 87, 103, 121, 120, 101),
              (72, 92, 95, 98, 112, 100, 103, 99)), dtype=np.float32)
```

It can be seen that the amount of data has been reduced because quantization reduces the image capacity.

|Input (imori.jpg)|Grayscale(9kb)|Output (answer_38.jpg) (7kb)|
|:---:|:---:|:---:|
|![](imori.jpg)|![](imori_gray.jpg)|![](answer_38.jpg)|

answer >> [38_JPEG_Compression_2_DCT_Quantization](./38_JPEG_Compression_2_DCT_Quantization.py)

## Q.39.  JPEG compression (Step. 3) YCbCr Color Space

In the YCbCr color apace, darken the contrast by multiplying Y by 0.7.

The YCbCr color system is an expression method of decomposing an image into Y representing brightness, a difference Cb between brightness and blue level, and a difference Cr between brightness and red level.

This is used in JPEG conversion.

The conversion from RGB to YCbCr is as follows.

```bash
Y = 0.299 * R + 0.5870 * G + 0.114 * B
Cb = -0.1687 * R - 0.3313 * G + 0.5 * B + 128
Cr = 0.5 * R - 0.4187 * G - 0.0813 * B + 128
```

The conversion from YCbCr to RGB is as follows.

```bash
R = Y + (Cr - 128) * 1.402
G = Y - (Cb - 128) * 0.3441 - (Cr - 128) * 0.7139
B = Y + (Cb - 128) * 1.7718
```

|Input (imori.jpg)|Output (answer_39.jpg) |
|:---:|:---:|
|![](imori.jpg)|![](answer_39.jpg)|

answer >> [39_JPEG_Compression_3_YCbCr_Color_Space](./39_JPEG_Compression_3_YCbCr_Color_Space.py)

## Q.40. JPEG compression (Step. 4) YCbCr + DCT + Quantization

In YCbCr color space, after DCT, quantize Y with quantization table Q1, Cb and Cr with Q2, and restore the image with IDCT. Also compare the capacity of the images.

This is a method for reducing the amount of data actually used in JPEG, and Q1 and Q2 are defined by the following equations in accordance with the JPEG specification.

```bash
Q1 = np.array(((16, 11, 10, 16, 24, 40, 51, 61),
               (12, 12, 14, 19, 26, 58, 60, 55),
               (14, 13, 16, 24, 40, 57, 69, 56),
               (14, 17, 22, 29, 51, 87, 80, 62),
               (18, 22, 37, 56, 68, 109, 103, 77),
               (24, 35, 55, 64, 81, 104, 113, 92),
               (49, 64, 78, 87, 103, 121, 120, 101),
               (72, 92, 95, 98, 112, 100, 103, 99)), dtype=np.float32)

Q2 = np.array(((17, 18, 24, 47, 99, 99, 99, 99),
               (18, 21, 26, 66, 99, 99, 99, 99),
               (24, 26, 56, 99, 99, 99, 99, 99),
               (47, 66, 99, 99, 99, 99, 99, 99),
               (99, 99, 99, 99, 99, 99, 99, 99),
               (99, 99, 99, 99, 99, 99, 99, 99),
               (99, 99, 99, 99, 99, 99, 99, 99),
               (99, 99, 99, 99, 99, 99, 99, 99)), dtype=np.float32)
```

|Input (imori.jpg) (13kb)|Output (answer_40.jpg) (8kb)|
|:---:|:---:|
|![](imori.jpg)|![](answer_40.jpg)|

answer >>  [40_JPEG_compression_4_YCbCr_DCT_Quantization](./40_JPEG_compression_4_YCbCr_DCT_Quantization.py)

