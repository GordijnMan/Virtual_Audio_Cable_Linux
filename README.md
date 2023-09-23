# Virtual Audio Cable Linux
## Quick links
* [Cadence](./Cadence.md)
* [PulseAudio](./PulseAudio.md)

## Description
* It took me way too long to fix this, so I made a repository for it. 

### Virtual Audio Cable
* I used [VoiceMeeter](https://vb-audio.com/Voicemeeter/) on Windows to record my stream audio into a virtual microphone.
* VoiceMeeter uses [Virtual Audio Cable](https://vb-audio.com/Cable/index.htm) (VAC) to create a virtual audio card.
* I wanted to achieve something on [Linux Mint](https://linuxmint.com/).

### PulseAudio
* I have tried to achieve such using [PulseAudio](https://www.freedesktop.org/wiki/Software/PulseAudio/) only.
* I created a [PulseAudio Method](./PulseAudio.md) to reconstruct the way VAC works on Windows.
* The [PulseAudio Method](./PulseAudio.md) works, but only if the virtual devices are detected by your application.
* That is because for some applications, you need to somehow create a Virtual Audio Card on Linux.

### PulseAudio
* I repeatedly came across the [JACK Audio Connection Kit](https://jackaudio.org/), but I found this very complex to use.
* Eventually I stumbled across [Cadence](https://kx.studio/Applications:Cadence) (KXStudio), a frontend to JACK.
* Cadence turned out to be extremely useful, so I also made a [Cadence Method](./Cadence.md) to try and reconstruct the VAC setup.
* The [Cadence Method](./Cadence.md) works, but only if you aren't intending to communicate with others through the same output.
* That is because this method requires exclusive control of your main audio device.

### So which method is better?
* I recommend using the [PulseAudio Method](./PulseAudio.md) for streaming.
* It doesn't take exclusive control over your audio devices.
* However, you might like the [Cadence Method](./Cadence.md) more if you are a content creator, especially if you are an artist or editor.
*  Use these methods in combination with [Open Broadcaster Software](https://obsproject.com/) (OBS), if you also want to record video or stream.
