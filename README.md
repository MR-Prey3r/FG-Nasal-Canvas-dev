# FG-Nasal-Canvas-dev
This is repo contains my personal notes of learning to develop canvas stuff with nasal scripting for flightgear


# Steps for a minimal canvas dialog window to be run from the nasal console

### flow:
window -> canvas -> group -> child element -> set properties like background color, font size/color/weight/type etc
& the bg color belongs to the canvas obj, the window title belongs to window obj

### desc:
- create a window since canvas can't be drawn on its own. It needs a dialog/hud/canvas window to be drawn onto
```javascript
var win = canvas.Window.new([width,height], "dialog");
```
- create a canvas into that window
```javascript
var canv = win.createCanvas()'
```
- create a canvas group into the canvas, which holds the elements(i.e texts) into it
```javascript
var rootGrp = canv.createGroup();
```
- add child elements(i.e texts) to the group now
```javascript
rootGrp.createChild("text")
```
- now add element properties to the elements (this step is attached with the prev one, so there will be only a single createChild function)
```javascript
rootGrp.createChild("text")
    .setText("Hello Canvas Desktop")
      .setFontSize(25, 1.0)
      .setColor(1,0,0,1)
      .setAlignment("center-center")
      .setTranslation(160, 80);
```


### Here's a complete demo Canvas dialog:
```javascript
var win = canvas.Window.new([512,512], "dialog");
win.set("title","My new canvas");

var canv = win.createCanvas();
canv.setColorBackground(1,1,1,0.5); // # hex code can be used too & less opacity of the window background can affect the text opacity as well!!!

var grp = canv.createGroup();
grp.createChild("text")
      .setText("Hello Canvas Desktop")
      .setFontSize(25, 1.0)          // font size (in texels) and font aspect ratio
      .setColor(1,0,0,1)             // red, fully opaque
      .setAlignment("center-center") // how the text is aligned to where you place it
      .setTranslation(160, 80);     // where to place the text
                                    // slash is used here due to discord syntax issues since # is used in bash, not in JS
      
```


# Steps for creating raster images with canvas

just use "image" as the element
```javascript
rootGroup.createChild("image")
    .setFile( url ) 
    .setTranslation(45,22)
    .setSize(310,155);
```

full example:
```javascript
var win = canvas.Window.new([400, 200], "dialog");
win.set("title","Demo raster image canvas");

var myCanvas = win.createCanvas();
myCanvas.setColorBackground("#030238");

var rootGroup = myCanvas.createGroup();

var url = "https://docs.flybywiresim.com/pilots-corner/a380x/assets/a380x-briefing/flight-deck/main/nd.png";

# create an image child for the texture
var child=rootGroup.createChild("image")
    .setFile( url ) 
    .setTranslation(45,22)
    .setSize(310,155);
```

### better image sizing
```javascript
var win = canvas.Window.new([350, 540], "dialog");
win.set("title","Demo raster image canvas");

var myCanvas = win.createCanvas();
myCanvas.setColorBackground("#030238");

var rootGroup = myCanvas.createGroup();

var url = "https://docs.flybywiresim.com/pilots-corner/a380x/assets/a380x-briefing/flight-deck/main/nd.png";

# create an image child for the texture
var child=rootGroup.createChild("image")
    .setFile( url ) 
    .setTranslation(0,0)
    .setSize(350,540);
```
