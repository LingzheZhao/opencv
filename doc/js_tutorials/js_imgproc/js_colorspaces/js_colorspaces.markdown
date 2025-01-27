Changing Colorspaces {#tutorial_js_colorspaces}
====================

Goal
----

-   In this tutorial, you will learn how to convert images from one color-space to another, like
    RGB \f$\leftrightarrow\f$ Gray, RGB \f$\leftrightarrow\f$ HSV etc.
-   You will learn following functions : **cv.cvtColor()**, **cv.inRange()** etc.

cvtColor
--------------------

There are more than 150 color-space conversion methods available in OpenCV. But we will look into
the most widely used one: RGB \f$\leftrightarrow\f$ Gray.

We use the function: **cv.cvtColor (src, dst, code, dstCn = 0)**
@param src    input image.
@param dst    output image of the same size and depth as src
@param code   color space conversion code(see **cv.ColorConversionCodes**).
@param dstCn  number of channels in the destination image; if the parameter is 0, the number of the channels is derived automatically from src and code.

For RGB \f$\rightarrow\f$ Gray conversion we use the code cv.COLOR_RGBA2GRAY.

Try it
------

Try this demo using the code above. Canvas elements named cvtColorCanvasInput and cvtColorCanvasOutput have been prepared. Choose an image and
click `Try it` to see the result. You can change the code in the textbox to investigate more.

\htmlonly
<!DOCTYPE html>
<head>
<style>
canvas {
    border: 1px solid black;
}
.err {
    color: red;
}
</style>
</head>
<body>
<div id="cvtColorCodeArea">
<h2>Input your code</h2>
<button id="cvtColorTryIt" disabled="true" onclick="cvtColorExecuteCode()">Try it</button><br>
<textarea rows="7" cols="80" id="cvtColorTestCode" spellcheck="false">
let src = cv.imread("cvtColorCanvasInput");
let dst = new cv.Mat();
// You can try more different parameters
cv.cvtColor(src, dst, cv.COLOR_RGBA2GRAY, 0);
cv.imshow("cvtColorCanvasOutput", dst);
src.delete(); dst.delete();
</textarea>
<p class="err" id="cvtColorErr"></p>
</div>
<div id="cvtColorShowcase">
    <div>
        <canvas id="cvtColorCanvasInput"></canvas>
        <canvas id="cvtColorCanvasOutput"></canvas>
    </div>
    <input type="file" id="cvtColorInput" name="file" />
</div>
<script src="utils.js"></script>
<script async src="opencv.js" id="opencvjs"></script>
<script>
function cvtColorExecuteCode() {
    let cvtColorText = document.getElementById("cvtColorTestCode").value;
    try {
        eval(cvtColorText);
        document.getElementById("cvtColorErr").innerHTML = " ";
    } catch(err) {
        document.getElementById("cvtColorErr").innerHTML = err;
    }
}

loadImageToCanvas("lena.jpg", "cvtColorCanvasInput");
let cvtColorInputElement = document.getElementById("cvtColorInput");
cvtColorInputElement.addEventListener("change", cvtColorHandleFiles, false);
function cvtColorHandleFiles(e) {
    let cvtColorUrl = URL.createObjectURL(e.target.files[0]);
    loadImageToCanvas(cvtColorUrl, "cvtColorCanvasInput");
}
</script>
</body>
\endhtmlonly

inRange
---------------

Checks if array elements lie between the elements of two other arrays.

We use the function: **cv.inRange (src, lowerb, upperb, dst)**
@param src     first input image.
@param lowerb  inclusive lower boundary Mat of the same size as src.
@param upperb  inclusive upper boundary Mat of the same size as src.
@param dst     output image of the same size as src and cv.CV_8U type.

Try it
------

Try this demo using the code above. Canvas elements named inRangeCanvasInput and inRangeCanvasOutput have been prepared. Choose an image and
click `Try it` to see the result. You can change the code in the textbox to investigate more.

\htmlonly
<!DOCTYPE html>
<head>
</head>
<body>
<div id="inRangeCodeArea">
<h2>Input your code</h2>
<button id="inRangeTryIt" disabled="true" onclick="inRangeExecuteCode()">Try it</button><br>
<textarea rows="8" cols="80" id="inRangeTestCode" spellcheck="false">
let src = cv.imread("inRangeCanvasInput");
let dst = new cv.Mat();
let low = new cv.Mat(src.rows , src.cols, src.type(), [0, 0, 0, 0]);
let high = new cv.Mat(src.rows , src.cols, src.type(), [150, 150, 150, 255]);
// You can try more different parameters
cv.inRange(src, low, high, dst);
cv.imshow("inRangeCanvasOutput", dst);
src.delete(); dst.delete(); low.delete(); high.delete();
</textarea>
<p class="err" id="inRangeErr"></p>
</div>
<div id="inRangeShowcase">
    <div>
        <canvas id="inRangeCanvasInput"></canvas>
        <canvas id="inRangeCanvasOutput"></canvas>
    </div>
    <input type="file" id="inRangeInput" name="file" />
</div>
<script>
function inRangeExecuteCode() {
    let inRangeText = document.getElementById("inRangeTestCode").value;
    try {
        eval(inRangeText);
        document.getElementById("inRangeErr").innerHTML = " ";
    } catch(err) {
        document.getElementById("inRangeErr").innerHTML = err;
    }
}

loadImageToCanvas("lena.jpg", "inRangeCanvasInput");
let inRangeInputElement = document.getElementById("inRangeInput");
inRangeInputElement.addEventListener("change", inRangeHandleFiles, false);
function inRangeHandleFiles(e) {
    let inRangeUrl = URL.createObjectURL(e.target.files[0]);
    loadImageToCanvas(inRangeUrl, "inRangeCanvasInput");
}
function onReady() {
    document.getElementById("inRangeTryIt").disabled = false;
    document.getElementById("cvtColorTryIt").disabled = false;
}
if (typeof cv !== 'undefined') {
    onReady();
} else {
    document.getElementById("opencvjs").onload = onReady;
}
</script>
</body>
\endhtmlonly
