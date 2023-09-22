## Create VAC sink
* `pacmd load-module module-null-sink sink_name=VAC`
* `pacmd update-sink-proplist STREAM device.description=Virtual_Output`
* `pacmd update-source-proplist STREAM.monitor device.description=Virtual_Input`
* This does nothing but create a "dummy" device!

## Add DEFAULT audio to VAC
* Check out which device is the DEFAULT
* `pactl list short sinks`
* `pacmd load-module module-combine-sink sink_name=MAIN slaves=<DEFAULT>,VAC`
* We have now created a combined sink which will split the audio to your VAC "dummy" from before

## Add MIC audio to VAC
* Check out which MIC first
* `pactl list short sources`
* `pacmd load-module module-loopback sink=VAC source=<MIC> latency_msec=1` # Add more latency if choppy
* The VAC device is now receiving DEFAULT and MIC audio

## Setting your MAIN and VAC as defaults
* Setting MAIN as default will now send output to DEFAULT and your VAC device
* `pacmd set-default-sink MAIN` # This is your output and it outputs to VAC
* `pacmd set-default-source VAC.monitor` # This is your VAC which will include your MIC and can be used as input
