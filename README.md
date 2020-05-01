# cool-tricks
Cool tricks to remember

## General settings

See [averissimo/config-files](https://github.com/averissimo/config-files)

This might be a private repository, sorry

## Use DSLR as webcam

[from stackoverflow](https://askubuntu.com/questions/856460/using-a-digital-camera-canon-as-webcam)

Requirements:

```
$ sudo apt install gphoto2 v4l2loopback-utils ffmpeg
```

Use it *(after plugging in camera via usb cable)*

```
#!/bin/bash

# killall gphoto processes
ps -aux | grep gphoto | grep -v grep | awk '{ print $2 }' | xargs kill -9 

# add video loopbackd device
sudo modprobe v4l2loopback

# Use gphoto to capture and pipe it to loopback device (that can be used by skype, zoom, etc..)
gphoto2 --stdout --capture-movie | ffmpeg -i - -vcodec rawvideo -pix_fmt yuv420p -threads 0 -f v4l2 /dev/video2
```

note: `/dev/video2` might be different *(depending on computer)*, use `v4l2-ctl --list-devices` to see which one is the loopback *(dummy)*
