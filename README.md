
# rtsp-simple-server

_rtsp-simple-server_ is a simple an ready-to-use RTSP video server, a program that allows multiple users to publish or read live video and audio streams. RTSP a standardized protocol that defines how to perform these operations with the help of a server, that both publishers and readers can contact in order to negotiate a streaming protocol and write or read data. The server is then responsible of linking the publisher stream with the readers.

This software was developed with the aim of simulating a live camera feed for debugging purposes, and therefore to use files instead of real streams. Another reason for the development was the deprecation of _FFserver_, the component of the FFmpeg project that allowed to create a RTSP server with _FFmpeg_ (but this server can be used with any software that supports RTSP).

It actually supports *one* publisher, while readers can be more than one.


## Installation

Precompiled binaries are available in the [release](https://github.com/aler9/rtsp-simple-server/releases) page. Just download and extract the executable.


## Usage

1. Start the server:
   ```
   ./rtsp-simple-server
   ```

2. In another terminal, publish something with FFmpeg (in this example it's a video file, but it can be anything you want):
   ```
   ffmpeg -re -stream_loop -1 -i file.ts -map 0:v:0 -c:v copy -f rtsp rtsp://localhost:8554/
   ```

3. Open the stream with VLC:
   ```
   vlc rtsp://localhost:8554/
   ```

   you can alternatively use GStreamer:
   ```
   gst-launch-1.0 -v rtspsrc location=rtsp://localhost:8554/ ! rtph264depay ! decodebin ! autovideosink
   ```

## Full command-line usage

```
usage: rtsp-simple-server [<flags>]

rtsp-simple-server

RTSP server.

Flags:
  --help            Show context-sensitive help (also try --help-long and --help-man).
  --version         print rtsp-simple-server version
  --rtsp-port=8554  port of the RTSP TCP listener
  --rtp-port=8000   port of the RTP UDP listener
  --rtcp-port=8001  port of the RTCP UDP listener
```

## Links

Specifications
* https://tools.ietf.org/html/rfc7826
