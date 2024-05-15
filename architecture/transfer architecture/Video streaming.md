# Theory
Video streaming has two similar but incredibly different use cases, live streaming and video streaming (twitch vs youtube). And there is a third party. bi-directional streaming (google meet).

- For **live streaming** The best are **RTMP** or **HLS** (twitch still uses RTMP)
- For **video streaming** (on demand streaming) **DASH** is better.
- For **bi-directional streaming** WebRTC is the best

**Adaptive streaming** is a key feature of modern video streaming technology. It adjusts the stream's bitrate or quality dynamically during playback, based on the viewer's [[bandwidth]] and [[network]] conditions. This ensures an optimal viewing experience, minimizing buffering and playback interruptions.

## DASH (MPEG-DASH)
Dynamic Adaptive Streaming over [[HTTP]]. **International standard** for streaming video and audio over the Internet, But excels at **video streaming** (on demand streaming). uses [[protocols#Main Network Protocols|TCP]] and runs over http. It allows **adaptive streaming**. Segments packages and ensures **low latency**. It is also codec agnostic. Hence you can use any codec you want.

It's used on youtube and netflix
## HLS
[[HTTP]] Live Streaming. Primarily for **live streaming**. Designed to work efficiently over a **variety of [[network]]s**, including high-speed broadband and mobile networks. Segments media into small fragments for separate download, facilitating **adaptive streaming**.

Offers broad compatibility, especially with Apple devices. However, it tends to have **higher latency** and quality limitations compared to other protocols.

is (mostly) the **only one** that works **on apple** (they created it with it's codecs in mind).

## RTMP
Real Time Messaging Protocol. Primarily for **live streaming**. Known for its low latency even though it's older, widely used with the **flash** player. and runs over [[protocols#Main Network Protocols|TCP]]. It has a lot of variants like
RTMPT (tunneled through HTTP), RTMPE (encrypted), RTMPTE (tunneled and encrypted), RTMFP (travels over UDP instead of TCP), RTMPS (encrypted over [[SSL]]). Known for it's **low latency** 

## WebRTC

Is a popular open-source project that allows **real-time communication** between **web browsers** and mobile applications through a set of APIs. This modern video protocol is used for **video conferencing**, peer-to-peer file sharing, and live streaming. used on google meet and zoom (zoom uses a [[chromium]] based solution). It uses **UDP**, therefore there is **no guaranteed delivery** of packets, which may cause losses or **delays** during **transmission**. This can result in choppy or interrupted video streams.

# Practice
## DASH (MPEG-DASH)

To use DASH for streaming you will need 2 parts. The video well encoded (with a MPD file) served in a http server (can be a local http-server or on aws [[Storage#S3|S3]]). And the second part is a frontend client that understand what dash is (with a library)

### encoding

The first step is encoding. What you need are 2 main things. A manifest (.MPD file) this is a xml file that tells what type of encodings are you using what resolutions and their locations. The second part is the encoding files, this will be streams of the duration you desire
![[DashStreams.png]]


The best way is using [[ffmpeg]]. You just run one command and get all of the expected output. In my case (to stream on 3 different resolutions and bitrates keeping the audio separate)
```shell
ffmpeg -i inputVideo.mp4 
-map 0 -b:v:0 500k -s:v:0 640x360 -c:v:0 libx264 -b:a:0 96k 
-map 0 -b:v:1 1000k -s:v:1 1280x720 -c:v:1 libx264 -b:a:1 128k  
-map 0 -b:v:2 3000k -s:v:2 1920x1080 -c:v:2 libx264 -b:a:2 192k  
-f dash -use_template 1 -use_timeline 1 -seg_duration 4  
-adaptation_sets "id=0,streams=v id=1,streams=a" output.mpd
```
The command should be on a single line. I've separated it for better visualization

### client
Finally you need a client that understands. This is done in html

```html
<script src="https://cdn.dashjs.org/latest/dash.all.min.js"></script>

<video id="videoPlayer" width="640" height="360" controls></video>

<script>
var url = "https://ytclone-dcanasp.s3.amazonaws.com/test/output.mpd"; 
var player = dashjs.MediaPlayer().create();
player.initialize(document.querySelector("#videoPlayer"), url, true);
```
That code will stream with dash (that's really all) But if you want to select the bitrate you can continue that code
```html
<script>
var url = "https://ytclone-dcanasp.s3.amazonaws.com/test/output.mpd"; 
var player = dashjs.MediaPlayer().create();
player.initialize(document.querySelector("#videoPlayer"), url, true);

player.on(dashjs.MediaPlayer.events.STREAM_INITIALIZED, function() {
var videoQualities = player.getBitrateInfoListFor("video");
var qualitySelector = document.getElementById('qualitySelector');
	videoQualities.forEach((quality, index) => {
	var option = document.createElement('option');
	option.value = index;
	option.text = quality.qualityIndex + " (" + quality.bitrate / 1000 + " kbps)";
	qualitySelector.appendChild(option);
	});
	qualitySelector.onchange = function() {
	player.setQualityFor("video", this.value);
	};
});
    </script>
```
that code will give you a menu to chose the bitrate you desire 

