# SASH - Simple Adaptive Streaming over HTTP

> The nice thing about standards is that you have so many to choose from. *&mdash; Andrew S. Tanenbaum*

## Overview

SASH is a new standard for adaptive HTTP streaming. SASH is inspired by [MPEG DASH](https://en.wikipedia.org/wiki/Dynamic_Adaptive_Streaming_over_HTTP) and [Apple HLS](https://en.wikipedia.org/wiki/HTTP_Live_Streaming), and is intended to complement them. 

Its aims are to provide a simpler, JSON based manifest format which learns from DASH and HLS's manifest design, but delivers something Javascript and Media Source Extensions friendly.

SASH is designed to be owned and developed by the community, and not be limited by patent pools or usage restrictions.

## Design Goals

1. Be 100% JSON.
2. Be friendly to both Media Source Extensions (MSE) and native clients.
3. Use the good concepts from DASH and HLS. Skip the bad parts.
4. Have one way to do things.
5. Eliminate ambiguity. All client behavior should be defined. Client implementations should never guess.
6. Usable and readable. Don't make developers think. 
7. Be codec and container agnostic.
8. Be compatible with most HLS and DASH media that you've already created.

## Examples

Here's a simple SASH manifest, with 1 audio track and 1 video track, using fragmented MP4 segments.

```json
{
    "sash_version" : 2,
    "presentation_duration": 300,
    "video" : [
        {
            "mime_type" : "video/mp4",
            "segment_template" : {
                "duration": 1.960,
                "init": "http://example.com/ace6123d-021d-41e2-bc31-4a082df189f9/$rendition$/init.m4f",
                "media": "http://example.com/ace6123d-021d-41e2-bc31-4a082df189f9/$rendition$/segment$number$.m4f",
                "start_number": 0,
                "end_number" : 154
            },
            "renditions" : {
                "video-540p-800k" : {
                    "bandwidth": 800000,
                    "codecs": "avc1.4d401e",
                    "height": 480,
                    "width": 852
                }
            }
        }
    ],
    "audio": [
        {
            "mime_type" : "video/mp4",
            "segment_template": {
                "duration": 1.996,
                "init": "http://example.com/ace6123d-021d-41e2-bc31-4a082df189f9/$rendition$/init.m4f",
                "media": "http://example.com/ace6123d-021d-41e2-bc31-4a082df189f9/$rendition$/segment$number$.m4f",
                "start_number": 0,
                "end_number": 154
            },
            "renditions": {
                "audio-64k" : {
                    "bandwidth": 64000,
                    "codecs": "mp4a.40.2"
                }
            }
        }
    ]
}

```

Also see:
* [Separate audio and video](0.2/sash-mbr-video-single-audio.json) (A common real world scenario, compatible with ISO DASH Media)
* [A prototype implementation of a segment-timeline approach, featuring discontinuities](0.2/sash-simple-timeline-with-disco.json)

## 2019 updates TODO list

[I returned to this project after a break. The changes I want to make are documented here.](2019-notes.md)

## How does SASH compare to HLS and DASH?

[How does SASH compare to HLS and DASH?](comparison.md)

## Is a new standard the solution?

Always.

See also [https://xkcd.com/927](https://xkcd.com/927/) and the election of [Antipope Alexander V](http://en.wikipedia.org/wiki/Antipope_Alexander_V).

## Is this a Joke?

No.
