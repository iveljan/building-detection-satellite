# Building Detection on Satellite Images
This project implements a deep learning approach for automated building detection on high-resolution satellite images using semantic segmentation.

## Project Overview
The main goal is to detect and delineate building footprints from satellite images using convolutional neural networks (CNNs), primarily U-Net. The project uses the SpaceNet V1 AOI1 (Paris) dataset, which includes RGB satellite imagery and manually annotated building masks.

 Main application areas: urban planning, disaster management, illegal construction monitoring, and geospatial mapping.

## Dataset
Source: SpaceNet V1 AOI1 (Paris) via AWS Public Datasets

~11,480 image tiles (200x200m, RGB 3-band, 50cm resolution)

~96,000 annotated building polygons (GeoJSON)

Only RGB data was used (not multispectral)

Dataset split: 80% training, 20% validation

## Preprocessing
+ Conversion of building polygons (GeoJSON) to binary masks

+ Image and mask resizing to 256×256

+ Data normalization and augmentation (rotation, scaling, flipping)

+ Filtering of empty or low-information tiles

## Model & Training
+ Architecture: U-Net with binary segmentation (buildings vs background)

+ Framework: PyTorch

+ Loss Function: Binary Cross Entropy (BCE)

+ Optimizer: Adam (lr=0.001)

+ Epochs: 10

+ Batch size: 4

Model training was performed on a local machine with GPU support.

## Performance
+ Final training loss: 0.0860

+ Validation IoU (Intersection over Union): 0.8333

+ Validation loss: 0.0406

The model generalizes well on unseen data and performs robustly in diverse urban conditions.

## Evaluation & Results
+ Tested on tiles not used during training

+ High-quality masks produced even for rotated or occluded buildings

+ Some minor issues with:

+ Small or shadowed buildings

+ Overlapping or touching structures

+ Label noise in original annotations



## Algorithm Flow

1. Load RGB satellite images and GeoJSON annotations
2. Convert vector polygons to binary raster masks
3. Resize images and normalize pixel values
4. Train U-Net model on (image, mask) pairs
5. Validate model on unseen tiles
6. Save and deploy model for future inference

## Future Improvements
+ Use ensemble models (e.g. U-Net + SegFormer)

+ Add attention layers to improve small object detection

+ Experiment with 8-band multispectral data

+ Apply post-processing (morphological filtering)
