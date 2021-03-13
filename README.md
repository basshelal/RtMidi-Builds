# RtMidi Builds

Builds of [RtMidi](https://github.com/thestk/rtmidi) for various platforms.

These are intended to be used for my port/bindings of RtMidi to Java,
[JRtMidi](https://github.com/basshelal/JRtMidi).

## Supported Platforms/Builds

A build consists of a CPU architecture and API(s) pair.

### Current Builds

* ALSA on x86-64
* ALSA + JACK on x86-64
* ALSA on armhf
* ALSA + JACK on armhf
* ALSA on aarch64
* ALSA + JACK on aarch64

### Future Builds

* CoreMIDI on x86-64
* CoreMIDI + JACK on x86-64
* WinMM on x86-64

## Build method

Download source from 
[RtMidi Releases](https://github.com/thestk/rtmidi/releases)

Run [`buildscript`](./buildscript) in the source directory on:

* a GNU/Linux x86_64 machine for all ALSA builds (including armhf and aarch64)
* a Darwin x86_64 machine for all CoreMIDI builds
* a MinGW x86_64 machine for all WinMM builds