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

* [Simple 1 Audio, 1 Video minimal manifest for VOD](sash-single-audio-single-video-vod-only.json) (The simplest SASH manifest feasible)
* [1 Audio, 2 Video MBR manifest for VOD](sash-mbr-video-single-audio.json) (A fairly common real world scenario)
* [Multi angle, MBR Video, Multi language MBR Audio for VOD](sash-mbr-video-single-audio.json) (Demonstrate ALL THE FEATURES!)

### What concepts does SASH borrow from DASH?

* Segement Template
  * But adds an "end_segment" to signal the end of a representation set.
* Representation Set
* Segmented, Fragmented mp4 media (FMP4)

### What concepts does SASH remove from DASH?

* Removes support for a lot of edge cases by removing some fields, including...
  * ~~`segmentAlignment="true"`~~ Segements in an adaption set **must** be aligned 
  * ~~`startWithSAP="1"`~~ Every Segment **must** start with an SAP
* Removes `period`s as a top level element

### What concepts are new to SASH?

* Declaration of manifest TTL
* Explicit version declaration
* One manifest format for Live and VOD content, and no byteranges

### Is a new standard the solution?

Always.

See also [https://xkcd.com/927](https://xkcd.com/927/) and the election of [Antipope Alexander V](http://en.wikipedia.org/wiki/Antipope_Alexander_V).

### Is this a Joke?

No. We are 100% serious.
