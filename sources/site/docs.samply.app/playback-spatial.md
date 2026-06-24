# Source: https://docs.samply.app/playback-spatial.html

# Spatial audio [​](https://docs.samply.app/#spatial-audio)

_In this article, we use the term "spatial audio" to refer to a broad set of new technologies that offer an immersive listening experience by positioning objects in 3D space._

Apple and Dolby have partnered to deliver the immersive listening experiences of [Dolby Atmos](https://www.dolby.com/technologies/dolby-atmos/#gref) on Apple products. These new features are deeply integrated into Apple's hardware, meaning that it's not just Apple Music users that benefit, but anyone using Apple products.

As consumers are enjoying these new features, audio professionals are faced with the challenge of accommodating spatial audio into their existing workflows, which are often optimized for stereo. Samply aims to serve those looking to add spatial audio into their workflow by extending the platform to support audio files with spatial audio.

## Listening to spatial audio on Samply [​](https://docs.samply.app/#listening-to-spatial-audio-on-samply)

In order to listen to spatial audio on Samply, you must satisfy the following prerequisites:

### Upload a supported format [​](https://docs.samply.app/#upload-a-supported-format)

Dolby [recommends](https://professionalsupport.dolby.com/s/article/How-do-I-QC-my-Dolby-Atmos-mix?language=en_US) using the Dolby Atmos Renderer to export MP4 files for quality control (QC) purposes. By default, the MP4 files exported from the Dolby Atmos Renderer contain a blank h.264 video stream and a multichannel DD+JOC audio stream.

**Samply only supports the MP4 files exported from the Atmos Renderer.**

### Listen on a supported device [​](https://docs.samply.app/#listen-on-a-supported-device)

Based on [support tables](https://developer.dolby.com/platforms/apple/ios/device-support/) provided by Dolby, the following devices with the latest operating systems support spatial audio playback:

1. The built-in speakers on an iPhone 7 or later, or on one of these iPad models:
 - iPad Pro 12.9‑inch (3rd generation) and later
 - iPad Pro 11‑inch
 - iPad Air (3rd generation) and later
 - iPad (6th generation) and later
 - iPad mini (5th generation) and later
2. iOS or iPadOS 15.1 or later
3. The built-in speakers on a [Mac computer with Apple silicon](https://support.apple.com/kb/HT211814)
4. Apple TV 4K with tvOS 15 or later

At this point, you can listen to your spatial audio mixes on Samply using the iOS app or Safari. On macOS, you must also be using Samply within Safari (Chrome does not natively support Atmos MP4 files).

If a spatial audio file in Samply is opened in an unsupported browser or device, then a stereo mixdown will be played and the following informative banner will tell the user to open in Safari if they want to listen to the full Atmos experience:

![Atmos banner](https://docs.samply.app/img/playback-atmos-banner.png)

### Upgrade to Samply Pro [​](https://docs.samply.app/#upgrade-to-samply-pro)

If you would like to share spatial audio in a player similar to other audio files (timecoded comments, track sequencing, etc.), then a Samply Pro account is required before uploading your MP4 files. Note that you can still share MP4 files in players without Samply Pro, but they will be treated as any other video MP4 file.

If you are looking to test this feature before purchasing, we offer a 10-day free trial of Samply Pro. The [10-day free trial](https://samply.app/pricing) will be applied at checkout.