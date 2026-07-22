---
sidebar_position: 6
---

# License Plate Detection

## Introduction

This section learns to use OpenCV to detect the position of license plates in an image (detection only, not recognition).

## Experiment Objective

Detect the position of license plates in an image and draw rectangular boxes for display.

## Experiment Explanation

Using the cascade classifier method introduced earlier, this section uses the license plate detection cascade classifier `haarcascade_russian_plate_number.xml`. The code writing flow is as follows:

```mermaid
graph TD
    Read-image-->Load-cascade-classifier-->Classifier-recognizes-specified-target-->Draw-box-->Display-image;
```

<br></br>

## Reference Code

Reference code is as follows:

```python
import cv2

img = cv2.imread('car.png') # Read the image

# Load the license plate detection cascade classifier; note that the path must not contain Chinese characters
plateFaceCascade = cv2.CascadeClassifier('data/haarcascade_russian_plate_number.xml')

# Detect all license plates
plates = plateFaceCascade.detectMultiScale(img, 1.15)

# Iterate through all results
for (x, y, w, h) in plates:
    cv2.rectangle(img, (x, y), (x+w, y+h), (0, 0, 255), 3) # Draw a box
    
cv2.imshow('result', img) # Display the image

cv2.waitKey() # Wait for any key press
cv2.destroyAllWindows() # Close the window    

```

## Experiment Results

Run the above code on the WalnutPi, and the experimental results are as follows:

![plate_detection](./img/plate_detection/plate_detection1.png) 

## Using USB Camera for Recognition

By combining the USB camera usage method introduced earlier, you can perform real-time recognition via a USB camera. Reference code is as follows:

### Reference Code

```python
import cv2, time

# Load the license plate detection cascade classifier; note that the path must not contain Chinese characters
plateFaceCascade = cv2.CascadeClassifier('data/haarcascade_russian_plate_number.xml')

cam = cv2.VideoCapture(1) # Open the USB camera

# Lowering the resolution can improve recognition speed; can be set to 480x320 or 320x240
cam.set(3,480) # Set capture image width to 480
cam.set(4,320) # Set capture image height to 320
 
# Calculate FPS (frames per second parameter)
start = 0
end = 0

while True:
    
    start = time.time() # Record start time
    
    retval, img = cam.read() # Read images from the camera in real-time

    # Detect all license plates
    plates = plateFaceCascade.detectMultiScale(img, 1.15)

    # Iterate through all results
    for (x, y, w, h) in plates:
        cv2.rectangle(img, (x, y), (x+w, y+h), (0, 0, 255), 3) # Draw a box
            
    end = time.time() # Record end time
    
    # Calculate FPS (frames per second), result rounded to integer
    fps = round(1/(end-start))
    print('FPS: ', fps)
    
    # Write text on the image
    cv2.putText(img, "FPS: "+ str(fps), (20, 70), cv2.FONT_HERSHEY_SIMPLEX, 2, (0, 255, 0), 5)
    
    cv2.imshow('result', img) # Display the image
    
    key = cv2.waitKey(1) # Window image refresh time is 1 millisecond to prevent blocking    
    if key == 32: # If the spacebar is pressed, break and exit
        break
    
cam.release() # Close the camera
cv2.destroyAllWindows() # Destroy the window displaying the camera video

```

### Experiment Results

![plate_detection](./img/plate_detection/plate_detection2.png) 
