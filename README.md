# SASH
## Simple Adaptive Streaming over HTTP

> The nice thing about standards is that you have so many to choose from. *&mdash; Andrew S. Tanenbaum*

### Overview

SASH is a replacement standard for MPEG DASH's manifest format. Its aims are to provide a simpler, JSON based manifest format which learns from DASH's manifest design, but delivers something very Javascript and Media Source Extension friendly.

SASH was born out of frustration of supporting many various and incomplete implementations of MPD parsers, and trying to build a reliable, simple, MSE friendly implementations of players.

### Design Goals

1. 100% less XML.
2. Designed for MSE and native clients.
3. Use the good parts of DASH. Skip the bad parts.
4. One way to do things. Follow the Python approach (There should be one -- and preferably only one --obvious way to do it.) rather than the Perl approach (TMTOWTDI).
5. Eliminate ambiguity. All client behavior should be defined. Client implementations should never guess.
6. Usable and readable. Don't make developers think. 

### Examples

* [Muxed audio and video manifest for VOD](0.1/sash-mbr-muxed-video-audio.json) (Show muxed video and audio)
* [Separate audio and video](0.1/sash-mbr-video-single-audio.json) (A fairly common real world scenario)
* [Multi angle, MBR Video, Multi language MBR Audio for VOD](0.1/sash-mbr-video-mbr-audio-multi-language-audio.json) (Multi-language audio, multiple camera angles)
* [Audio, video, and subtitles](0.1/sash-mbr-video-single-audio-single-subtitle.json) (What about subtitles?)

### Is a new standard the solution?

Always.

See also [https://xkcd.com/927](https://xkcd.com/927/) and the election of [Antipope Alexander V](http://en.wikipedia.org/wiki/Antipope_Alexander_V).

### Is this a Joke?

No.
