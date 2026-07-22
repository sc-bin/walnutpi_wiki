---
sidebar_position: 2
---

# ToolButton

## Introduction

The main difference between a ToolButton and a PushButton is that a ToolButton can include a directional arrow.

![ToolButton1](./img/ToolButton/ToolButton1.png)
<br></br>
Editing a ToolButton is simple — double-click to modify the button text, and drag the edges to resize it. All other properties can be configured in the property panel on the right.

![ToolButton2](./img/ToolButton/ToolButton2.png)

The generated Python code for this window is as follows:

```python

# -*- coding: utf-8 -*-

from PyQt5 import QtCore, QtGui, QtWidgets


class Ui_MainWindow(object):
    def setupUi(self, MainWindow):
        MainWindow.setObjectName("MainWindow")
        MainWindow.resize(480, 320)
        self.centralwidget = QtWidgets.QWidget(MainWindow)
        self.centralwidget.setObjectName("centralwidget")
        self.toolButton = QtWidgets.QToolButton(self.centralwidget)
        self.toolButton.setGeometry(QtCore.QRect(180, 130, 50, 50))
        self.toolButton.setArrowType(QtCore.Qt.LeftArrow)
        self.toolButton.setObjectName("toolButton")
        self.toolButton_2 = QtWidgets.QToolButton(self.centralwidget)
        self.toolButton_2.setGeometry(QtCore.QRect(290, 130, 50, 50))
        self.toolButton_2.setArrowType(QtCore.Qt.RightArrow)
        self.toolButton_2.setObjectName("toolButton_2")
        MainWindow.setCentralWidget(self.centralwidget)
        self.menubar = QtWidgets.QMenuBar(MainWindow)
        self.menubar.setGeometry(QtCore.QRect(0, 0, 480, 22))
        self.menubar.setObjectName("menubar")
        MainWindow.setMenuBar(self.menubar)
        self.statusbar = QtWidgets.QStatusBar(MainWindow)
        self.statusbar.setObjectName("statusbar")
        MainWindow.setStatusBar(self.statusbar)

        self.retranslateUi(MainWindow)
        QtCore.QMetaObject.connectSlotsByName(MainWindow)

    def retranslateUi(self, MainWindow):
        _translate = QtCore.QCoreApplication.translate
        MainWindow.setWindowTitle(_translate("MainWindow", "MainWindow"))
        self.toolButton.setText(_translate("MainWindow", "..."))
        self.toolButton_2.setText(_translate("MainWindow", "..."))

```

The code related to the ToolButton is as follows:

```python
# -*- coding: utf-8 -*-

from PyQt5 import QtCore, QtGui, QtWidgets

class Ui_MainWindow(object):
    def setupUi(self, MainWindow):

        ...

        # ToolButton (left arrow)
        self.toolButton = QtWidgets.QToolButton(self.centralwidget) 
        self.toolButton.setGeometry(QtCore.QRect(180, 130, 50, 50))
        self.toolButton.setArrowType(QtCore.Qt.LeftArrow) # Left arrow
        self.toolButton.setObjectName("toolButton")

        # ToolButton (right arrow)
        self.toolButton_2 = QtWidgets.QToolButton(self.centralwidget)
        self.toolButton_2.setGeometry(QtCore.QRect(290, 130, 50, 50))
        self.toolButton_2.setArrowType(QtCore.Qt.RightArrow) # Right arrow
        self.toolButton_2.setObjectName("toolButton_2")

        ...

    def retranslateUi(self, MainWindow):

        ...

        self.toolButton.setText(_translate("MainWindow", "..."))
        self.toolButton_2.setText(_translate("MainWindow", "..."))

        ...

```

## QToolButton Object

|  Common Methods |  Description |
|  :---:  | --- | 
| setText()  |  Set the text displayed on the button  | 
| setArrowType()  |  Set arrow direction. Parameters:<br></br> ● QtCore.Qt.NoArrow : None<br></br> ● QtCore.Qt.UpArrow : Up <br></br> ● QtCore.Qt.DownArrow : Down <br></br> ● QtCore.Qt.LeftArrow : Left<br></br> ● QtCore.Qt.RightArrow : Right| 

<br></br>

|  Common Signals |  Description |
|  :---:  | --- | 
| clicked  |  Triggered on click  | 


## Example

**Example: Programmatically make clicking two buttons execute different functions.**

The most commonly used button signal is click, i.e., `clicked`. Use `pushButton.clicked.connect()` to specify the function to execute when the button is clicked.

Referring to the signals and slots section, add the following after `self.retranslateUi(MainWindow)`:

```python

self.toolButton.clicked.connect(self.fun1) # Execute fun1 when pressed
self.toolButton_2.clicked.connect(self.fun2) # Execute fun2 when pressed

```

Then add the functions to execute inside the `Ui_MainWindow` class — here we'll have them print messages to the terminal:

```python

# Function executed when ToolButton 1 is pressed
def fun1(self):
    print('Left')
        
# Function executed when ToolButton 2 is pressed
def fun2(self):
    print('Right')

```

Here's the complete code:

```python
# -*- coding: utf-8 -*-

from PyQt5 import QtCore, QtGui, QtWidgets


class Ui_MainWindow(object):
    def setupUi(self, MainWindow):
        MainWindow.setObjectName("MainWindow")
        MainWindow.resize(480, 320)
        self.centralwidget = QtWidgets.QWidget(MainWindow)
        self.centralwidget.setObjectName("centralwidget")
        self.toolButton = QtWidgets.QToolButton(self.centralwidget)
        self.toolButton.setGeometry(QtCore.QRect(180, 130, 50, 50))
        self.toolButton.setArrowType(QtCore.Qt.LeftArrow)
        self.toolButton.setObjectName("toolButton")
        self.toolButton_2 = QtWidgets.QToolButton(self.centralwidget)
        self.toolButton_2.setGeometry(QtCore.QRect(290, 130, 50, 50))
        self.toolButton_2.setArrowType(QtCore.Qt.RightArrow)
        self.toolButton_2.setObjectName("toolButton_2")
        MainWindow.setCentralWidget(self.centralwidget)
        self.menubar = QtWidgets.QMenuBar(MainWindow)
        self.menubar.setGeometry(QtCore.QRect(0, 0, 480, 22))
        self.menubar.setObjectName("menubar")
        MainWindow.setMenuBar(self.menubar)
        self.statusbar = QtWidgets.QStatusBar(MainWindow)
        self.statusbar.setObjectName("statusbar")
        MainWindow.setStatusBar(self.statusbar)

        self.retranslateUi(MainWindow)
        self.toolButton.clicked.connect(self.fun1) # Execute fun1 when pressed
        self.toolButton_2.clicked.connect(self.fun2) # Execute fun2 when pressed
        QtCore.QMetaObject.connectSlotsByName(MainWindow)

    def retranslateUi(self, MainWindow):
        _translate = QtCore.QCoreApplication.translate
        MainWindow.setWindowTitle(_translate("MainWindow", "MainWindow"))
        self.toolButton.setText(_translate("MainWindow", "..."))
        self.toolButton_2.setText(_translate("MainWindow", "..."))
        
    # Function executed when ToolButton 1 is pressed
    def fun1(self):
        print('Left')
        
    # Function executed when ToolButton 2 is pressed
    def fun2(self):
        print('Right')

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
MainWindow = QtWidgets.QMainWindow() # Create window object
ui = Ui_MainWindow() # Create PyQt5-designed window object
ui.setupUi(MainWindow) # Initialize window
MainWindow.show() # Show window

# [Recommended] Allow Ctrl+C to interrupt the window from terminal for easier debugging
import signal
signal.signal(signal.SIGINT, signal.SIG_DFL)
timer = QtCore.QTimer()
timer.start(100)  # You may change this if you wish.
timer.timeout.connect(lambda: None)  # Let the interpreter run each 100 ms

sys.exit(app.exec_()) # Exit the process when the window is closed

```

Run the code. Pressing the left arrow button prints "Left", and pressing the right arrow button prints "Right".

![ToolButton3](./img/ToolButton/ToolButton3.png)
