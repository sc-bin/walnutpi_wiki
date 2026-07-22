---
sidebar_position: 6
---
# YOLO11 Pose Estimation
This model identifies poses, outputting coordinates of keypoints such as nose, eyes, ears, shoulders, hands, and legs. These coordinates can be used to determine postures. You can also train it to recognize poses of other animals.

![model_change](./img/pose/pose0.png)


## Prepare Model File

The program package we provide includes a file named `yolo11n-pose.nb`, which is the model file for running YOLO11 pose estimation on the WalnutPi 2B (T527) NPU.

![result](./img/pose/pose1.png)

If you want to try converting the model yourself, refer to: [Model Conversion Tutorial](./model_convert.md)

## Install OpenCV

This tutorial requires the OpenCV library. For installation instructions, refer to: [OpenCV Installation](../../opencv/install.md)

## Run Model with Python

WalnutPi 2B v1.3.0 and above provides a packaged YOLO11 Python library.

### 1. Instantiate yolo11 Class
Instantiate the `YOLO11_POSE` class by passing the model file path:
```python
from walnutpi import YOLO11
yolo = YOLO11.YOLO11_POSE("model/yolo11n-pose.nb")
```
### 2. Run Model - Blocking Mode
Use the `run` method to run the model and get detection results. It takes 3 parameters:
- Image data, read using OpenCV's image reading method
- Confidence threshold, only detection boxes above this confidence will be returned
- Detection box overlap threshold, the model often hits multiple boxes around an object. If the area overlap between boxes exceeds this value, only the box with the highest confidence is kept, and other overlapping boxes are removed

```python
# Read image
import cv2
img = cv2.imread("image/bus.jpg")

# Detect
boxes = yolo.run(img, 0.5, 0.5)
```

### 3. Run Model - Non-blocking Mode
Use the `run_async` method, which creates a thread to run the model and returns immediately. It takes 3 parameters:
- Image data, read using OpenCV's image reading method
- Confidence threshold, only detection boxes above this confidence will be returned
- Detection box overlap threshold

Non-blocking mode works with the `is_running` property, which has a value of `true` or `false`, indicating whether a `run_async` model thread is running in the background. If a thread is already running, calling `run_async` again won't start a new thread. You can also use this property to check if the model thread has finished and results are ready.

Use the `get_result()` method to return the background recognition result, which is the same as what the blocking `run` method returns:

```python
import cv2
img = cv2.imread("image/bus.jpg")

yolo.run_async(img, 0.5, 0.5)
while yolo.is_running:
    time.sleep(0.1)
boxes = yolo.get_result()
```

### 4. Detection Results
Both the `run` method and `get_result` method return a list. If nothing is detected in the image, an empty list is returned. Each value in the list represents a detected box, and each box object contains the following properties:

| Property    | Description                                          |
| ----------- | --------------------------------------------- |
| x           | x-coordinate of the detection box center                           |
| y           | y-coordinate of the detection box center                           |
| w           | Width of the detection box                                  |
| h           | Height of the detection box                                  |
| reliability | Confidence of the detection box, e.g., 0.78                 |
| label       | Label of the detection box; generally pose models only recognize 1 type |
| keypoints   | Information about each keypoint                              |

The `keypoints` property is a list, where each value is a keypoint object. For example, using the official YOLO human pose model, there are 17 keypoints in the following order:

| Keypoint Index | Keypoint Name |
| ---------- | ---------- |
| 0          | Nose       |
| 1          | Left Eye       |
| 2          | Right Eye       |
| 3          | Left Ear       |
| 4          | Right Ear       |
| 5          | Left Shoulder       |
| 6          | Right Shoulder       |
| 7          | Left Elbow     |
| 8          | Right Elbow     |
| 9          | Left Wrist     |
| 10         | Right Wrist     |
| 11         | Left Hip     |
| 12         | Right Hip     |
| 13         | Left Knee     |
| 14         | Right Knee       |
| 15         | Left Ankle     |
| 16         | Right Ankle     |

    
Each keypoint object contains the following properties:
| Property   | Description                          |
| ---------- | ----------------------------- |
| xy         | Keypoint xy coordinates, e.g., (192,320) |
| visibility | Probability that the point is visible                |


The following code can be used to output all detected box information:
```python
print(f"boxes: {boxes.__len__()}")
for box in boxes:
    print(
        "{:f} ({:4d},{:4d}) w{:4d} h{:4d} lbael:{:d}".format(
            box.reliability,
            box.x,
            box.y,
            box.w,
            box.h,
            box.label,
        )
    )
```

## Example Programs

### Image-Based

Read an image for detection and draw the detected keypoints.

![results](./img/pose/pose0.png)

```python
'''
Experiment Name: YOLO11 Pose Estimation
Experiment Platform: WalnutPi 2B
Description: Image-based
'''

from walnutpi import YOLO11
import cv2

# [Optional] Allow Thonny remote execution
import os
os.environ["DISPLAY"] = ":0.0"

label_names = ["person"]

model_path = "model/yolo11n-pose.nb"
picture_path = "image/person.jpg"
output_path = ".result.jpg"

# Detect image
yolo = YOLO11.YOLO11_POSE(model_path)
boxes = yolo.run(picture_path, 0.5, 0.5)

# Draw boxes on image
img = cv2.imread(picture_path)
for box in boxes:
    left_x = int(box.x - box.w / 2)
    left_y = int(box.y - box.h / 2)
    right_x = int(box.x + box.w / 2)
    right_y = int(box.y + box.h / 2)
    label = str(label_names[box.label]) + " " + str('%.2f'%(box.reliability))
    (label_width, label_height), bottom = cv2.getTextSize(
        label,
        cv2.FONT_HERSHEY_SIMPLEX,
        0.5,
        1,
    )
    cv2.rectangle(
        img,
        (left_x, left_y),
        (right_x, right_y),
        (255, 255, 0),
        2,
    )
    cv2.rectangle(
        img,
        (left_x, left_y - label_height * 2),
        (left_x + label_width, left_y),
        (255, 255, 255),
        -1,
    )
    cv2.putText(
        img,
        label,
        (left_x, left_y - label_height),
        cv2.FONT_HERSHEY_SIMPLEX,
        0.5,
        (0, 0, 0),
        1,
    )
    
    # 0 Nose 1 Left Eye 2 Right Eye 3 Left Ear 4 Right Ear 5 Left Shoulder 6 Right Shoulder
    # 7 Left Elbow 8 Right Elbow 9 Left Wrist 10 Right Wrist 11 Left Hip 12 Right Hip
    # 13 Left Knee 14 Right Knee 15 Left Ankle 16 Right Ankle
    for i in box.keypoints:  # Draw all keypoints with high enough visibility
        if i.visibility > 0.5:
            cv2.circle(img, i.xy, 5, (0, 0, 200), -1)
            
    # Head connections
    cv2.line(img, box.keypoints[3].xy, box.keypoints[1].xy, (0, 255, 255), 2)
    cv2.line(img, box.keypoints[1].xy, box.keypoints[0].xy, (0, 255, 255), 2)
    cv2.line(img, box.keypoints[0].xy, box.keypoints[2].xy, (0, 255, 255), 2)
    cv2.line(img, box.keypoints[2].xy, box.keypoints[4].xy, (0, 255, 255), 2)
    cv2.line(img, box.keypoints[3].xy, box.keypoints[5].xy, (0, 255, 255), 2)
    cv2.line(img, box.keypoints[4].xy, box.keypoints[6].xy, (0, 255, 255), 2)
    
    # Left and right arm connections
    cv2.line(img, box.keypoints[7].xy, box.keypoints[5].xy, (255, 0, 0), 2)
    cv2.line(img, box.keypoints[7].xy, box.keypoints[9].xy, (255, 0, 0), 2)
    cv2.line(img, box.keypoints[8].xy, box.keypoints[6].xy, (255, 0, 0), 2)
    cv2.line(img, box.keypoints[8].xy, box.keypoints[10].xy, (255, 0, 0), 2)

    # Torso connections
    cv2.line(img, box.keypoints[5].xy, box.keypoints[6].xy, (100, 255, 100), 2)
    cv2.line(img, box.keypoints[11].xy, box.keypoints[5].xy, (100, 255, 100), 2)
    cv2.line(img, box.keypoints[12].xy, box.keypoints[6].xy, (100, 255, 100), 2)
    cv2.line(img, box.keypoints[12].xy, box.keypoints[11].xy, (100, 255, 100), 2)

    # Left and right leg connections
    cv2.line(img, box.keypoints[13].xy, box.keypoints[11].xy, (255, 255, 0), 2)
    cv2.line(img, box.keypoints[13].xy, box.keypoints[15].xy, (255, 255, 0), 2)
    cv2.line(img, box.keypoints[14].xy, box.keypoints[12].xy, (255, 255, 0), 2)
    cv2.line(img, box.keypoints[14].xy, box.keypoints[16].xy, (255, 255, 0), 2)

# Save image
cv2.imwrite(output_path, img)

# Display image in window
cv2.imshow('result',img)

cv2.waitKey()
cv2.destroyAllWindows()

```

### Camera-Based

You can first learn about the [USB Camera Usage Tutorial](../../opencv/usb_cam.md) in OpenCV.

![results](./img/pose/pose2.png)

```python
'''
Experiment Name: YOLO11 Pose Estimation
Experiment Platform: WalnutPi 2B
Description: Camera-based
'''

from walnutpi import YOLO11
import cv2

# [Optional] Allow Thonny remote execution
import os
os.environ["DISPLAY"] = ":0.0"

label_names = ["person"]

model_path = "model/yolo11n-pose.nb"
yolo = YOLO11.YOLO11_POSE(model_path)

# Open camera and loop to get frames and display on screen
cap = cv2.VideoCapture(0)
if not cap.isOpened():
    print("Cannot open camera")
    exit()

boxes = []
while True:
    ret, img = cap.read()
    if not ret:
        print("Can't receive frame (stream end?). Exiting ...")
        break
    if not yolo.is_running:
        yolo.run_async(img, 0.3)
    boxes = yolo.get_result()

    for box in boxes:
        label = str(label_names[box.label]) + " " + str('%.2f'%box.reliability)
        left_x = int(box.x - box.w / 2)
        left_y = int(box.y - box.h / 2)
        right_x = int(box.x + box.w / 2)
        right_y = int(box.y + box.h / 2)
        (label_width, label_height), bottom = cv2.getTextSize(
            label, cv2.FONT_HERSHEY_SIMPLEX, 0.5, 1,
        )
        (label_width, label_height), bottom = cv2.getTextSize(
            label, cv2.FONT_HERSHEY_SIMPLEX, 0.5, 1,
        )
        cv2.rectangle(img, (left_x, left_y), (right_x, right_y), (255, 255, 0), 2)
        cv2.rectangle(img, (left_x, left_y - label_height * 2), (left_x + label_width, left_y), (255, 255, 255), -1)
        cv2.putText(img, label, (left_x, left_y - label_height), cv2.FONT_HERSHEY_SIMPLEX, 0.5, (0, 0, 0), 1)
        
        for i in box.keypoints:
            if i.visibility > 0.5:
                cv2.circle(img, i.xy, 5, (0, 0, 200), -1)

        # Head connections
        cv2.line(img, box.keypoints[3].xy, box.keypoints[1].xy, (0, 255, 255), 2)
        cv2.line(img, box.keypoints[1].xy, box.keypoints[0].xy, (0, 255, 255), 2)
        cv2.line(img, box.keypoints[0].xy, box.keypoints[2].xy, (0, 255, 255), 2)
        cv2.line(img, box.keypoints[2].xy, box.keypoints[4].xy, (0, 255, 255), 2)
        cv2.line(img, box.keypoints[3].xy, box.keypoints[5].xy, (0, 255, 255), 2)
        cv2.line(img, box.keypoints[4].xy, box.keypoints[6].xy, (0, 255, 255), 2)
        
        # Left and right arm connections
        cv2.line(img, box.keypoints[7].xy, box.keypoints[5].xy, (255, 0, 0), 2)
        cv2.line(img, box.keypoints[7].xy, box.keypoints[9].xy, (255, 0, 0), 2)
        cv2.line(img, box.keypoints[8].xy, box.keypoints[6].xy, (255, 0, 0), 2)
        cv2.line(img, box.keypoints[8].xy, box.keypoints[10].xy, (255, 0, 0), 2)

        # Torso connections
        cv2.line(img, box.keypoints[5].xy, box.keypoints[6].xy, (100, 255, 100), 2)
        cv2.line(img, box.keypoints[11].xy, box.keypoints[5].xy, (100, 255, 100), 2)
        cv2.line(img, box.keypoints[12].xy, box.keypoints[6].xy, (100, 255, 100), 2)
        cv2.line(img, box.keypoints[12].xy, box.keypoints[11].xy, (100, 255, 100), 2)

        # Left and right leg connections
        cv2.line(img, box.keypoints[13].xy, box.keypoints[11].xy, (255, 255, 0), 2)
        cv2.line(img, box.keypoints[13].xy, box.keypoints[15].xy, (255, 255, 0), 2)
        cv2.line(img, box.keypoints[14].xy, box.keypoints[12].xy, (255, 255, 0), 2)
        cv2.line(img, box.keypoints[14].xy, box.keypoints[16].xy, (255, 255, 0), 2)

    cv2.imshow("result", img)
    key = cv2.waitKey(1)
    if key == 32:
        break
    
cap.release()
cv2.destroyAllWindows()

```
