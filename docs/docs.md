# Links 
- https://gist.github.com/TaylorBurnham/b53f24083d6030947804db8e96a4da7c


## Notes 
- Core Knowledge Areas
  - FFMPEG 
  - Tensor Flow 
  - Video Formats and streaming formats/tech
  - ONVIF
- firgate uses ffmpeg to get video feed from camera 
- ffmpeg -> video segments -> frigate processing 
- detect resolution to be configure 
  - Eg 320 x 320 
- create motion mask in areas where unwanted motion happens ; including camera timestamps
- If format is not h264 , disable rtmp 
- For getting pics of events , enable snapshots
- define zones ; events can be limited to required_zones 
- Tune for reducing false positives
- Integration with home assistant 
- See frigate/config.py : roles are record, rtmp and detect
- Where is tensor flow used , locate the interfacing 
- restreaming using rtmp 
- custom tf models 
- list of objects 




# Regarding mqtt-acl.conf 
- See https://mosquitto.org/documentation/authentication-methods/
- Using docker 
```bash  
  docker run -it eclipse-mosquitto sh
  mosquitto_passwd  -c  ./pass.conf frigate  # frigate 
  mosquitto_passwd  ./pass.conf amx          # amx
```

## Camera 1 
- 2304 x 1296 / 2k 
- 15 fps 
- 

## Logs 
```bash 
udp://nandanam:9481940333@192.168.0.186/stream1

https://ffmpeg.org/ffmpeg-protocols.html

ffmpeg -f avfoundation -list_devices true -i ""

# Working Stream 

rtsp://nandanam:9481940333@192.168.0.2/stream1
# Adjust Frame Rate 

ffmpeg \
  -f avfoundation \
  -pix_fmt yuyv422 \
  -video_size 640x480 \
  -framerate 15 \
  -i "0:0" -ac 2 \
  -vf format=yuyv422 \
  -vcodec libx264 -maxrate 2000k \
  -bufsize 2000k -acodec aac -ar 44100 -b:a 128k \
  -f rtp_mpegts udp://127.0.0.1:9988


# RTSP 

ffmpeg \
  -f avfoundation \
  -pix_fmt yuyv422 \
  -video_size 640x480 \
  -framerate 15 \
  -i "0:0" -ac 2 \
  -vf format=yuyv422 \
  -vcodec libx264 -maxrate 2000k \
  -bufsize 2000k -acodec aac -ar 44100 -b:a 128k \
  -f rtp_mpegts udp://127.0.0.1:9988
  ```
  