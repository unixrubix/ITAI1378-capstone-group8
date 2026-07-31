# ITAI1378-capstone-group8

## Backyard Bird Identification using Computer Vision

Computer Vision course midterm. Using image detection to identify birds at a backyard feeder.

This project has multiple large video files, and unable to upload in Github. For viewing the output as well as the Google colab notebooks natively, please visit the project's Google Drive:

https://drive.google.com/drive/folders/1Az2sX6fY5jJ2O6aMfUaFZ2xWbRjn2rWM?usp=sharing

### Group 8: Stuart Fairchild | Kalen Foster | Ranveer Chand

## Proposal

Tier 2 Project, using a multi-model detection and classification pipeline.

Tier 2 justification: Our CV pipeline uses a multi-model approach, with a detection step feeding into a classification step.

#### Problem

Birds give invaluable data on the overall health of our planet's ecosystem. By observing their populations and species, we can gain insight of our world.

#### Solution

Current phone app based amateur birder detection is reliant on a person's observations. Our solution is a static camera continuously observing a birdfeeder for autonomous detection and classification of bird species, giving a more robust coverage of a single area.

#### Technical Approach

Using the PyTorch framework, YOLO11Large will act as an initial detection model for birds in the image, and its bounding box output will be piped into a custom specialist model that will classify the bird species.

#### Data Plan

Custom trained model dataset sources:​

 Kaggle Bird Detection 2000 Image by gpiosenka​: https://www.kaggle.com/datasets/gpiosenka/birdies/data

 2000 images, labels for bounding box, Intended to replace YOLO11Large as a custom initial detection model​
​

Custom classification model dataset

Collected species images from pixabay.com, approx. 500 images of each.

https://pixabay.com/images/search/american%20robin/

https://pixabay.com/images/search/blue%20jay/

https://pixabay.com/images/search/downy%20woodpecker/

https://pixabay.com/images/search/house%20finch/

https://pixabay.com/images/search/mourning%20dove/

https://pixabay.com/images/search/northern%20cardinal/

https://pixabay.com/photos/search/red%20bellied%20woodpecker/

#### Success Metrics

Detection accuracy: 90% of detections, 80% of classifications

Detection speed: 150ms initial detection for realtime video stream constraint

#### Milestones

Explore and Choose - Find a problem that is challenging and useful​

Blueprint - Realistic scope and ability - Submission: 7/13/26​

First Working Demo - Detection pipeline (YOLO11) working on static images and recorded video; initial species classifier integrated​ - Submission: 7/17/26​

Make it Yours​ - Streamline pipeline for live video - Submission: 7/24/26

Improve and Measure - Measure improvements in CV pipeline performance speed and accuracy - Submission: 7/26/26​

Build​ - Final working demo, README, and AI usage log finalized, demo video recorded, project analysis presented​ - Submission: 7/28/26

#### Top Risks

Species classifier accuracy may fall short of 90%, even if detection alone succeeds. Chaining two models means errors compound. ​

Getting initial detection under 150ms and still accurate (Not classification)​
Plan B: no realtime detection​

Custom dataset training – managing scale of individual species dataset​
Plan B: cut down dataset to just species known to visit the area

## Build

This section follows the Jupyter notebooks in the repo with a brief overview of the build process

#### Pt 1: Proof of concept

This notebook explores the performance of various models in detection and lays out the rough project direction. The outcome of this notebook determines that YOLO11Large is the best performing detection model for birds in the subset we sampled. This pipeline worked on a subset of sample images.

#### Pt 2: Segmentation

Going further with the experimentation in detection, this section explored the necessity of image segmentation using SAM2 in the detection and classification pipeline. It was determined that bounding boxes would be a good enough output of the detection model as a prepared input for the classification model.

#### Pt 3: Video

This section explored the process of detecting frames in a video file with both the large and nano versions of YOLO11. The models ran on CPU, giving us a very slow detection time of around 1.2s per frame in large and 150ms in nano. The nano performance wasn't good enough to warrant moving to the smaller model to save in processing time.

#### Pt 4: Refinement

This is an attempt at a custom detection model to replace the current best performing, YOLO11Large. 2 iterations of a custom detection model from the Kaggle 2000 bird dataset, the first trained using YOLO11nano as a base and the second using YOLO11Large. Both failed to outperform YOLO11Large and were not used in the final pipeline.

#### Pt 4.1 Convert premade classification model and

#### Pt 4.5: Use pretrained Kaggle detection model

The Kaggle dataset came packaged with a model in the Keras (.h5) format. The conversion process failed to migrate the model into the Pytorch framework and this was discarded.

#### Pt 5: Classification preparation and

#### Pt 6: Species Categorization

This notebook marks the refined classification training pipeline.

A subset of birds was selected from known species that visit the feeder. These birds were separated into folders and copied into the /dataset/raw location in the Google drive. The bird classes were prepared by:

1. Run the YOLO11Large model on the images to get an annotated image and bounding box coordinates

2. Define the data.yaml file for training the classification model based on the subfolder names

3. Update the corresponding image labels to the data structure of the data.yaml file

4. Create the train/val split

5. Train the model using YOLO11Large as the base

#### Pt 7: Video with Classification

This final notebook showcases the detection and classification pipeline working on multiple videos, with a second pipeline step of tracking the bird within the image, allowing for a better data export of the species in the image.
