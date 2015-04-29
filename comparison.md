# SASH, HLS, and DASH

### What does SASH add to DASH?

* `end_segment` to signal the end of a representation set
* `manifest_ttl` to define manifest refresh behavior

### What concepts does SASH remove from DASH?

* Multiple profiles
* Removes support for a lot of edge cases by removing some fields, including...
  * ~~`segmentAlignment="true"`~~ Segments in an adaption set **must** be aligned 
  * ~~`startWithSAP="1"`~~ Every Segment **must** start with an SAP
* Removes `period`s as a top level element
* `scanType`, `sar`, `timescale`

### What concepts does SASH borrow from HLS?

* Segmented WebVTT for subtitles

### What HLS concepts are not included in SASH?

* Fixed binding of audio representation to video representation
* AUTOSELECT on alternate adaptation sets
* DEFAULT setting on alternate adaptation sets
* TS media

### What concepts are new to SASH?

* Declaration of manifest TTL
* Explicit version declaration
* One manifest format for Live and VOD content, and no byteranges