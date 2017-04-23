---
layout: page
title: 'Part 5: Panoramas'
---

In this tutorial, you will create an AR experience that utilizes panoramas. Let's begin by creating a new Twine story and entering the JavaScript editor. Remember that the first code you must add to any AR Twine experience is the 'passage-cleanup'. For this experience, the same code as the previous example will suffice.

We now need to add three important macros to give our AR experience panorama functionality.

The first macro we must define is 'createPanorama'. This macro will be called in the StoryInit passage and be used to initialize a panorama that we may later use in our Twine passages. It takes in three arguments, a name, a dataset url, and a string containing the latitude, longitude, and altitude, of the location of the panorama. We will also be creating a short helper function for our createPanorama macro. Add the code below.

''' javascript

A helper function for createPanorama that gets information from the arguments passed into it.
    function getComponentAttrFromArg(arg) {
        var eq = arg.indexOf("=");
        if (eq == -1) {
            return(arg);
        } else if (eq == 0 || eq == arg.length-1) {
            return "";
        } else {
            return arg.slice(0,eq) + ":" + arg.slice(eq+1) + ";";
        }
    }

LLA stands for latitude, longitude, altitude

    Macro.add(['createPanorama'], {
        handler() {
            if (this.args.length < 3) {
                    return this.error('required parameters are {name, dataset url, LLA}, plus other optional additional parameters');
            }
            console.log("new panorama '" + this.args[0] + "', url: " + this.args[1]);
            var argValue = "src:url(" + this.args[1] + ");lla:" + this.args[2] + ";";

            // Manipulates the argument to get the necessary information. Above the 'createPanorama' macro, you can find the helper function that this loop utilizes.
            for (var i = 3; i<this.args.length; i++) {
                argValue += getComponentAttrFromArg(this.args[i]);
            }

            // Adds the panorama into Argon
            $('#argon-aframe').attr("panorama__" + this.args[0], argValue);
        }
    });

'''

The second macro we will define is 'requestPanoramaReality', which can be used in our story passages to retrieve a panorama reality that we will need to place our panorama in. The macro will take in two arguments, the name of the panorama reality we want to create and the url of the panoramaReality. Finally, we will add a last, simple macro that will display the panorama of our choosing. The only parameter we need is the name of the panorama.

''' javascript

//var panoramaRealityURL = "http://argonjs.io/argon-aframe/resources/reality/panorama/index.html"
Macro.add(['requestPanoramaReality'], {
    handler() {
        if (this.args.length < 2) {
            return this.error('required parameters are name and url');
        }
        console.log("new reality '" + this.args[0] + "', url: " + this.args[1]);
        $('#argon-aframe').attr("desiredreality", "name:'" + this.args[0] + "';src:url(" + this.args[1] + ");");
    }
});


Macro.add(['showPanorama'], {
    handler() {
        if (this.args.length < 1) {
            return this.error('parameter is panorama name');
        }
        console.log("show panorama '" + this.args[0]);
        $('#argon-aframe')[0].emit("showpanorama", { name: this.args[0] });
    }
});

'''

Now, onto the fun part! Leave the editor, open the auto=generated empty passage, and name it 'Start'. Remember that the first passage must always be the 'Start' passage.

We will now create our 'StoryInit' passage. Click the add passage button and navigate to its editor. Let's initialize a few panoramas, keeping in mind the three arguments that 'createPanorama' requires. Add the following code to the passage.

'''

<<createPanorama aquarium http://bmaci.com/a4/twine/panoramas/aqui.jpg "-84.3951 33.7634 206" initial=true>>
<<createPanorama skyline http://bmaci.com/a4/twine/panoramas/cent.jpg "-84.3931 33.7608 309">>
<<createPanorama museum http://bmaci.com/a4/twine/panoramas/high.jpg "-84.38584 33.79035 289">>
<<createPanorama park http://bmaci.com/a4/twine/panoramas/pied.jpg "-84.37427 33.78577 271">>

'''

Notice that the first 'createPanorama' has an extra parameter. That parameter simply lets Argon know which that you plan to use that panorama first.

Now that we've initialized the panoramas, we can move on to the 'Start' passage. We will now need the other two macros we added: 'requestPanoramaReality' and 'showPanorama'. Add this code to your 'Start' passage.

'''

Here we see our first panorama, take a look around! Notice how the resolution is diminished, a result of expanding the picture to a 360 degree view. [[Click next|second]] to see how 3D objects look when placed on a panorama.

<<requestPanoramaReality "Panorama Reality" "http://bmaci.com/a4/twine/panoramaReality/index.html">>
<<showPanorama aquarium>>


'''

With our next passage, let's try to overlay our panorama with some 3D objects. Think back to tutorial 3. How did we add 3D objects to a scene?

Remember, we first have to add the append3d (and optionally the replace3d) macro into the JavaScript component before we can begin placing 3D objects into our scene. After that's done, we can start creating all kinds of 3D objects. Your second passage can look something like this:

'''

Here is our second panorama, and as you can see (you might have to look around), we have added some 3D objects to it! Click [[here|Start]] to go back to the 'Start' scene.

<<requestPanoramaReality "Panorama Reality" "http://bmaci.com/a4/twine/panoramaReality/index.html">>
<<showPanorama skyline>>

<<append3d story sphere-and-box>>
<a-sphere position="0 1.25 -5" radius="1.25" color="pink" ></a-sphere><a-box id="bluebox" position="5 0.5 -5" rotation="0 45 0" width="1" height="1" depth="1"  color="blue"></a-box>
<</append3d>>

'''

Now that we have shown you the basic process for adding panoramas to your AR experiences, you should go ahead and play around and practice what you've learned. Feel free to implement passages for the last two panoramas!

When you are ready, continue onto the next tutorial, which will be all about utilizing Vuforia.



//TODO: explain what a panoramaReality and dataseturl are and see if you have to alter the requestPanoramaReality paragraph.

//TODO: check if you can make the names for panoramas longer than four letters long. If so, call them: aquarium, skyline, artMuseum, and park.

//Macros you need
//createReferenceFrameEntity