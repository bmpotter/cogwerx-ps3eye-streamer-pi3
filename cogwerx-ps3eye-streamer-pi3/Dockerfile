## Docker build for a base raspbian image with [PS3 "Eye" Cam](https://en.wikipedia.org/wiki/PlayStation_Eye) support for mjpg-streamer libraries for Raspberry Pi3
#  Builds upon existing docker image [openhorizon/mjpg-streamer-rpi3](https://hub.docker.com/r/openhorizon/mjpg-streamer-pi3/) (https://github.com/open-horizon/cogwerx-mjpg-streamer-pi3)
#  Reference: http://chris.gg/2012/07/using-a-ps3-eyetoy-with-the-raspberry-pi/


# Start from openhorizon/mjpg-streamer image   351MB
#FROM openhorizon/mjpg-streamer-rpi3  

## Start from resin.io's image   126MB
FROM resin/rpi-raspbian

MAINTAINER dyec@us.ibm.com

RUN apt-get update && apt-get -y install motion
# +76MB

#RUN echo "daemon on" >> /etc/motion/motion.conf
COPY motion.conf /etc/motion/motion.conf

## Use new motion settings file 
#  daemon on (default, no output on output HDMI screen)
#  width 640, #  height 480
#  stream_motion on (always output frames (1 FPS even when no motion detected))
#  stream_localhost off  (stream visible external to machine)
#  stream_port 8080
#  webcontrol_port 8081 (TCP/IP port for the http server to listen on)

EXPOSE 8080

## To verify that the PS3 Eye camera is working, run motion (in non-daemon mode): 
#  `docker run -it --privileged openhorizon/ps3eye-streamer-pi3 motion -n`   # Red / Blue lights should illuminate
#  browse to http://<your Pi3's IP address>:8080 to see a live stream