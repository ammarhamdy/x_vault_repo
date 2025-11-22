
https://ffmpeg.org/

----
# Convert 

```
ffmpeg -i input.mp4 output.avi
```

```
ffmpeg -formats
```

```
ffmpeg -i input.webm -c:v libx264 -c:a aac output.mp4
```
- `-i input.webm`: Input file
- `-c:v libx264`: Use H.264 for video (compatible with most devices)
- `-c:a aac`: Use AAC for audio (standard for MP4)


---
# Record

## Record the Entire Screen
```sh
>> screen_size=$(xdpyinfo | grep dimensions | awk '{print $2}')
>> ffmpeg -f x11grab -framerate 30 -video_size $screen_size -i $DISPLAY output.mp4
```
OR
```sh
ffmpeg -video_size 1920x1080 -framerate 30 -f x11grab -i :0.0 output.mp4
```
- `1920x1080` → Change this to match your screen resolution.
- `30` → Adjust the frame rate as needed.
- `x11grab` → Captures the X11 display (`:0.0` is the default display).
- `output.mp4` → Output filename.


## Record a Specific Screen Region
```sh
ffmpeg -f x11grab -video_size 800x600 -framerate 30 -i :0.0+100,200 output.mp4
```
`+100,200` → Adjust the top-left corner offset.


##  Record Screen with Audio
```sh
screen_size=$(xdpyinfo | grep dimensions | awk '{print $2}')

ffmpeg -f x11grab -video_size $screen_size -framerate 30 -i $DISPLAY -f pulse -i default output.mp4
```
`-f pulse -i default` → Captures audio from PulseAudio.

## Record with System Audio (if available)
```
pactl list sources | grep "Name:"
```
Look for something like `alsa_output.pci-0000_00_1b.0.analog-stereo.monitor`, then record with:
```sh
ffmpeg -f x11grab -video_size 1920x1080 -framerate 30 -i :0.0 -f pulse -i alsa_output.pci-0000_00_1b.0.analog-stereo.monitor output.mp4
```

## Stop Recording
Press [q] to stop, [?] for help

----

# Speed up the GIF rate

**Using the `setpts` filter:**
```
ffmpeg -i input.gif -filter:v "setpts=0.5*PTS" output.gif
```
- `setpts=0.5*PTS` doubles the playback speed. You can adjust the value (e.g., `0.25` for quadrupling speed, `2.0` for halving speed).


**Using the `-r` option:**
```
ffmpeg -i input.gif -r 20 output.gif
```
This method sets a specific output frame rate for the GIF.
- `-r 20` sets the output frame rate to 20 frames per second. You can adjust this value as needed.


**Combining `setpts` and `-r`:**
```
ffmpeg -i input.gif -filter:v "setpts=0.5*PTS" -r 20 output.gif
```


---
# Fix pad scale issue


### How to Fix: Pad or Scale the Video to Even Dimensions

You can fix this by **adding padding** or **scaling** to make the height divisible by 2.
#### 🔧 Option 1: Pad the video to even dimensions (non-destructive)
```bash
ffmpeg -i input.webm -vf "pad=ceil(iw/2)*2:ceil(ih/2)*2" -c:v libx264 -c:a aac output.mp4
```

#### 🔧 Option 2: Scale the video (can change resolution)
You can force scale to the nearest even number, e.g.:
```bash
ffmpeg -i input.webm -vf "scale=752:964" -c:v libx264 -c:a aac output.mp4
```


---
# Cut mp3

```bash
ffmpeg -i input.mp3 -ss 00:01:00 -to 00:02:30 -c copy output.mp3
```


