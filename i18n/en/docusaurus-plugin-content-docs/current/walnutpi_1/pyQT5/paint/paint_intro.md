---
sidebar_position: 1
---

# Introduction to Drawing

We've seen that PyQt5 already has very powerful widget features. However, widget interfaces are relatively fixed. If we want to DIY and draw custom graphics such as points, lines, rectangles, circles, characters, images, etc., we can use the QPainter class drawing functions.

## QPainter Object

All drawing and setting functions/methods are in QPainter, located under PyQt5.QtGui.

|  Drawing Methods |  Description |
|  :---:  | --- | 
| drawPoint()  |  Draw a point  | 
| drawPoints()  |  Draw multiple points  | 
| drawLine()  |  Draw a straight line  | 
| drawLines()  |  Draw multiple straight lines  | 
| drawRect()  |  Draw a rectangle  | 
| drawRects()  |  Draw multiple rectangles  | 
| drawRoundedRect()  |  Draw a rounded rectangle  | 
| drawEllipse()  |  Draw an ellipse (circle)  |
| drawArc()  |  Draw an arc  | 
| drawChord()  |  Draw a chord  |
| drawImage()  |  Draw an image  | 
| drawPath()  |  Draw a path  | 
| drawLines()  |  Draw multiple straight lines  | 
| drawPicture()  |  Draw a Picture image  |
| drawPie()  |  Draw a pie sector  |
| drawPixmap()  |  Extract Pixmap from an image and draw it |
| drawPolygon()  |  Draw a polygon  | 
| drawPolyline()  |  Draw a polyline  | 
| drawText()  |  Draw text  | 
| fillPath()  |  Fill a path  | 
| fillRect()  |  Fill a rectangle  | 

<br></br>

|  Configuration Methods |  Description |
|  :---:  | --- | 
| setPen()  |  Set the pen  | 
| setBrush()  |  Set the brush  | 
| setFont()  |  Set the font  | 
| setOpacity()  |  Set transparency  | 
| begin()  |  Begin drawing  | 
| end()  |  End drawing  | 
