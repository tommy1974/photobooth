[![Build Status](https://travis-ci.org/digitaltom/photobooth.png?branch=master)](https://travis-ci.org/digitaltom/photobooth)
[![Code Climate](https://codeclimate.com/github/digitaltom/photobooth.png)](https://codeclimate.com/github/digitaltom/photobooth)
[![Coverage Status](https://coveralls.io/repos/github/digitaltom/photobooth/badge.svg?branch=master)](https://coveralls.io/github/digitaltom/photobooth?branch=master)

# Photobooth

This application is supposed to run on a linux machine which is connected to a (gphoto)[http://www.gphoto.org/] supported camera ([list](http://www.gphoto.org/proj/libgphoto2/support.php)).

I've build it to run on a Raspberry Pi with openSUSE/Raspbian, connected to a Nikon D60 camera. See below for install instructions.

The *Angular.js* frontend uses a *Ruby on Rails* server on the backend to trigger and process the pictures.
Any tablet or notebook with a web-browser connected to the same wifi as the raspi
will work as a screen.

LEDs can get connected to the Raspberry Pi's gpio ports.
It uses port 23 for 'ready', the ports 4,5,6,17  for picture 1-4 and port 24 for 'image processing'.

By default, the UI runs in read-only mode (no '*take a picture*' and '*delete*' buttons), so that you can share the url with the users,
that are connected to the same wifi. So they can directly download and share the pictures
with their mobile phones.

To load the UI in record mode, open it like this: http://&lt;ip&gt;/?rw/

## Hardware Setup

The general hardware setup looks like this:

```
                               +--------------+
                               |              |
                               |   Camera     |
                               |              |
                               +------^-------+
                                      |
                            USB Cable |
                                      | gphoto lib
+--------------+               +------v------------+
|    Tablet    |    Wifi       | Photobooth server |
|   /Notebook  +-------------> | (eg. Raspberry Pi)|
| with Browser |               |                   |
+--------------+               +------+------------+
                                      | gpio ports
                                Wires |
                                      |
                               +------v-------+
                               |              |
                               |  Status LEDS |
                               |              |
                               +--------------+
```

## Server Setup

The Photobooth can run on any Linux server, for building a portable photo booth I recommend running it on a Raspberry Pi.

General instructions on how to install Rasbian on the Raspberry can be found in  [INSTALL-RASPBIAN.md](INSTALL-RASPBIAN.md)

## Software Setup

- Clone the photobooth repo:
  - `sudo su`
  - `cd /root; git clone https://github.com/digitaltom/photobooth.git`
- Install the needed gems:
  - `echo 'gem: --no-document' >> ~/.gemrc`
  - `gem install bundler`
  - `cd photobooth; bundle install`
- Precompile the assets: `RAILS_ENV=production rake assets:precompile`
- Autostart the app on boot time:
  - `cp photobooth.service /etc/systemd/system/photobooth.service`
  - `systemctl enable /etc/systemd/system/photobooth.service`
- `cp config/options.yml config/options-local.yml` and set your config options in config/options-local.yml

## Operations

Useful commands to run the photobooth

- Control the app with systemd:
  `systemctl <start|stop|restart|status> photobooth`
- See the logfile: `tail -f log/production.log`
- Rake tasks
  - `rake picture_set:record`: Trigger a new picture from console
  - `rake picture_set:recreate_polaroid_images[path]`: Re-create all polaroid images in a batch
  - `rake picture_set:recreate_animations[path]`: Re-create all animations in a batch
  - `rake picture_set:export[output,path]`: Export all images into one output directory

Anything is not working when following this manual? Please open an [issue](https://github.com/digitaltom/photobooth/issues) in the github project!


## My Photobooth:

My current photobox setup is a Raspberry Pi 3, a Nikon D60 with a Nikkor 35mm lens and a Nexus 7 tablet. All build into an old wooden suitcase.
It can run completely from battery for 2-3 hours.  

It was already used at multiple parties and weddings.

![wedding_box](https://user-images.githubusercontent.com/582520/32445572-765e1e0a-c306-11e7-92b4-99331baf6092.png)
