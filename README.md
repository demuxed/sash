# SASH
## Simple Adaptive Streaming over HTTP

> The nice thing about standards is that you have so many to choose from. *&mdash; Andrew S. Tanenbaum*

### Overview

SASH is a replacement standard for MPEG DASH's manifest format. Its aims are to provide a simpler, JSON based manifest format which learns from DASH's manifest design, but delivers something very Javascript and Media Source Extension friendly.

### Examples

* [Simple 1 Audio, 1 Video minimal manifest for VOD](sash-single-audio-single-video-vod-only.json) (The simplest SASH manifest feasible)
* [1 Audio, 2 Video MBR manifest for VOD](sash-mbr-video-single-audio.json) (A fairly common MBR scenario)
* [Multi angle, MBR Video, Multi language MBR Audio for VOD](sash-mbr-video-single-audio.json) (Demonstrate ALL THE FEATURES!)

### What concepts does SASH borrow from DASH?

* Segement Template
  * But adds an "end_segment" to signal the end of a representation set.
* Representation Set

### What concepts does SASH remove from DASH?

* Removes support for a lot of edge cases by removing some fields...
  * ~~`segmentAlignment="true"`~~ Segements in an adaption set **must** be aligned 
  * ~~`startWithSAP="1"`~~ Every Segment **must** start with an SAP
* Removes `period`s

### What concepts are new to SASH?

* Declaration of manifest TTL

### Is this a Joke?

No, we're 100% serious.
