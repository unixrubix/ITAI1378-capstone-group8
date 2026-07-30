# ITAI1378-capstone-group8

## Backyard Bird Identification using Computer Vision

Computer Vision course midterm. Using image detection to identify birds at a backyard feeder.

### Group 8: Stuart Fairchild | Kalen Foster | Ranveer Chand

Tier 2 Project, using a multi-model detection and classification pipeline

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

 LaSBiRD dataset through IEEE Dataport: https://ieee-dataport.org/documents/lasbird-large-scale-bird-recognition-dataset​

 5M images, labelled by species, Intended to train the species classifier model

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
