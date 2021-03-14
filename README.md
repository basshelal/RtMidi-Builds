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

* a GNU/Linux x86_64 machine for all ALSA builds (including armhf and aarch64, read [GNU/Linux Cross Compiling](#gnulinux-cross-compiling)
* a Darwin x86_64 machine for all CoreMIDI builds
* a MinGW x86_64 machine for all WinMM builds

## GNU/Linux Cross Compiling

To cross compile for GNU/Linux `armhf` and `aarch64` you need some additional steps.

The below steps are for an Ubunutu 20.04 based machine.

1. Add the desired architectures as follows:

    `sudo dpkg --add-architecture armhf`

    `sudo dpkg --add-architecture arm64`

2. Create a new .list file in `/etc/apt/sources.list.d`:

    `sudo touch /etc/apt/sources.list.d/arm-cross-compile-sources.list`

3. Add the default sources to that list with the architectures (armhf, arm64) prefixed as such:

    ```
    deb [arch=armhf,arm64] http://ports.ubuntu.com/ focal main restricted
    deb [arch=armhf,arm64] http://ports.ubuntu.com/ focal-updates main restricted
    deb [arch=armhf,arm64] http://ports.ubuntu.com/ focal universe
    deb [arch=armhf,arm64] http://ports.ubuntu.com/ focal-updates universe
    deb [arch=armhf,arm64] http://ports.ubuntu.com/ focal multiverse
    deb [arch=armhf,arm64] http://ports.ubuntu.com/ focal-updates multiverse
    deb [arch=armhf,arm64] http://ports.ubuntu.com/ focal-backports main restricted universe multiverse
    ```

4. Update `/etc/apt/sources.list` to include your default architecture (if it doesn't already), otherwise apt will try to use your newly added architectures in those sources which may cause errors as it did with me. Add `[arch=amd64]` **for each line** in `/etc/apt/sources.list` as follows:

    `deb [arch=amd64] http://us.archive.ubuntu.com/ubuntu/ focal main restricted universe multiverse`

5. Run `sudo apt update` and make sure you get no errors

6. Install the required libraries, namely:

    `sudo apt install libasound2-dev:armhf libasound2-dev:arm64 libjack-jackd2-dev:armhf libjack-jackd2-dev:arm64`

7. Install the cross compile tools, if not already installed:

    `sudo apt install arm-linux-gnueabihf-g++-8 aarch64-linux-gnu-g++-8`