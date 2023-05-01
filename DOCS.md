# you stream mic

## important

In your go2rtc, add this stream

```
streams:
  webcam: "ffmpeg:device?video=1&resolution=640x480#video=h264#hardware"
```

### audio only aac:

```
ffmpeg -f alsa -ac 1 -i default -c:a aac -ar:a 16000 -ac:a 1 -rtsp_transport tcp -f rtsp rtsp://localhost:8554/webcam
```

### audio only opus:

```
ffmpeg -f alsa -ac 1 -i default -c:a libopus -ar:a 16000 -ac:a 1 -rtsp_transport tcp -f rtsp rtsp://localhost:8554/webcam
```

### video only:

```
ffmpeg -hide_banner -hwaccel vaapi -hwaccel_output_format vaapi -f v4l2 -video_size 640x480 -i /dev/video2 -c:v h264_vaapi -g 50 -bf 0 -profile:v high -level:v 4.1 -sei:v 0 -an -vf "format=vaapi|nv12,hwupload" -user_agent ffmpeg/go2rtc -rtsp_transport tcp -f rtsp rtsp://localhost:8554/webcam
```

### audio and video:

```
ffmpeg -f alsa -ac 1 -i default -c:a libopus -ar:a 16000 -ac:a 1 -hide_banner -hwaccel vaapi -hwaccel_output_format vaapi -f v4l2 -video_size 640x480 -i /dev/video2 -c:v h264_vaapi -g 50 -bf 0 -profile:v high -level:v 4.1 -sei:v 0 -an -vf "format=vaapi|nv12,hwupload" -user_agent ffmpeg/go2rtc -rtsp_transport tcp -f rtsp rtsp://localhost:8554/webcam
```
