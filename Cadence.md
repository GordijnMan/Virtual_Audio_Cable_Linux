# Cadence Method
* **JACK Audio Connection Kit takes exclusive control of your audio devices.**
* This means that this method will not work if you need to use the configured devices for other purposes than JACK.
* If you want to record your mic and desktop audio into a seperate Virtual Audio Cable, such as VAC or VoiceMeeter on Windows, THIS is what you are looking for!
* Cadence is an installation suite, and comes with multiple apps:
  1. Catarina: Patchbay, I never use it.
  2. Catia: Patchbay, I never use it.
  3. Claudia: This is what you need.
  
## Claudia
* Claudia makes the other 2 tools redundant; it is a patchbay with session control.
* This means you can configure a virtual audio card for JACK, which you can fully configure.
* This will create a virtual audio channel, and you can route your mic and desktop into this channel.
* You can then save your session, and load this session each time you start Cadence.
* You can even add additional commands, which can be useful for using PulseAudio with Cadence.

### Get it, now
* First, make sure you've updated your kernel to the latest version.
* Unfortunately, KXStudio is not in default repositories, so you'll have to add it.
* If you're on Debian / Ubuntu, you can install it using a package: [kxstudio-repos](https://kx.studio/Repositories).
* Once you have this package, update your sources and get `cadence`.
* When installing `cadence` you will install many dependencies, including `jackd2`.
* For JACK to work correctly, you need Realtime permissions.
* Without Realtime permissions, you cannot achieve a VAC on Linux.

```
# Update software sources
sudo apt-get update

# Update everything, including your kernel
sudo apt-get upgrade

# Install required dependencies if needed
sudo apt-get install apt-transport-https gpgv wget

# Download package file from https://kx.studio/, install
sudo dpkg -i ./kxstudio-repos*.deb

# Install Cadence
sudo apt-get install cadence
```

## Cadence
* Claudia is part of the Cadence suite (KXStudio).
* If you've installed Cadence, you also get JACK and Claudia.
* In Cadence:
  1. Set your **JACK Bridges** to *Bridge Type*: `ALSA -> PulseAudio -> JACK (Plugin)`
  2. Go to 'Configure'
  3. Go to `Configure -> Driver`.
  4. Configure your microphone as Input and Output.
  5. Your microphone can now be used with JACK.
  
## Using Claudia
* From here on out, you need to configure your Studio and save it.
* You can add custom commands at `Application -> Run Custom`.
* These commands (applications) can be executed on command by 'Starting' them.
* Use the run levels to manage the order of execution.
* I recommend using `PulseAudio` commands here, to set your defaults:

```
# Set JACK as the default input device
/usr/bin/pacmd set-default-source jack_in

# Set JACK as the default output device
/usr/bin/pacmd set-default-sink jack_out

# Boost your microphone
/usr/bin/pactl set-source-volume <YOUR MIC>
```

* Unfortunately, JACK ended up not being the solution to my problem.
* That is because JACK took exclusive control of the same device I needed for communications.
* So, I had another go at the [PulseAudio Method](./PulseAudio.md).
