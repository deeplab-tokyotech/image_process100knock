# Image Processing 100 Questions

---

This is the English version of image processing 100 questions.  The [original Japanese repository](https://github.com/yoyoyo-yo/Gasyori100knock) was created by [yoyoyo-yo](https://github.com/yoyoyo-yo).  It’s updated by him now.  To be honest, I can not speak Japanese. Since the code is language independent and I’m preparing for my interview questions about computer vision now. I decided to translate the English version of this 100 questions.

Hope this could help more people and thanks for [yoyoyo-yo's](https://github.com/yoyoyo-yo) great effort.  

I'm currently working on ROS and OpenCV, so I'm updating another repository: [OpenCV_for_Beginners](https://github.com/KuKuXia/OpenCV_for_Beginners). Please feel free to fork and pull request.

## Before Reading

1. I’ll use the Google translator to help me understand his original meaning. Pretty cool, right? It’s the time for NLP.
2. I may add some additional materials and my own opinions to this repository.
3. **I’ll discard the irrelevant parts** and mainly focus on the OpenCV parts.

3. I’ll update this as soon as possible since I have to do my research project now.

## Environment Setting

 1. Go to [Miniconda](https://conda.io/miniconda.html) website, download and install it.

 2. Open your terminal, create a virtual environment using following command:

    ```bash
    $ conda create python = 3.6 -n Image_Processing_100
    ```

3. Activate your virtual environment:

   ```bash
   $ source activate Image_Processing_100
   ```

4. Install the packages:

   ```bash
   $ pip install -r requirement.txt
   ```

## Testing Your Environment

1. Clone this repository into your local computer:

   ```bash
   $ git clone git@github.com:KuKuXia/Gasyori100knock.git
   ```

2. In the Image_Processing_100_Questions folder, make a new file named sample.py, copy and paste the following code:

   ```python
   import cv2

   img = cv2.imread("assets/imori.jpg")
   cv2.imshow("imori", img)
   cv2.waitKey(0)
   cv2.destroyAllWindows()
   ```

3. Save the file and run it.
   ```bash
   python ./sample.py
   ```
4. Successful if the following image is displayed with a new window! Then if you press any button, it disappears.


![](assets/sample.png)

 4. Next, see the [Tutorial folder](https://github.com/KuKuXia/Image_Processing_100_Questions/tree/master/Tutorial) to learn `numpy `related to image processing. (Please skip this if you already know.)

 5. From now on, please solve the Question. The Question contents are included in each folder. Please use 	`assets/imori.jpg` in the question. Questions are written in the README.md of each folder.



## Content

​            Question         >>        Folder

- [x] Question 1 - 10   >> Question_01_10
- [x] Question 11 - 20 >> Question_ 11 _ 20
- [x] Question 21 - 30 >> Question_ 21 _ 30
- [x] Question 31 - 40 >> Question_ 31 _ 40
- [x] Question 41 - 50 >> Question_ 41 _ 50
- [ ] Question 51 - 60 >> Question_ 51 _ 60
- [ ] Question 61 - 70 >> Question_ 61 _ 70
- [ ] Question 71 - 80 >> Quesiton_ 71 _ 80
- [ ] Question 81 - 90 >> Question_ 81 _ 90
- [ ] Question 91 - 100 >> Question_ 91 _ 100

## Note

- This paper is a teaching material to learn fundamental knowledge and theory of image processing.
- In the solution, we do not use main () etc. to simplify the code as much as possible.
- We will use numpy, but we do not post basic knowledge about numpy. Please check each one.

## Question

**Unresolved** issues are unanswered

## [Question 1-10](https://github.com/KuKuXia/Image_Processing_100_Questions/tree/master/Question_01_10)

| Number |                           Question                           | Number |                           Question                           |
| :----: | :----------------------------------------------------------: | :----: | :----------------------------------------------------------: |
|   1    |  [Channel swapping](./Question_01_10/1_Channel_Swapping.py)  |   6    | [Discretization of Color](./Question_01_10/6_Discretization_of_Color.py) |
|   2    |         [Grayscale](./Question_01_10/2_Grayscale.py)         |   7    |   [Average Pooling](./Question_01_10/7_Average_Pooling.py)   |
|   3    |      [Binarization](./Question_01_10/3_Binarization.py)      |   8    |       [Max Pooling](./Question_01_10/8_Max_Pooling.py)       |
|   4    | [Binarization of Otsu](./Question_01_10/4_Binarization_of_Otsu.py) |   9    |   [Gaussian Filter](./Question_01_10/9_Gaussian_Filter.py)   |
|   5    |    [HSV Conversion](./Question_01_10/5_HSV_Conversion.py)    |   10   |    [Median Filter](./Question_01_10/10_Median_Filter.py)     |

## [Question 11 - 20](https://github.com/KuKuXia/Image_Processing_100_Questions/tree/master/Question_11_20)

| Number |                           Question                           | Number |                           Question                           |
| :----: | :----------------------------------------------------------: | :----: | :----------------------------------------------------------: |
|   11   | [Smoothing Filter](./Question_11_20/11_Smoothing_Filter.py)  |   16   |   [Prewitt Filter](./Question_11_20/16_Prewitt_Filter.py)    |
|   12   |    [Motion Filter](./Question_11_20/12_Motion_Filter.py)     |   17   | [Laplacian Filter](./Question_11_20/17_Laplacian_Filter.py)  |
|   13   |   [MAX_MIN Filter](./Question_11_20/13_Max_Min_Filter.py)    |   18   |    [Emboss Filter](./Question_11_20/18_Emboss_Filter.py)     |
|   14   | [Differential Filter](./Question_11_20/14_Differential_Filter.py) |   19   |       [LoG Filter](./Question_11_20/19_LoG_Filter.py)        |
|   15   |     [Sobel Filter](./Question_11_20/15_Sobel_Filter.py)      |   20   | [Histogram Display](./Question_11_20/20_Histogram_Display.py) |

## [Question 21 - 30](https://github.com/KuKuXia/Image_Processing_100_Questions/tree/master/Question_21_30)

| Number |                           Question                           | Number |                           Question                           |
| :----: | :----------------------------------------------------------: | :----: | :----------------------------------------------------------: |
|   21   | [Histogram Normalization](./Question_21_30/21_Histogram_Normalization.py) |   26   | [Bi-linear Interpolation](./Question_21_30/26_Bi-linear_Interpolation.py) |
|   22   | [Histogram Operation](./Question_21_30/22_Histogram_Operation.py) |   27   | [Bi-cubic Interpolation](./Question_21_30/27_Bi-cubic_Interpolation.py) |
|   23   | [Histogram Equalization](./Question_21_30/23_Histogram_Equalization.py) |   28   | [Affine transformation (Translation)](./28_Affine_Transformation_Translation.py) |
|   34   | [Gamma Correction](./Question_21_30/24_Gamma_Correction.py)  |   29   | [Affine transformation (Scaling)](./Question_21_30/29_Affine_Transformation_Scaling.py) |
|   25   | [Nearest Neighbor Interpolation](./Question_21_30/25_Nearest_Neighbor_Interpolation.py) |   30   | Affine transformation (Rotation)[v_1](./Question_21_30/30_Affine_Transformation_Rotation_1.py), [v_2](./Question_21_30/30_Affine_Transformation_Rotation_2.py) |

## [Question 31 - 40](https://github.com/KuKuXia/Image_Processing_100_Questions/tree/master/Question_31_40)

| Number |                           Question                           | Number |                           Question                           |
| :----: | :----------------------------------------------------------: | :----: | :----------------------------------------------------------: |
|   31   | [Affine Transformation(Skew)](./Question_31_40/31_Affine_Transformation(Skew).py) |   36   | [JPEG Compression (Step 1) Discrete Cosine Transform](./Question_31_40/36_JPEG_Compression_1_Discrete_Cosine_Transform.py) |
|   32   | [Fourier Transfrom](./Question_31_40/32_Fourier_transform.py) |   37   |             [PSNR](./Question_31_40/37_PSNR.py)              |
|   33   | [Fourier Transform Low Pass Filter](./Question_31_40/33_Fourier_Transform_and_Low_Pass_Filter.py) |   38   | [JPEG Compression (Step 2) DCT + Quantization](./Question_31_40/38_JPEG_Compression_2_DCT_Quantization.py) |
|   34   | [Fourier Transform High Pass Filter](./Question_31_40/34_Fourier_Transform_and_High_Pass_Filter.py) |   39   | [JPEG Compression (Step 3) YCbCr Color System](./Question_31_40/39_JPEG_Compression_3_YCbCr_Color_Space.py) |
|   35   | [Fourier Transform Band Pass Filter](./Question_31_40/35_Fourier_Transform_and_Band_Pass_Filter.py) |   40   | [JPEG Compression (Step 4) YCbCr + DCT + Quantization](./Question_31_40/40_JPEG_compression_4_YCbCr_DCT_Quantization.py) |

## [Question 41 - 50](https://github.com/KuKuXia/Image_Processing_100_Questions/tree/master/Question_41_50)

| Number |                           Question                           | Number |                           Question                           |
| :----: | :----------------------------------------------------------: | :----: | :----------------------------------------------------------: |
|   41   | [Canny Edge Detection (Step 1) Edge Magnitude](Question_41_50/answers/41_Canny_Edge_Detection_1_Edge_Strength.py) |   46   | [Hough Transform / Line Detection (Step. 3) Hough Inverse Transform](Question_41_50/answers/46_Hough_Transform_Line_Detection_3_Hough_Inverse_Transform.py) |
|   42   | [Canny Edge Detection (Step 2) Thinning](./Question_41_50/answers/42_Canny_Edge_Detection_2_Thinning.py) |   47   | [Morphological Processing (Expansion)](Question_41_50/answers/47_Morphological_Processing_Expansion.py) |
|   43   | [Canny Edge Detection (Step 3) Hysteresis Threshold Processing](./Question_41_50/answers/43_Canny_Edge_Detection_3_Hysteresis_Thresholding.py) |   48   | [Morphology Processing (Erosion)](Question_41_50/answers/48_Morphology_Processing_Erosion.py) |
|   44   | [Hough Transform / Line Detection (Step. 1) Hough Transform](Question_41_50/answers/44_Hough_Transform_Line_Detection_1_Hough_Transform.py) |   49   | [Opening Processing](Question_41_50/answers/49_Opening_Process.py) |
|   45   | [Hough Transformation / Line Detection (Step. 2) NMS](Question_41_50/answers/45_Hough_Transform_Line_Detection_2_NMS.py) |   50   | [Closing Processing](Question_41_50/answers/50_Closing_Process.py) |

## [Question 51 - 60](https://github.com/KuKuXia/Image_Processing_100_Questions/tree/master/Question_51_60)

| Number |       Question        | Number |        Question         |
| :----: | :-------------------: | :----: | :---------------------: |
|   51   |  Morphology gradient  |   56   |  Template matching NCC  |
|   52   |  Top hat conversion   |   57   | Template matching ZNCC  |
|   53   | Black hat conversion  |   58   |     Labeling 4 Near     |
|   54   | Template matching SSD |   59   | Labeling 8 neighborhood |
|   55   | Template matching SAD |   60   |       Alpha Blend       |

## [Question 61 - 70](https://github.com/KuKuXia/Image_Processing_100_Questions/tree/master/Question_61_70)

|     Number     |          Problem          | Number |                     Problem                      |
| :------------: | :-----------------------: | :----: | :----------------------------------------------: |
|       61       |    4-connected number     |   66   | HOG (Step 1) Gradient intensity · Gradient angle |
|       62       | 8 - number of connections |   67   |         HOG (Step 2) gradient histogram          |
|       63       |         Thinning          |   68   |       HOG (Step 3) Histogram normalization       |
| 64 **not yet** |    Hiruditchi thinning    |   69   |      HOG (Step 4) Drawing feature quantity       |
|       65       |    Zhang-Suen thinning    |   70   |                  Color tracking                  |

## [Problem 71 - 80](https://github.com/KuKuXia/Image_Processing_100_Questions/tree/master/Question_71_80)

|     Number     |          Problem          | Number |                     Problem                      |
| :------------: | :-----------------------: | :----: | :----------------------------------------------: |
|       61       |    4-connected number     |   66   | HOG (Step 1) Gradient intensity · Gradient angle |
|       62       | 8 - number of connections |   67   |         HOG (Step 2) gradient histogram          |
|       63       |         Thinning          |   68   |       HOG (Step 3) Histogram normalization       |
| 64 **not yet** |    Hiruditchi thinning    |   69   |      HOG (Step 4) Drawing feature quantity       |
|       65       |    Zhang-Suen thinning    |   70   |                  Color tracking                  |

## Reference
https://github.com/KuKuXia/Image_Processing_100_Questions
