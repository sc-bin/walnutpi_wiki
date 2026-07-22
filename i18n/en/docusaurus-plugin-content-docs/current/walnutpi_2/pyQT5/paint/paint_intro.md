---
sidebar_position: 1
---

# Drawing Introduction

Previously, we saw that PyQt5 already has very powerful widget capabilities. However, the widget interfaces are relatively fixed. If we want to DIY and draw some custom graphics, such as points, lines, rectangles, circles, characters, images, etc., we can use the QPainter class drawing functionality.

## QPainter Object

The drawing and setting functions are all in QPainter, located under PyQt5.QtGui.

|  Drawing Methods |  Description |
|  :---:  | --- | 
| drawPoint()  |  Draw point  | 
| drawPoints()  |  Draw multiple points  | 
| drawLine()  |  Draw straight line  | 
| drawLines()  |  Draw multiple straight lines  | 
| drawRect()  |  Draw rectangle  | 
| drawRects()  |  Draw multiple rectangles  | 
| drawRoundedRect()  |  Draw rounded rectangle  | 
| drawEllipse()  |  Draw ellipse (circle)  |
| drawArc()  |  Draw arc  | 
| drawChord()  |  Draw chord  |
| drawImage()  |  Draw image  | 
| drawPath()  |  Draw path  | 
| drawLines()  |  Draw multiple straight lines  | 
| drawPicture()  |  Draw Picture image  |
| drawPie()  |  Draw pie slice  |
| drawPixmap()  |  Extract Pixmap from image and draw |
| drawPolygon()  |  Draw polygon  | 
| drawPolyline()  |  Draw polyline  | 
| drawText()  |  Draw text  | 
| fillPath()  |  Fill path  | 
| fillRect()  |  Fill rectangle  | 

<br></br>

|  Setting Methods |  Description |
|  :---:  | --- | 
| setPen()  |  Set pen  | 
| setBrush()  |  Set brush  | 
| setFont()  |  Set font  | 
| setOpacity()  |  Set transparency  | 
| begin()  |  Begin drawing  | 
| end()  |  End drawing  | 
