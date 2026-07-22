---
sidebar_position: 1
---

# PushButton

## Introduction

The PushButton widget is very common; it's called a button widget with press and release effects.

![PushButton1](./img/PushButton/PushButton1.png)

Editing the button is simple. Double-click to modify the button text content, and drag the edges to resize the button. Font size, adding icons, and other settings can all be configured in the right-side properties panel.

![PushButton2](./img/PushButton/PushButton2.png)

The Python code generated from this window is as follows:
```python

# -*- coding: utf-8 -*-

from PyQt5 import QtCore, QtGui, QtWidgets


class Ui_MainWindow(object):
    def setupUi(self, MainWindow):
        MainWindow.setObjectName("MainWindow")
        MainWindow.resize(480, 320)
        self.centralwidget = QtWidgets.QWidget(MainWindow)
        self.centralwidget.setObjectName("centralwidget")
        self.pushButton = QtWidgets.QPushButton(self.centralwidget)
        self.pushButton.setGeometry(QtCore.QRect(180, 120, 111, 41))
        font = QtGui.QFont()
        font.setFamily("Agency FB")
        font.setPointSize(12)
        self.pushButton.setFont(font)
        self.pushButton.setObjectName("pushButton")
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
        self.pushButton.setText(_translate("MainWindow", "Button"))

```

The code related to the button is as follows:

```python
# -*- coding: utf-8 -*-

from PyQt5 import QtCore, QtGui, QtWidgets


class Ui_MainWindow(object):
    def setupUi(self, MainWindow):
        ...
        self.pushButton = QtWidgets.QPushButton(self.centralwidget) # Create a button widget in the window
        self.pushButton.setGeometry(QtCore.QRect(180, 120, 111, 41)) # Button x, y, width, height

        # Set button font and color
        font = QtGui.QFont()
        font.setFamily("Agency FB")
        font.setPointSize(12)
        self.pushButton.setFont(font)
        
        self.pushButton.setObjectName("pushButton") # Set button object name, not display name


    def retranslateUi(self, MainWindow):
        ...
        self.pushButton.setText(_translate("MainWindow", "Button")) # Change display name to "Button"

```
## QPushButton Object

|  Common Methods |  Description |
|  :---:  | --- | 
| setText()  |  Set the text displayed on the button  | 
| Text()  |  Get the text content displayed on the button  | 
| setEnabled()  |  When parameter is False, the button is disabled  | 

<br></br>

|  Common Signals |  Description |
|  :---:  | --- | 
| clicked  |  Triggered on click  | 


## Example

**Example: Program the button to execute a custom function when clicked.**

The most commonly used signal for buttons is click, i.e., clicked. Use pushButton.clicked.connect() to specify the function to execute when the button is clicked.

Referring to the Signals and Slots section, add the following after self.retranslateUi(MainWindow):

```python

self.pushButton.clicked.connect(self.fun) # Execute fun function when button is pressed

```

Then add the function to be executed inside the Ui_MainWindow class. Here, it prints information to the terminal:

```python

# Function executed when button is pressed
def fun(self):
    print('Button is Press!')

```

The complete code is as follows:

```python

# -*- coding: utf-8 -*-

from PyQt5 import QtCore, QtGui, QtWidgets


class Ui_MainWindow(object):
    def setupUi(self, MainWindow):
        MainWindow.setObjectName("MainWindow")
        MainWindow.resize(480, 320)
        self.centralwidget = QtWidgets.QWidget(MainWindow)
        self.centralwidget.setObjectName("centralwidget")
        self.pushButton = QtWidgets.QPushButton(self.centralwidget)
        self.pushButton.setGeometry(QtCore.QRect(180, 120, 111, 41))
        font = QtGui.QFont()
        font.setFamily("Agency FB")
        font.setPointSize(12)
        self.pushButton.setFont(font)
        self.pushButton.setObjectName("pushButton")
        MainWindow.setCentralWidget(self.centralwidget)
        self.menubar = QtWidgets.QMenuBar(MainWindow)
        self.menubar.setGeometry(QtCore.QRect(0, 0, 480, 22))
        self.menubar.setObjectName("menubar")
        MainWindow.setMenuBar(self.menubar)
        self.statusbar = QtWidgets.QStatusBar(MainWindow)
        self.statusbar.setObjectName("statusbar")
        MainWindow.setStatusBar(self.statusbar)

        self.retranslateUi(MainWindow)
        self.pushButton.clicked.connect(self.fun) # Button signal and slot definition
        QtCore.QMetaObject.connectSlotsByName(MainWindow)

    def retranslateUi(self, MainWindow):
        _translate = QtCore.QCoreApplication.translate
        MainWindow.setWindowTitle(_translate("MainWindow", "MainWindow"))
        self.pushButton.setText(_translate("MainWindow", "Button"))
    
    # Function executed when button is pressed
    def fun(self):
        print('Button is Press!')

#################
#   Main Program Code   #
#################
import sys

#【Optional Code】Allow Thonny remote execution
import os
os.environ["DISPLAY"] = ":0.0"

#【Optional Code】Fix display issues on monitors with 2K+ resolution
QtCore.QCoreApplication.setAttribute(QtCore.Qt.AA_EnableHighDpiScaling)

# Program entry point: build the window and display it
app = QtWidgets.QApplication(sys.argv)
MainWindow = QtWidgets.QMainWindow() # Build window object
ui = Ui_MainWindow() # Build PyQt5-designed window object
ui.setupUi(MainWindow) # Initialize window
MainWindow.show() # Display window

#【Recommended Code】Allow terminal to interrupt window with ctrl+c for easier debugging
import signal
signal.signal(signal.SIGINT, signal.SIG_DFL)
timer = QtCore.QTimer()
timer.start(100)  # You may change this if you wish.
timer.timeout.connect(lambda: None)  # Let the interpreter run each 100 ms

sys.exit(app.exec_()) # Exit process when program closes

```

Run the code. Each time you press the button, you will see 'Button is Press!' printed in the terminal.

![PushButton3](./img/PushButton/PushButton3.png)

You can also combine this with the earlier Python embedded programming to implement functions like controlling an LED with a button.
