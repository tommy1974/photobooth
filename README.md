[![Build Status](https://travis-ci.org/digitaltom/photobooth.png?branch=master)](https://travis-ci.org/digitaltom/photobooth)
[![Dependency Status](https://gemnasium.com/digitaltom/photobooth.svg)](https://gemnasium.com/digitaltom/photobooth)
[![Code Climate](https://codeclimate.com/github/digitaltom/photobooth.png)](https://codeclimate.com/github/digitaltom/photobooth)
[![Coverage Status](https://coveralls.io/repos/digitaltom/photobooth/badge.svg?branch=master&service=github)](https://coveralls.io/github/digitaltom/photobooth?branch=master)

# Photobooth

This application is supposed to run on a linux machine which is connected to a gphoto supported camera.
I've build it to run on a raspberry pi 2 with openSUSE, connected to a Nikon D60 camera.

The Angular.js frontend uses a Rails server on the backend to trigger and process the pictures.
As this is a webserver, any tablet with a web-browser will work as a screen.

=== TODO:

* Run without gpio support
* Image upload
* generate qrcode + shortlink for images
* design


=== Prototype pictures:

![alt tag](https://raw.github.com/digitaltom/photobooth/master/public/images/readme/box_front.jpg)
![alt tag](https://raw.github.com/digitaltom/photobooth/master/public/images/readme/internals.jpg)
![alt tag](https://raw.github.com/digitaltom/photobooth/master/public/images/readme/picture_list.jpg)
![alt tag](https://raw.github.com/digitaltom/photobooth/master/public/images/readme/picture_list2.jpg)

