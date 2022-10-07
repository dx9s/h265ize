== Review examples ==
* https://unix.stackexchange.com/questions/230800/re-encoding-video-library-in-x265-hevc-with-no-quality-loss


``` 
I've recently gone through the trouble of Transcoding my whole video catalog over to HEVC. I use https://github.com/FallingSnow/h265ize with the following settings.

h265ize -v -m medium -q 20 -x --no-sao --aq-mode 3 --delete --stats

-v - Verbose Output
-m medium - Medium encode speed (smaller higher quality, anything slower I find is not worth the time/quality dif)
-q 20 - the CRF used, 20 is similar to 18 or so in x264 but hey. This is for 1080p content (90% of my TV) I tend to use 22 for my 4K movies
-x - Use x265 central defined commands
--no-sao turns off Sample Adaptive Offset (improves speed of encode)
--aq-mode 3 - use Adaptive Quantisation with auto variance, helps 8bit encodes, especially in dark areas, stops most of the banding that can happen (at expense of encode time though)
--delete - replace encoding file with encoded file (test before using this one)
--stats - Write stats out to a csv file in the root of the path you ran from.

Encode speeds are around 30fps (for most 1080p stuff) on my rig. Dual Xeon E5 2687W v2, but I force the FFMPEG process to not use the first side of one of the processors (It's my Plex server, so have to make sure there's overhead for transcode if needed on playback etc)

Yes it took a while to convert most of it over, and now I have a scheduled task that runs twice a day to encode the stuff from that day over to x265.

The space savings have been enormous. My initial SAN was at 20Tb use, now it's around 12 but obviously has been added too with 6 months more content.

I've started to transcode all my Movies over too, however, that's an ongoing process, as I have to ID quality levels (Radarr fortunately labels then nicely) and use one of three transcode settings:

-m slower -q 18 -x --no-sao --aq-mode 3 for 720p transcodes
-m medium -q 20 -x --no-sao --aq-mode 3 for 1080p
-m medium -q 22 -x --no-sao for 2160p

Hope that helps some people. Shout if anyone needs a hand setting it all up. And before you encode everything to x265, think about playback, if the client doesn't support x265 native, then the transcade can be expensive in terms of CPU and Quality.

```


== Determine if resizing can be done ==

