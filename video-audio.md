# Video and Audio

1. WebRTC, RTMP, RTSP, RTP, SRT, QUIC, HEVC(H.265), AVC (H.264), DASH(MPEG-DASH), HLS, flv, mp4
2. tcp, udp, http
3. 音视频采集, 编解码, 传输, 控制, 播放.

## Transport

1. RTMP - TCP
2. WebRTC - UDP

## Tools

```bash
# flv -> mp4
ffmpeg -i input.flv -codec copy output.mp4
```
