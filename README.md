# Vehicle Detection
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

<img src="writeup_images/overview.PNG" width="920" alt="Combined Image" />

### Overview
In this project, we will use write a software pipeline to detect vehicles in a video (start with the test_video.mp4 and later implement on full project_video.mp4) however the main product is to create a detailed writeup of the project.

### Goals
- Histogram of Oriented Gradients (HOG)
  - Feature extraction on a labeled training set of images 
  - Train a classifier Linear SVM classifier using selected HOG features
- Sliding Window Search (SWS)
  - Implement a SWS technique
  - Use trained classifier to search for vehicles in images.
- Video Implementation
  - The SWS plus classifier has been used to search for and identify vehicles in the videos provided. 
  - Implement some kind of filter for false positives and some method for combining overlapping bounding boxes.
- Reflection

### Files


### Loading and Visualizing the data
- Datasets provided by Udacity
  - [Car Images](https://s3.amazonaws.com/udacity-sdc/Vehicle_Tracking/vehicles.zip)
  - [NonCar Images](https://s3.amazonaws.com/udacity-sdc/Vehicle_Tracking/non-vehicles.zip)
  - Example of random sample images from the vehicle and non-vehicle datasets.
<img src="output_images/data_visualization.png" width="920" alt="Combined Image" />


### Histogram of Oriented Gradients (HOG) 
#### Feature extraction from training images(HOW) and final parameters.

**HOG FINAL PARAMETERS**
```
color_space = 'YCrCb' 
orient = 9  
pix_per_cell = 8 
cell_per_block = 2
hog_channel = "ALL"
```

The **get_hog_features** function takes in an image and computes the Histogram of Oriented Gradient (HOG).
Takes image as input and HOG parameters **(orientations, pixels_per_cell, cells_per_block)**

**Sample Result of Different HOG parameters**

| SVM Accuracy | Orientation | Pixels Per Cell| Feature Vector Length| Time|
|:------------:|:-----------:|:--------------:|:--------------------:|----:|
|98.59%|11|16|2|4356|237|
|98.45%|9|16|2|4140|110|
|97.38%|11|16|2|4356|104|
|97.61%|9|16|2|4140|107|
|**98.62%**|9|8|2|8460|103|

Color Space mainly used were RGB, YUV, YCrCb.

###### **Accuracy and Time taken were considered when finalizing HOG Parameters**


### Histogram of Oriented Gradients (HOG) 
#### Training classifier using selected HOG featres

**SVM Classifier** with the default classifier parameters using HOG features as indicated above was able to achieve test accuracy of **98.62%**.  Features were scaled to zero mean  and unit variance before training the classifier using sklearn's **StandardScaler** (slection for training/testing radomised using np's random).


### Sliding Window Search

<img src="writeup_images/sliding-final.PNG" alt="Sliding" />

* Implement a sliding-window technique and use your trained classifier to search for vehicles in images.
* Run your pipeline on a video stream (start with the test_video.mp4 and later implement on full project_video.mp4) and create a heat map of recurring detections frame by frame to reject outliers and follow detected vehicles.
* Estimate a bounding box for vehicles detected.

Some example images for testing your pipeline on single frames are located in the `test_images` folder.  To help the reviewer examine your work, please save examples of the output from each stage of your pipeline in the folder called `ouput_images`, and include them in your writeup for the project by describing what each image shows.    The video called `project_video.mp4` is the video your pipeline should work well on.  
