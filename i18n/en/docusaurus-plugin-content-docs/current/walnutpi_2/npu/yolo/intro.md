---
sidebar_position: 1
---

# YOLO Introduction

YOLO (You Only Look Once) is an advanced real-time object detection algorithm primarily used for visual recognition. It was proposed by Joseph Redmon et al. in 2015. Its core idea is to treat the object detection task as a single regression problem, directly predicting the bounding box coordinates and category of objects through a single forward pass of the network, significantly improving detection speed and efficiency.

## Technical Principles

YOLO divides the input image into an S×S grid, where each grid cell is responsible for predicting objects that fall within that cell. Each grid cell outputs B bounding boxes along with their confidence scores, while also predicting C class probabilities. Bounding boxes contain location information (center coordinates, width, height) and a confidence score (reflecting the probability of an object existing in the box and the accuracy of box positioning). Through the Non-Maximum Suppression (NMS) algorithm, redundant boxes with high overlap are filtered out, retaining the optimal detection results.

![intro](./img/intro/intro1.png)

## Development History

YOLO has many versions, with different versions even maintained by different companies. Among them, the most popular are YOLOv5, YOLOv8, and YOLO11 maintained by Ultralytics.

![intro](./img/intro/intro2.png)

YOLO11 is the latest product in the Ultralytics YOLO real-time object detector series, redefining what is possible with state-of-the-art accuracy, speed, and efficiency. Building upon the impressive progress of previous YOLO versions, YOLO11 introduces significant improvements in architecture and training methods, making it a versatile choice for a wide range of computer vision tasks.

To meet different speed and accuracy requirements, each YOLO version is further divided into different variant versions. For example, YOLO11 includes YOLO11n, YOLO11s, YOLO11m, YOLO11l, and YOLO11x. The main differences lie in model size, performance, and accuracy. Below are their core differences:

- Model Scale and Parameter Count
    - YOLO11n (Nano): The smallest version with the fewest parameters (typically < 1M), small model size, suitable for edge device deployment.
    - YOLO11s (Small): Moderate parameter count (about 2-5M), balancing speed and accuracy, suitable for lightweight applications.
    - YOLO11m (Medium): Medium scale (about 10-20M), significantly improved accuracy, suitable for most general scenarios.
    - YOLO11l (Large): Larger parameter count (about 30-50M), higher accuracy but slower inference speed.
    - YOLO11x (Extra-Large): The largest version (parameters > 50M), providing the highest accuracy, suitable for scenarios with extremely high accuracy requirements.

- Application Scenarios
    - YOLO11n: Drones, mobile devices, real-time monitoring (low-compute environments).
    - YOLO11s/m: General object detection (e.g., security monitoring, autonomous driving assistance).
    - YOLO11l/x: High-precision scenarios (e.g., industrial inspection, medical image analysis).

The WalnutPi YOLO tutorial will use YOLO11n as the case study, covering five application routines: classification, detection, oriented detection, pose recognition, and image segmentation.

![intro](./img/intro/intro3.png)

The WalnutPi system comes with a built-in encapsulated YOLO11 Python library, making it easy to implement YOLO recognition functions using Python programming. The code materials are located in the development board resource package - example program directory.

![intro](./img/intro/intro4.png)
