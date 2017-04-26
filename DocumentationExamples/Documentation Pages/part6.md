---
layout: page
title: 'Part 6: Incorporating Vuforia in Your Twine Experience'
---

To begin using Vuforia with your Twine story, you need to have a server available to host online. If you are a Georgia Tech student, you are in luck! You can find out how to do so [here](https://faq.oit.gatech.edu/content/how-do-i-setup-new-homepage-prism-web-server). If you are not a Tech student, try [this](http://www.webhostingsecretrevealed.net/web-hosting-beginner-guide/).

After you have your server, you can proceed. The next step is to generate a Vuforia license key. First, navigate to this [website](https://developer.vuforia.com/license-manager). You will need to create an account. After creating an account, you can generate a license key. Warning: do not share your key with others because you are only alloted so many "recos" before you are charged. A "reco" occurs when your app recognizes an image in a cloud database. Your license key will look like a long block of randomly generated characters. 

After you generate your Vuforia license key, navigate to [this page](http://docs.argonjs.io/start/vuforia-pgp-encryptor/). Don't publish your key in a public folder! Now comes the tricky bit. Paste your key in the box titled "Vuforia Key." Read the instructions below, and then type in your server address with this format: "?(*.)yourwebsitehere.com**". Copy the new encrypted key under the "License Data (encrypted)" box. 

Now you should download the entire "samples" folder from the [Argon Github](https://github.com/argonjs/samples). Navigate to the Vuforia folder, inside you should find an "app.ts" file. Open the file in your favorite text editor. Scroll until you find a block of code that looks like your Vuforia key. Replace this key with your own encrypted key, and upload this to your website. 