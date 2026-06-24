# Source: https://docs.samply.app/playback-loudness-matching.html

# Loudness Matching [​](https://docs.samply.app/#loudness-matching)

When comparing two different mixes of the same track, it's often helpful to first ensure that the two are at approximately the same loudness. If we remove loudness as a variable in our comparison, then we can be more confident that we don't just prefer a mix simply because it's louder.

Mixing engineers often use measures of loudness called Loudness Units relative to Full Scale (LUFS) and True Peak (TP) to quantify "loudness" in a manner that accounts for the frequency response of the human auditory system. In fact, LUFS and TP are part of an [international standard](https://www.itu.int/rec/R-REC-BS.1770) which defines how they can be calculated using digital signal processing (DSP). Because LUFS and TP are standards, streaming services like Spotify use them to normalize the loudness of all uploaded tracks.

_Note: In Samply, loudness matching is off by default and completely optional. It does not apply to any tracks uploaded prior to September 6th, 2022._

## Using Loudness Matching [​](https://docs.samply.app/#using-loudness-matching)

Under your **Audio preferences** located on the left in the app sidebar, first enable the loudness matching switch.

The same options are available to your clients from shared players that have loudness matching enabled in the player options.

### Loudness Penalty platform [​](https://docs.samply.app/#loudness-penalty-platform)

[![](https://storage.crisp.chat/users/helpdesk/website/404a5021fea83800/31841d93-071c-4a8f-b782-013706_13l1991.png)](https://downloads.intercomcdn.com/i/o/683882393/ce390e575fdb2aaa827f1d9d/image.png)

Samply partners with [Loudness Penalty](https://www.loudnesspenalty.com/?utm_source=samply) to allow platform-specific loudness matching. Simply select which of the streaming platforms you'd like to emulate with track-level loudness matching. The currently supported platforms are (left to right):

- Spotify
- Apple Music
- Tidal
- Amazon Music
- YouTube Music

### Custom LUFS [​](https://docs.samply.app/#custom-lufs)

[![](https://storage.crisp.chat/users/helpdesk/website/e8b6d58a43eb1800/2d11aaab-f175-4d09-8c41-75d6bc_1sw2bzo.png)](https://downloads.intercomcdn.com/i/o/683882060/0943c07940c068bdd63bbce1/image.png)

Then, you can adjust the target LUFS by entering a number between -60 and 0 into the "LUFS" input.

### How Custom LUFS gain works [​](https://docs.samply.app/#how-custom-lufs-gain-works)

If loudness matching is on and you are using a supported browser, then we attempt to match a target LUFS without introducing any clipping by applying gain according to the following rules:

- Target LUFS must be between -60 and 0 LUFS
- If the target LUFS is less than the original LUFS, then apply _negative gain_ until the target LUFS is reached
- If the target LUFS is greater than the original LUFS, then apply _positive gain_ until the target LUFS is reached or there is 1 dB of headroom left based on the original TP (whichever is less).

**Example:** You upload a track with -18 LUFS and -4 TP, and you set the target LUFS to -14 LUFS. In this case, Samply will apply 3 dB of positive gain, resulting in -15 LUFS and -1 TP.

These rules ensure that Samply's loudness matching will never introduce clipping into your tracks. Note that these rules do not guarantee that all tracks will have at least 1 dB of headroom; if you upload a track with a TP of 0 dB, then we will never apply positive gain to it.

### Browser support & caveats [​](https://docs.samply.app/#browser-support-caveats)

Loudness matching is fully supported on most modern browsers with some exceptions.

On Safari, HLS streaming does not work with the Web Audio API due to a known [WebKit bug](https://bugs.webkit.org/show_bug.cgi?id=180696). To circumvent this issue, Samply attempts to directly stream the underlying asset when loudness matching is enabled on Safari version 15.6 or higher.

Furthermore, since the Web Audio context gets suspended on iOS devices when the screen is locked, enabling loudness matching will cause playback to stop when the client's screen is locked.