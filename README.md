# RtMidi Builds

Builds of [RtMidi](https://github.com/thestk/rtmidi) for various platforms.

These are intended to be used for my port/bindings of RtMidi to Java,
[JRtMidi](https://github.com/basshelal/JRtMidi).

## Supported Platforms/Builds

A build consists of a CPU architecture and API(s) pair.

### Current Builds

* ALSA on x86-64
* ALSA + JACK on x86-64
* ALSA on aarch64
* ALSA + JACK on aarch64

### Future Builds

* CoreMIDI on x86-64
* CoreMIDI + JACK on x86-64
* WinMM on x86-64

## Build method

Downloaded source from 
[RtMidi Releases](https://github.com/thestk/rtmidi/releases)

### ALSA x86-64 & aarch64

`g++ -Wall -shared -fPIC -D__LINUX_ALSA__ -o librtmidi.so rtmidi_c.cpp rtmidi_c.h RtMidi.cpp RtMidi.h -lasound -lpthread`

### ALSA + JACK x86-64 & aarch64

`g++ -Wall -shared -fPIC -D__LINUX_ALSA__ -D__UNIX_JACK__ -o librtmidi.so rtmidi_c.cpp rtmidi_c.h RtMidi.cpp RtMidi.h -lasound -lpthread -ljack`