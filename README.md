# SASH
## Simple Adaptive Streaming over HTTP

> The nice thing about standards is that you have so many to choose from. *&mdash; Andrew S. Tanenbaum*

### Overview

SASH is a new standard for adaptive HTTP streaming. SASH is inspired by [MPEG DASH](TODO) and [Apple HLS](TODO), and is intended to complement them. Its aims are to provide a simpler, JSON based manifest format which learns from DASH and HLS's manifest design, but delivers something Javascript and Media Source Extension friendly.

SASH is designed to be owned and developed by the community, and not be limited by patent pools or restrictions.

### Design Goals

1. Be 100% JSON.
2. Designed for MSE and native clients.
3. Use the good parts of DASH and HLS. Skip the bad parts.
4. One way to do things. Follow the Python approach (There should be one -- and preferably only one --obvious way to do it.) rather than the Perl approach (TMTOWTDI).
5. Eliminate ambiguity. All client behavior should be defined. Client implementations should never guess.
6. Usable and readable. Don't make developers think. 
7. Be codec and container agnostic.
8. Be compatible with HLS and DASH media that you've already created.

### Examples

* [Muxed audio and video manifest for VOD](0.1/sash-mbr-muxed-video-audio.json) (Show muxed video and audio)
* [Separate audio and video](0.1/sash-mbr-video-single-audio.json) (A common real world scenario, compatible with ISO DASH Media)
* [Multi angle, MBR Video, Multi language MBR Audio for VOD](0.1/sash-mbr-video-mbr-audio-multi-language-audio.json) (Multi-language audio, multiple camera angles)
* [Audio, video, and subtitles](0.1/sash-mbr-video-single-audio-single-subtitle.json) (What about subtitles?)

TODO: Live exmples!

### How does SASH compare to HLS and DASH?

[How does SASH compare to HLS and DASH?](comparison.md)

### Is a new standard the solution?

Always.

See also [https://xkcd.com/927](https://xkcd.com/927/) and the election of [Antipope Alexander V](http://en.wikipedia.org/wiki/Antipope_Alexander_V).

### Is this a Joke?

No.
