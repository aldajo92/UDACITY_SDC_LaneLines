## Udacity SDC (Self-Driving Car): Finding Lane Lines on the Road ##
---

## Overview ##
In this project, some concepts of computer vision werw implemented to identify lane lanes on the road from images and videos in this context. A pipeline is developed with a series of individual images to validate the concepts required to implement in a video stream, that is the final objective for this project.

## The Project ##
The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road using images
* Reflect verify the result obtained in images in a videostream.

[//]: # (Image References)

[image1]: ./test_images/solidWhiteRight.jpg "Solid white"

[image2]: ./test_images/solidYellowLeft.jpg "Solid white"

[image1_step1]: ./test_images_output/image1_step1.jpg "Step 1: Grayscale"

[image1_step2]: ./test_images_output/image1_step2.jpg "Step 2: Blur"

[image1_step3]: ./test_images_output/image1_step3.jpg "Step 3: Blur"

[image1_step4]: ./test_images_output/image1_step4.jpg "Step 4: Blur"

[image1_step5]: ./test_images_output/image1_step5.jpg "Step 5: Blur"

[image1_step6]: ./test_images_output/image1_step6.jpg "Step 6: Blur"




[image2_step1]: ./test_images_output/image2_step1.jpg "Step 1: Grayscale"

[image2_step2]: ./test_images_output/image2_step2.jpg "Step 2: Blur"

[image2_step3]: ./test_images_output/image2_step3.jpg "Step 3: Blur"

[image2_step4]: ./test_images_output/image2_step4.jpg "Step 4: Blur"

[image2_step5]: ./test_images_output/image2_step5.jpg "Step 5: Blur"

[image2_step6]: ./test_images_output/image2_step6.jpg "Step 6: Blur"

[original_video1]: ./test_videos/solidWhiteRight.mp4 "Solid Yellow Right"

[original_video2]: ./test_videos/solidYellowLeft.jpg "Solid Yellow Left"

[video1]: ./test_videos_output/solidWhiteRight.mp4 "Solid Yellow Right"

[video2]: ./test_videos_output/solidYellowLeft.jpg "Solid Yellow Left"

---

## Pipeline Description ##
This pipeline consist on 6 steps:

* Grayscale: Convert Image to grayscale.
* Gaussian: Apply Gaussian smoothing Module.
* Canny: Apply Canny Edge detection.
* Region: Select Region of interest.
* Hough: Apply Hough Transform to detect lines.
* Draw lines

## Parameters for each step ##

#### Convert Image to grayscale.

This step requires only use the respective operation to convert image to grayscale. Command used was ```grayscale(image)```, that use the following instruction:

```
cv2.cvtColor(img, cv2.COLOR_RGB2GRAY)
```
#### Apply Gaussian smoothing Module.

Similar as the previous step, the command used was ```gaussian_blur(image, kernel_size)``` which use internaly use the following instruction:

```cv2.GaussianBlur(img, (kernel_size, kernel_size), 0)```

Parameter used in kernel size was ```11```. 

#### Apply Canny Edge detection.

Command used was ```canny(image, low_threshold, high_threshold)``` which use the following instruction:

```cv2.Canny(img, low_threshold, high_threshold)```

Parameters used in this command was:
```
low_threshold = 80
high_threshold = 150
```

#### Select Region of interest.

Command used was ```region_of_interest(image, area)```, the parameter ```area``` was calculated with this lines:

```
left_bottom = [0, 539]
right_bottom = [959, 539]
apex = [479, 310]
area = np.array([[left_bottom, right_bottom, apex]], dtype=np.int32)
```

#### Apply Hough Transform to detect lines.

Command used was ```hough_lines(image, rho, theta, threshold, min_line_len, max_line_gap)```, each parameter was defined as follows:

```
rho = 2 # distance resolution in pixels of the Hough grid
theta = np.pi/180 # angular resolution in radians of the Hough grid
threshold = 15     # minimum number of votes (intersections in Hough grid cell)
min_line_len = 15 #minimum number of pixels making up a line
max_line_gap = 20    # maximum gap in pixels between connectable line segments
img_lines = hough_lines(img_region, rho, theta, threshold, min_line_len, max_line_gap)
```

#### Draw lines
Command used was ```weighted_img(image, image)```, each parameter was defined on the following instruction:

## Results on Images ##

#### Solid White: ####
The image, named ```solidWhiteRight.jpg``` was used as the first input to the pipeline.

![image1]

Result obtained is:

Grayscale:
![image1_step1]
Gaussian:
![image1_step2]
Canny:
![image1_step3]
Select Region:
![image1_step4]
Hough Transform:
![image1_step5]
Draw Lines:
![image1_step6]

The image, named ```solidWhiteRight.jpg``` was used as the first input to the pipeline.

#### Solid Yellow: ####
The image, named ```solidYellowCurve2.jpg``` was used as the next input to the pipeline.

![image2]

The result obtained is:

Grayscale:
![image2_step1]
Gaussian:
![image2_step2]
Canny:
![image2_step3]
Select Region:
![image2_step4]
Hough Transform:
![image2_step5]
Draw Lines:
![image2_step6]

## Results on Video ##

The procesing made before was implemented in the videos:

[Solid White Right][original_video1]

[Solid White Left][original_video2]

And the result obtained is (respectively):

[video1]

[video2]

