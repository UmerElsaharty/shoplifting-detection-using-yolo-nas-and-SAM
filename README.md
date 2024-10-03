# Shoplifting Detection Project

This project aims to detect shoplifting activities in a retail environment by analyzing video frames. The approach leverages a combination of object detection (YOLO-NAS) and segmentation (Segment Anything Model - SAM) to focus on the actions of individuals within the scene, ensuring the detection is based on behavior and context rather than just identifying people.

## 1. Dataset Preparation

- **Video Frame Extraction**: 
  - Extracted frames from video files that contain shoplifting and non-shoplifting activities.
  - Used YOLOv5 to detect persons in the frames and filtered frames that only contained individuals. 
  - Frames were labeled based on two classes:
    - `0`: Shoplifting
    - `1`: Non-shoplifting

- **Oversampling the Minority Class**:
  - To balance the dataset, oversampled the minority class (`shoplifting`) by duplicating images to ensure an even distribution between both classes.

## 2. Model Training

- **YOLO-NAS Custom Model**:
  - Trained a custom YOLO-NAS model using the prepared dataset. The model was designed to classify between two classes:
    - Shoplifting
    - Non-shoplifting
  - The model was trained using bounding box annotations from the dataset. These annotations focused on individuals in the video frames and classified their behavior accordingly.

## 3. Segmentation Using SAM (Segment Anything Model)

- **Purpose**: 
  - After training the YOLO-NAS model, SAM was used to create segmentation masks over the detected individuals to ensure the focus remained on their actions and behavior rather than their identity.

- **Segmentation Steps**:
  1. The YOLO-NAS model detected the person and assigned the relevant class label (`shoplifting` or `non-shoplifting`).
  2. SAM was then applied to segment only the person within the bounding box provided by YOLO-NAS.
  3. The segmented mask helped focus on the action within the bounding box to better assess the behavior (shoplifting vs. non-shoplifting).

![Segmented Shoplifting Example](path_to_your_segmented_image.png)

*The image above shows an example of the model detecting shoplifting and using SAM to segment the person involved.*

## 4. Video Processing Pipeline

- **Real-Time Detection**:
  - The pipeline was set to process videos in near real-time. 
  - Frames were analyzed by the YOLO-NAS model, and every person detected was segmented using SAM.
  
- **Frame Skipping**:
  - For efficiency, the model only processed frames every 5 seconds, starting from the 3-second mark of each video.

## Model Performance

- The model was able to detect shoplifting behaviors with high accuracy after training, demonstrating that using YOLO-NAS for object detection and SAM for segmentation helped mitigate bias and generalize better to unseen individuals and scenarios.
