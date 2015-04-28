# SASH
## Simple Adaptive Streaming over HTTP

> The nice thing about standards is that you have so many to choose from. *&mdash; Andrew S. Tanenbaum*

### Overview

SASH is a replacement standard for MPEG DASH's manifest format. Its aims are to provide a simpler, JSON based manifest format which learns from DASH's manifest design, but delivers something very Javascript and Media Source Extension friendly.

SASH was born out of frustration of supporting many various and incomplete implementations of MPD parsers, and trying to build a reliable, simple, MSE friendly implementations of players.

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
* Seperate Audio & Video representation sets

### Is this a Joke?

No, we're 100% serious.
