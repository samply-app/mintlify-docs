# Source: https://docs.samply.app/playback-quality.html

# Audio Quality & Playback [​](https://docs.samply.app/#audio-quality-playback)

Samply's audio playback engine is engineered to deliver the highest quality audio to the widest possible set of devices. In addition, it allows you to set the audio quality for listeners, giving you more control over what your clients hear.

### Uncompressed Stereo [​](https://docs.samply.app/#uncompressed-stereo)

When a typical uncompressed audio file (e.g. WAV) is uploaded to Samply, different variants are created for streaming purposes, including:

1. FLAC (Original bit depth and sample rate)
2. High quality AAC (256 kbps)
3. Medium quality AAC (128 kbps)

The AAC variants are combined for "Adaptive" bitrate streaming, and the FLAC variant is used for "Lossless" streaming.

> Note: Since the FLAC variant is at the original bit depth and sample rate, the "Lossless" quality will deliver the exact same waveform data in the original WAV file to the client.

### Compressed Stereo [​](https://docs.samply.app/#compressed-stereo)

When a compressed audio file (e.g. MP3) is uploaded to Samply, the FLAC variant is not created since the source itself is not lossless. The bitrate of our AAC variant is typically higher than the bitrate of compressed audio files uploaded to Samply, so any losses due to transcoding are minimal.

> Note: If you need Lossless streaming for a compressed audio file, then you can convert the compressed file to an uncompressed WAV before uploading it to Samply.

### Atmos MP4s [​](https://docs.samply.app/#atmos-mp4s)

When a [Dolby Atmos MP4](https://professionalsupport.dolby.com/s/article/How-do-I-QC-my-Dolby-Atmos-mix?language=en_US) is uploaded to Samply, the original MP4 file will be streamed to the client on supported devices (Safari). The stereo AAC variants are also made as a fallback for devices without Atmos support, but a warning message is presented to the user in this case.

### ADM files [​](https://docs.samply.app/#adm-files)

Samply has partnered with Dolby to provide official ADM support for Dolby Atmos.

When an ADM WAV file is upload to Samply, the file is processed using Dolby's Audio Encoder to produce an Atmos MP4 file for streaming. Once the Atmos MP4 file is created, the same variants are created as above.

## Lossless [​](https://docs.samply.app/#lossless)

There are 3 different places you can configure lossless audio playback. In your [audio preferences](https://samply.app/preferences), you can set the default audio quality for the specific device you are listening on, which will not affect any other device.

If you're on our Pro tier, you can set the default audio quality of your project in the [project options](https://docs.samply.app/./sharing.html#link-options). This preference will override the listener's default audio quality set on their device.

Finally, in the project link itself, any listener can change the audio quality by clicking the Audio Options button. This will override any other defaults, but will only apply to that specific device and project, and it will be reset upon reloading the page.

### Exceptions [​](https://docs.samply.app/#exceptions)

In some scenarios, lossless playback is not an option, either because it is not supported in the browser or the source files themselves are lossy (as mentioned previously). Most of the time, if lossless audio quality cannot be enabled, it is because one of the following file types exists in the player which are lossy:

- .mp4
- .m4a
- .mp3
- .aac

Additionally, the below browsers do not support lossless audio quality:

- iOS Chrome
- iOS Instagram in-app browser
- iOS Safari major version 13 or below