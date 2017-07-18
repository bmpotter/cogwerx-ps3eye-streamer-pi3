## Raspberry Pi3 with a PS3 Eye Cam

![PS3 Eye Cam](https://ibm.box.com/shared/static/brx56ds2iz0x4uxlj72vzqhcwt8wcrs8.jpg)

### Docker build for a base raspbian image with Motion streaming video libraries

This repo contains build files and instructions for a Docker image for Raspberry Pi3 (ARM), which will run the Motion libraries using a PS3 Eye cam on your Pi
See Chris Barnes' [instructions](http://chris.gg/2012/07/using-a-ps3-eyetoy-with-the-raspberry-pi/) for reference

### Initial setup:

Manual pre-setup steps:
* Connect a PS3 Eye camera to a USB port on your Raspberry Pi 3.
* Flash a raspbian-based image (we tested with the [Horizon](https://bluehorizon.network/) raspbian RPi3 image [here](https://bluehorizon.network/documentation/disclaimer))
* Power up your Pi3

You're done with pre-setup steps.

#### To pull a prebuilt docker image: 
You might want to get started immediately from an existing docker image. Pull the container image from docker hub:

```
docker pull openhorizon/ps3eye-streamer-pi3:latest
```

#### (or) To build a docker image yourself:
This took about 15 mins on a Pi3... (longer if the Pi needs to download the resin.io image)


```
git clone https://github.com/open-horizon/cogwerx-ps3eye-streamer-pi3.git
cd cogwerx-ps3eye-streamer-pi3
docker build -t openhorizon/ps3eye-streamer-pi3 .
```

### To run:

* You must run the container in "privileged" mode for docker to allow access to the PS3 Eye USB camera on /dev/video0.

```
docker run -it --rm --privileged -p 8080:8080 openhorizon/ps3eye-streamer-pi3 motion -n
```

Using a web browser, visit your Pi3's IP address followed by 8080 (e.g. http://xxx.xxx.xxx.xxx:8080) on your LAN.
That's it! You should be able to see a streaming video image from your Pi.
  
