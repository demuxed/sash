Its been nearly 4 years since Jon and I spitballed the idea of SASH. A lot has changed in that time. I think there's a lot of areas I'd like to re-think as a result of the intervening 4 years.

I've also started putting together what I think the resulting manifests for these changes would look like [in the 0.2 directory](0.2/).

*This is a poorly edited brain dump of the things I think we should think about changing. It was written on a plane. Sorry about the typos.*

## Codecs and Containers

We should be container and codec agnostic. SASH should be a solution for people delivering any media, in any container a user wants. We're opinionated about manifest formats and nothing else.

That said, I think being explicit about signalling codec and container is important. DASH's signalling of container is poor (communicated via MIME type), and currently we're using the same approach. I'd suggest we rename `mime_type` to `container`, and make it simple enum of:
* webm
* fmp4
* cmaf
* ts

FIXME: I just re-read the MSE specification, and actually, we should use MIME type because that's what you need to pass to `MediaSource.isTypeSupported`

TODO: Can/should you have mixed container adaptation sets or manifests?

## Ad insertion / Discos

We need a way to do ad insertion. Without ad insertion this is of limited value to a lot of the community, even if users don't use server-side ads today,  they don't know what their business model will be in 2-5 years.

Here's some options for how we could support ads:

*  Follow HLS and use Discontinuities
    *  Advantage: its not just about ads. Discos are useful for allsorts of other things
*  Follow DASH ad use Periods
    *  Just eugh.
*  Do our own thing!
    *  Template: Use discos, but provide a way for it to work on templates? Something like `discontinious_segments: [3,19,229]` providing a list of segments that have discos at the start of them
    *  Timeline: Make our media item (or whatever we call it) entry in a timeline an object which can include a flag for if its discontinious

TODO: Its also been pointed out that it would be very useful to provide a mechanism for providing a new initialisation segment when a disco is used.

## Decoder startup acceleration support

Having to do a HTTP round trip to get a tiny init segment for each rendition you want to be able to play is inefficient. Smooth gets round this be embedding, SPS and PPS in the manifest.

We should condsider providing a way to signal decoder initialisation data efficiently. Other closed manifest implementations we've seen have done this before by embedding init segments in the manifest (base 64 encoded).

This _could_ also be something where we say "Hey, if you want this, use HTTP 2.0 push to push the init segments from the manifest server"...

## HDR, colour spaces, etc.

We should have a place to signal HDR profile information in the manifest. We should think about if HDR and SDR content can exist in the same adaptation set.

## Mixed-codec adaptation sets

We probably shouldn't support this, even Apple now seem to consider this a mis-step. 

## Roles

I like what we did with Roles, but should we apply some form of validation? 

## DRM

I think we might want a DRM extension for similar reasons to the ad insertion reasoning - people won't invest unless we upfront commit to supporting their business model.

## Adaptation set grouping

Honsetly, I think we might want to re-consider the top level structure of the manifest to split adaptation_sets by their function, specifically `audio` `video` `captions/subtitles`

I think this makes client implementations easier since the first thing any client would likely have to do would be to categorise the assets. I think it also increases human readability of the manifests.

Some thought needs to be put into future extensibility if we do this, along with if `captions` and `subtitles` are the same thing as far as we're concerned. One option is to signal `text_tracks` which would be more extensible because could add VTT chapter support etc. which currently isn't supported anywhere.

We could extend this further however to make each adaptation set a named key, but I think this takes it too far.

## "User Data"

For the longest time when I've built systems, providing a specific space for vendor-specific data has been a life-saver. Usually we've implemented this as a list of key-value pairs that have no reserved function. 

I think providing a specific space in the specification for this type of data would be super helpful.

## 360 / VR / AR

Do we need some specific signalling of this, or is this a 'extend it yourself' place, or should you just use `user_data` ?

## Durations

I love that we made "duration" consistent, but in our segment_template implementation we may want to rename it avg_duration, and at the top level pres_duration, particularly if we implement Timeline support.

## Template / Timeline / Profiles in general

Timeline now makes a tonne more sense to me, especially in a live context, it also opens the window to more elegant ad insertion strategies. 

Lots of people want segment lists or timelines, and I can understand why. Could the follwing 4 profiles cover all use cases:

 * VOD Segment Template-esque
 * VOD Segment Timeline-esque
 * Live Segment Template-esque
 * Live Segment Timeline-esque

## Use less DASH terminology

I don't think we should use DASH terminology if there's better industry terminology.

Replacing `representation` with `rendition` is an obvious improvement in my book. I think removing adaptation_sets is easy if we [make the changes I suggested above](# Adaptation set grouping).

Coming up with better/alternative name for segment_template / segment_timeline might be harder.

## Progressive MP4/WebM etc.

Providing an interchange format which describes availiable MP4 renditions isn't completely insane. I'm not sure if this is interesting to the industry as a whole though.

## Branding

I like the name SASH, I really do, but is it really the best name? Would OpenABR be a better name?

## Captions / Subtitles / Text Tracks

In the README, we declared we were supporing segmented WebVTT. Having now worked with Segmented WebVTT more, I don't like this. Segmented WebVTT is a great way to blote more HTTP requests in your playback experience for VOD, when you could do 1 simple request when playback starts. Its not worth it.

We do need to understand if we can live without segmented WebVTT for live though.

At a higher level, do we actually care if its segmented or not? Is a non-segmented WebVTT just one URL that covers the entire timeline?

## Bandwidth

Should bandwidth be declared in kbps rather than bps? I'm so bored of typing extra `000`.

Or should it be a more complex type, where `"1000k"`, `1000000` and `"1m"` are all the same thing? Oh no wait, one way to do it, right.

## Chunked Transfer low latency stuff

I guess we should support this pre-emptively.