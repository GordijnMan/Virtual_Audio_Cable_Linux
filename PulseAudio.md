# PulseAudio Method
## Monitor Devices
* **PulseAudio does NOT take exclusive control of your device.**
* This means you can combine this method with usual configurations.
* This only works if the program you are using detects a DEFAULT set monitor device as input device.
* A monitor device is a channel connected to an output, that monitors it as input.
* Not all applications can detect monitor devices, some only detect virtual sound cards (like JACK).

## Create a VAC channel
* This is your audio stream.
* We will send desktop output and mic input to this channel.
* At this point, this channel still does nothing.

```
# Creating the sink
pacmd load-module module-null-sink sink_name=VAC

# Optional descriptions
pacmd update-sink-proplist STREAM device.description=Virtual_Output
pacmd update-source-proplist STREAM.monitor device.description=Virtual_Input
```

* Notice how the .monitor device can set as DEFAULT.

## Add desktop audio to VAC
* Check the sinks to see which output you'd like to use to hear desktop audio.
* Create a combined sink to split audio to this channel so you can hear it.
* Split the audio to the VAC as well.
* Now, the VAC channel picks up your desktop audio.

```
# Check out which sink you'd like to use
pactl list short sinks

# Create a combined channel where you split the audio to this sink and the VAC
pacmd load-module module-combine-sink sink_name=MAIN slaves=<PREFERRED SINK>,VAC
```

## Add MIC audio to VAC
* Check out which microphone you want to use first.
* Add a loopback channel, where you send your mic input to the VAC.
* Add more latency if the mic sounds choppy.
* Now have a VAC channel with desktop audio and mic input!

```
# Check out which source you'd like to use
pactl list short sources

# Add your source to the VAC, using module-loopback
pacmd load-module module-loopback sink=VAC source=<MIC> latency_msec=1
```

## Setting your MAIN and VAC as DEFAULT
* Setting MAIN as default will now send output to your preferred sink, as well as the VAC device.
* That implies that everything which is being heard will also be recorded.
* That means that communications are looped back into the mic when you are in a two-way stream.
* If you want to prevent looping back certain applications (such as Discord), you can select your preferred output inside this app (instead of the combined MAIN channel).
* This way, only your preferred output hears the communications channel.

```
# Set your MAIN as DEFAULT sink, to your preferred output and VAC
pacmd set-default-sink MAIN

# Set your VAC as DEFAULT source, to your preffered applications that detect .monitor devices
pacmd set-default-source VAC.monitor
```

* You should now be able to record desktop audio with mic input for streaming.
* If configured correctly, any third parties will not hear themselves in your stream.
