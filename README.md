# Virtual Audio Cable Linux
* It took me way too long to fix this, so I made a repository for it. 
* I used [VoiceMeeter](https://vb-audio.com/Voicemeeter/) on Windows to record my stream audio into a virtual microphone.
* VoiceMeeter uses [Virtual Audio Cable](https://vb-audio.com/Cable/index.htm) (VAC) to create a virtual audio card.
* I wanted to achieve something on [Linux Mint](https://linuxmint.com/).
* I have tried to achieve such using [PulseAudio](https://www.freedesktop.org/wiki/Software/PulseAudio/) only.
* The PulseAudio method came close, but the virtual devices were not detected by my applications.
* That is because I needed to somehow create a Virtual Audio Card on Linux.
* I was mistaken to think PulseAudio's Sink Monitors or Sources would suffice.
* I repeatedly came acress the [JACK Audio Connection Kit](https://jackaudio.org/), but I found this very complex to use.
* Eventually I stumbled across [Cadence](https://kx.studio/Applications:Cadence) (KXStudio).
* Cadence eventually turned out to be exactly what I was looking for.
* I highly recommend Cadence for streamers and content creators, in combination with [Open Broadcaster Software](https://obsproject.com/) (OBS)
* Both tools are not easy to use and will require some tinkering or customization.
