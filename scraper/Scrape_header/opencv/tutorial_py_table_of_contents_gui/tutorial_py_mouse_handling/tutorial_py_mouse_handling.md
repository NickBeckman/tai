

OpenCV: Mouse as a Paint-Brush

 MathJax.Hub.Config({
 extensions: ["tex2jax.js", "TeX/AMSmath.js", "TeX/AMSsymbols.js"],
 jax: ["input/TeX","output/HTML-CSS"],
});
//<![CDATA[
MathJax.Hub.Config(
{
 TeX: {
 Macros: {
 matTT: [ "\\[ \\left|\\begin{array}{ccc} #1 & #2 & #3\\\\ #4 & #5 & #6\\\\ #7 & #8 & #9 \\end{array}\\right| \\]", 9],
 fork: ["\\left\\{ \\begin{array}{l l} #1 & \\mbox{#2}\\\\ #3 & \\mbox{#4}\\\\ \\end{array} \\right.", 4],
 forkthree: ["\\left\\{ \\begin{array}{l l} #1 & \\mbox{#2}\\\\ #3 & \\mbox{#4}\\\\ #5 & \\mbox{#6}\\\\ \\end{array} \\right.", 6],
 forkfour: ["\\left\\{ \\begin{array}{l l} #1 & \\mbox{#2}\\\\ #3 & \\mbox{#4}\\\\ #5 & \\mbox{#6}\\\\ #7 & \\mbox{#8}\\\\ \\end{array} \\right.", 8],
 vecthree: ["\\begin{bmatrix} #1\\\\ #2\\\\ #3 \\end{bmatrix}", 3],
 vecthreethree: ["\\begin{bmatrix} #1 & #2 & #3\\\\ #4 & #5 & #6\\\\ #7 & #8 & #9 \\end{bmatrix}", 9],
 cameramatrix: ["#1 = \\begin{bmatrix} f\_x & 0 & c\_x\\\\ 0 & f\_y & c\_y\\\\ 0 & 0 & 1 \\end{bmatrix}", 1],
 distcoeffs: ["(k\_1, k\_2, p\_1, p\_2[, k\_3[, k\_4, k\_5, k\_6 [, s\_1, s\_2, s\_3, s\_4[, \\tau\_x, \\tau\_y]]]]) \\text{ of 4, 5, 8, 12 or 14 elements}"],
 distcoeffsfisheye: ["(k\_1, k\_2, k\_3, k\_4)"],
 hdotsfor: ["\\dots", 1],
 mathbbm: ["\\mathbb{#1}", 1],
 bordermatrix: ["\\matrix{#1}", 1]
 }
 }
}
);
//]]>

 (function() {
 var cx = '002541620211387084530:kaexgxg7oxu';
 var gcse = document.createElement('script');
 gcse.type = 'text/javascript';
 gcse.async = true;
 gcse.src = 'https://cse.google.com/cse.js?cx=' + cx;
 var s = document.getElementsByTagName('script')[0];
 s.parentNode.insertBefore(gcse, s);
 })();

|  |  |
| --- | --- |
| Logo | OpenCV
 4.8.0-dev

Open Source Computer Vision |

var searchBox = new SearchBox("searchBox", "../../search",false,'Search');

$(function() {
 initMenu('../../',true,false,'search.php','Search');
 $(document).ready(function() { init\_search(); });
});

* [OpenCV-Python Tutorials](../../d6/d00/tutorial_py_root.html "../../d6/d00/tutorial_py_root.html")
* [Gui Features in OpenCV](../../dc/d4d/tutorial_py_table_of_contents_gui.html "../../dc/d4d/tutorial_py_table_of_contents_gui.html")

Mouse as a Paint-Brush  

## Goal

* Learn to handle mouse events in OpenCV
* You will learn these functions : **[cv.setMouseCallback()](../../d7/dfc/group__highgui.html#ga89e7806b0a616f6f1d502bd8c183ad3e "Sets mouse handler for the specified window. ")**

## Simple Demo

Here, we create a simple application which draws a circle on an image wherever we double-click on it.

First we create a mouse callback function which is executed when a mouse event take place. Mouse event can be anything related to mouse like left-button down, left-button up, left-button double-click etc. It gives us the coordinates (x,y) for every mouse event. With this event and location, we can do whatever we like. To list all available events available, run the following code in Python terminal: 

import cv2 as cvevents = [i for i in dir(cv) if 'EVENT' in i][print](../../df/d57/namespacecv_1_1dnn.html#a43417dcaeb3c1e2a09b9d948e234c366 "../../df/d57/namespacecv_1_1dnn.html#a43417dcaeb3c1e2a09b9d948e234c366")( events ) Creating mouse callback function has a specific format which is same everywhere. It differs only in what the function does. So our mouse callback function does one thing, it draws a circle where we double-click. So see the code below. Code is self-explanatory from comments : 

import numpy as npimport cv2 as cv# mouse callback functiondef draw\_circle(event,x,y,flags,param): if event == cv.EVENT\_LBUTTONDBLCLK: [cv.circle](../../d6/d6e/group__imgproc__draw.html#gaf10604b069374903dbd0f0488cb43670 "../../d6/d6e/group__imgproc__draw.html#gaf10604b069374903dbd0f0488cb43670")(img,(x,y),100,(255,0,0),-1)# Create a black image, a window and bind the function to windowimg = np.zeros((512,512,3), np.uint8)[cv.namedWindow](../../d7/dfc/group__highgui.html#ga5afdf8410934fd099df85c75b2e0888b "../../d7/dfc/group__highgui.html#ga5afdf8410934fd099df85c75b2e0888b")('image')[cv.setMouseCallback](../../d7/dfc/group__highgui.html#ga89e7806b0a616f6f1d502bd8c183ad3e "../../d7/dfc/group__highgui.html#ga89e7806b0a616f6f1d502bd8c183ad3e")('image',draw\_circle)while(1): [cv.imshow](../../df/d24/group__highgui__opengl.html#gaae7e90aa3415c68dba22a5ff2cefc25d "../../df/d24/group__highgui__opengl.html#gaae7e90aa3415c68dba22a5ff2cefc25d")('image',img) if [cv.waitKey](../../d7/dfc/group__highgui.html#ga5628525ad33f52eab17feebcfba38bd7 "../../d7/dfc/group__highgui.html#ga5628525ad33f52eab17feebcfba38bd7")(20) & 0xFF == 27: break[cv.destroyAllWindows](../../d7/dfc/group__highgui.html#ga6b7fc1c1a8960438156912027b38f481 "../../d7/dfc/group__highgui.html#ga6b7fc1c1a8960438156912027b38f481")() ## More Advanced Demo

Now we go for a much better application. In this, we draw either rectangles or circles (depending on the mode we select) by dragging the mouse like we do in Paint application. So our mouse callback function has two parts, one to draw rectangle and other to draw the circles. This specific example will be really helpful in creating and understanding some interactive applications like object tracking, image segmentation etc. 

import numpy as npimport cv2 as cvdrawing = False # true if mouse is pressedmode = True # if True, draw rectangle. Press 'm' to toggle to curveix,iy = -1,-1# mouse callback functiondef draw\_circle(event,x,y,flags,param): global ix,iy,drawing,mode if event == cv.EVENT\_LBUTTONDOWN: drawing = True ix,iy = x,y elif event == cv.EVENT\_MOUSEMOVE: if drawing == True: if mode == True: [cv.rectangle](../../d6/d6e/group__imgproc__draw.html#gac865734d137287c0afb7682ff7b3db23 "../../d6/d6e/group__imgproc__draw.html#gac865734d137287c0afb7682ff7b3db23")(img,(ix,iy),(x,y),(0,255,0),-1) else: [cv.circle](../../d6/d6e/group__imgproc__draw.html#gaf10604b069374903dbd0f0488cb43670 "../../d6/d6e/group__imgproc__draw.html#gaf10604b069374903dbd0f0488cb43670")(img,(x,y),5,(0,0,255),-1) elif event == cv.EVENT\_LBUTTONUP: drawing = False if mode == True: [cv.rectangle](../../d6/d6e/group__imgproc__draw.html#gac865734d137287c0afb7682ff7b3db23 "../../d6/d6e/group__imgproc__draw.html#gac865734d137287c0afb7682ff7b3db23")(img,(ix,iy),(x,y),(0,255,0),-1) else: [cv.circle](../../d6/d6e/group__imgproc__draw.html#gaf10604b069374903dbd0f0488cb43670 "../../d6/d6e/group__imgproc__draw.html#gaf10604b069374903dbd0f0488cb43670")(img,(x,y),5,(0,0,255),-1) Next we have to bind this mouse callback function to OpenCV window. In the main loop, we should set a keyboard binding for key 'm' to toggle between rectangle and circle. 

img = np.zeros((512,512,3), np.uint8)[cv.namedWindow](../../d7/dfc/group__highgui.html#ga5afdf8410934fd099df85c75b2e0888b "../../d7/dfc/group__highgui.html#ga5afdf8410934fd099df85c75b2e0888b")('image')[cv.setMouseCallback](../../d7/dfc/group__highgui.html#ga89e7806b0a616f6f1d502bd8c183ad3e "../../d7/dfc/group__highgui.html#ga89e7806b0a616f6f1d502bd8c183ad3e")('image',draw\_circle)while(1): [cv.imshow](../../df/d24/group__highgui__opengl.html#gaae7e90aa3415c68dba22a5ff2cefc25d "../../df/d24/group__highgui__opengl.html#gaae7e90aa3415c68dba22a5ff2cefc25d")('image',img) k = [cv.waitKey](../../d7/dfc/group__highgui.html#ga5628525ad33f52eab17feebcfba38bd7 "../../d7/dfc/group__highgui.html#ga5628525ad33f52eab17feebcfba38bd7")(1) & 0xFF if k == ord('m'): mode = not mode elif k == 27: break[cv.destroyAllWindows](../../d7/dfc/group__highgui.html#ga6b7fc1c1a8960438156912027b38f481 "../../d7/dfc/group__highgui.html#ga6b7fc1c1a8960438156912027b38f481")() ## Additional Resources

## Exercises

1. In our last example, we drew filled rectangle. You modify the code to draw an unfilled rectangle.

---

Generated on Wed Oct 4 2023 23:37:11 for OpenCV by  [![doxygen](../../doxygen.png)](http://www.doxygen.org/index.html "http://www.doxygen.org/index.html") 1.8.13

//<![CDATA[
addTutorialsButtons();
//]]>
