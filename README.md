# Bambu P1 Camera Streamer

Only tested on a P1S.

Built and tested on Ubuntu Latest / amd64.
ARM 64 is not supported due Bambu Library don't work.

Based on: https://github.com/slynn1324/BambuP1Streamer
and https://github.com/hisptoot/BambuSource2Raw.  

# DEPENDENCIES

* [Bambu Studio Proprietary Plugin Library](https://public-cdn.bambulab.com/upgrade/studio/plugins/01.05.00.10/linux_01.05.00.10.zip)
* [Go2Rtc](https://github.com/AlexxIT/go2rtc/)
* wget unzip curl ffmpeg

# BUILD

## build container
```
docker build -t bambu_p1_streamer .
```

# RUN

## Docker (local)
```
docker run -d --name bambu_p1_streamer -p 1984:1984 -p 8554:8554 \
-e PRINTER_ADDRESS=<PrinterIP> -e PRINTER_ACCESS_CODE=12345678 \
-e UI_USERNAME=<UI_USERNAME> -e UI_PASS=<UI_PASS> \
-e RTSP_USERNAME=<RTSP_USERNAME> -e RTSP_PASSWORD=<RTSP_PASSWORD> \
bambu_p1_streamer
```
Port: 1984 Basic API UI
Port: 8554 for RTSP Stream

## Docker compose with Wireguard
Run with docker compose in combination with wireguard.
Download: docker-compose.yml and ip.env

Input the needed data:
```yml
environment:
  - WIREGUARD_PUBLIC_KEY=
  - WIREGUARD_PRIVATE_KEY=
  - WIREGUARD_PRESHARED_KEY=
  - WIREGUARD_ADDRESSES=
  - VPN_ENDPOINT_IP=
  - VPN_ENDPOINT_PORT=
...
environment:
  PRINTER_ADDRESS: 
  PRINTER_ACCESS_CODE: 
  UI_USERNAME: 
  UI_PASS: 
  RTSP_USERNAME: 
  RTSP_PASSWORD: 
```


# ACCESS
###Index Page (only the MJPEG parts will work)
```
http://<host>:1984/links.html?src=p1s
```

### MJPEG Streamurl
```
http://<host>:1984/api/stream.mjpeg?src=p1s
```
### RTSP Streamurl
```
rtsp://<user>:<pw>@<host>:8554/p1s
```
