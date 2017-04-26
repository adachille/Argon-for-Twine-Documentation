---
layout: page
title: 'Part 4: CSS Styling in Twine'
---


The example used in this tutorial can be found [here](https://github.com/blairmacintyre/oldfashioned). It is "test1" found in the "examples" folder.


Argon experience in Twine utilizes CSS for its layout, font, and presentation. Let's begin to add some CSS styling to our existing story in Twine. First, we need to reference our story. In CSS, this is done with a "#." Next, we specify our pointer events.'Pointer-events' allows you to control when a graphic element becomes the target of mouse elements. "Auto" applies to all events. Next, we add in our font families. The example below employs the "Arial" family name and the generic "sans-serif" family. Next, add some padding with pixels. Now, we can specify our background color. The "rgba" function takes four inputs (red,green,blue,opacity). The first three inputs take values from 0 to 255, the opacity input takes values in a decimal range from 0-1.0. The "-webkit-backdrop-filter" property uses the "blur" function to distort the image. The "position" property assigns an "absolute" value. The element is positioned relative to its first positioned (not static) ancestor element. The "bottom" property is placed zero pixels above the bottom-most edge. 

'''css

#story {
  pointer-events: auto;
  font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
  padding: 10px;
  background-color:rgba(255,255,255,0.7);
  -webkit-backdrop-filter: blur(5px);
  position:absolute;
  bottom: 0px;
}

'''

Next, we direct our attention to ".argon-focus". The "transition: opacity" creates a fade of duration 0.8 seconds. We want the element to be visible so we define it as "visible," not "hidden". The "opacity" value of 1 means the image is not transparent at all and easy to view. 

'''css 

.argon-focus #story {
  transition: opacity 0.8s;
  visibility: visible;
  opacity: 1; 
}

'''

For "argon-no-focus", the code is similar. However, the transition property implements the "linear" function. The "linear" command represents a linear animation curve with an animation delay of 0.5 seconds. "Opacity" should have a zero value here which means it is completely transparent.  

'''css

.argon-no-focus #story {
  transition: visibility 0s linear 0.8s, opacity 0.8s;
  visibility: visible;
  opacity: 0;

'''


"Argon-focus" and "argon-no-focus" have an important distinction here. The "argon-focus" class focuses in on the object. The object is highly visible for the user. In contrast, the "argon-no-focus" blurs the object with its use of transition and opacity level. Argon uses these two classes to blur and focus the view element based on events.

Next, we will learn about Panoramas.