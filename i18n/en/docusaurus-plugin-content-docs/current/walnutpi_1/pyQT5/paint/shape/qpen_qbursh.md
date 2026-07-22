---
sidebar_position: 2
---

# Pen and Brush Configuration

In the previous section, we learned the basic methods of drawing shapes. In this section, we'll learn about pen and brush configuration.

## Pen Object (QPen)

The pen is primarily used to configure the thickness, color, style, etc., of shape outlines.

|  Common Pen Methods |  Description |
|  :---:  | --- | 
| setColor()  |  Set the pen color  | 
| setWidth()  |  Set the pen width  | 
| setStyle()  |  Set the style:<br></br>● Qt.SolidLine: Regular solid line  | 

## Brush Object (QBrush)

The brush is primarily used to fill geometric shapes with color.

|  Common Brush Methods |  Description |
|  :---:  | --- | 
| setColor()  |  Set the brush color  |
| setStyle()  |  Set the style:<br></br>● Qt.SolidPattern: Solid fill  |  

## Example

**Example: Change the line width of all shapes from the previous section to 5, fill the rectangle with red, and fill the circle with blue.**

Here's the implementation code:

```python
# -*- coding: utf-8 -*-

# pyQT5 For WalnutPi

from PyQt5 import QtCore, QtGui, QtWidgets

from PyQt5.QtCore import Qt
from PyQt5.QtGui import QPainter,QPen,QBrush
from PyQt5.QtWidgets import QWidget

class Window(QWidget):
    
    def __init__(self):
        super().__init__() # Execute the parent QWidget's __init__ as well
        self.setWindowTitle("WalnutPi Paint") # Set window title
        self.resize(480,320) # Set window size
        
        # Window background color setting
        self.setObjectName("Paint_Window")
        self.setStyleSheet("#Paint_Window{background-color: black}") # Black

    def paintEvent(self,event):
        
        painter=QPainter(self) # Create drawing object
        
        # Pen configuration:
        pen = QPen()
        pen.setColor(Qt.green) # Green
        pen.setWidth(5) # Width 5
        painter.setPen(pen)
        
        # Brush configuration
        brush = QBrush()
        brush.setColor(Qt.red) # Red
        brush.setStyle(Qt.SolidPattern) # Fill
        painter.setBrush(brush) 
        
        painter.drawPoint(10,10) # Draw point
        
        painter.drawLine(20, 10, 80, 10) # Draw line
        
        painter.drawRect(100, 10, 80, 40) # Draw rectangle
        
        # Reconfigure brush, blue
        brush.setColor(Qt.blue)
        painter.setBrush(brush) 
        painter.drawEllipse(200, 10, 50, 50) # Draw circle
        

#################
#   Main Code    #
#################
import sys

# [Optional] Allow Thonny remote execution
import os
os.environ["DISPLAY"] = ":0.0"

# [Optional] Fix display issues on 2K+ resolution monitors
QtCore.QCoreApplication.setAttribute(QtCore.Qt.AA_EnableHighDpiScaling)

# Main program entry — build and display the window
app = QtWidgets.QApplication(sys.argv)
window = Window() # Create window object
window.show() # Show window
#window.showFullScreen() # Full-screen display

# [Recommended] Allow Ctrl+C to interrupt the window from terminal for easier debugging
import signal
signal.signal(signal.SIGINT, signal.SIG_DFL)
timer = QtCore.QTimer()
timer.start(100)  # You may change this if you wish.
timer.timeout.connect(lambda: None)  # Let the interpreter run each 100 ms

sys.exit(app.exec_()) # Exit the process when the window is closed

```

The main difference from the previous code is the addition of pen and brush configuration:

```python

    def paintEvent(self,event):

        ...

        # Pen configuration:
        pen = QPen()
        pen.setColor(Qt.green) # Green
        pen.setWidth(5) # Width 5
        painter.setPen(pen)
        
        # Brush configuration
        brush = QBrush()
        brush.setColor(Qt.red) # Red
        brush.setStyle(Qt.SolidPattern) # Fill
        painter.setBrush(brush) 
```

Additionally, the brush was initially set to red, so before drawing the circle after the rectangle, it needs to be reconfigured:

```python
    ...
        # Reconfigure brush, blue
        brush.setColor(Qt.blue)
        painter.setBrush(brush) 
        painter.drawEllipse(200, 10, 50, 50) # Draw circle
```

The result is as follows:

![pen_brush1](./img/qpen_qbrush/pen_brush1.png)
