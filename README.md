# RtMidi Builds

Work in progress...

Builds of [RtMidi](https://github.com/thestk/rtmidi) for multiple platforms.

These are intended to be used for my bindings of RtMidi to Java,
[JRtMidi](https://github.com/basshelal/JRtMidi).

## Supported Platforms/Builds

A build consists of an API(s) and CPU architecture pair.

### Current Builds

#### `x86_64`

* ALSA on `x86-64`
* ALSA + JACK on `x86-64`
* CoreMIDI on `x86-64`
* CoreMIDI + JACK on `x86-64`
* WinMM on `x86-64`

#### `armhf` and `aarch64`

* ALSA on `armhf`
* ALSA + JACK on `armhf`
* ALSA on `aarch64`
* ALSA + JACK on `aarch64`

### *Possible* Future Builds

* CoreMIDI on `aarch64`
* CoreMIDI + JACK on `aarch64`

## Build Method (for reference)

Download source from 
[RtMidi Releases](https://github.com/thestk/rtmidi/releases)

Run [`buildscript`](./buildscript) in the source directory on:

* a GNU/Linux x86_64 machine for all ALSA builds (including `armhf` and `aarch64`, read [GNU/Linux Cross Compiling](#gnulinux-cross-compiling) for full instructions and details)
* a Darwin x86_64 machine for all CoreMIDI builds
* a MSYS2 (with mingw-w64 installed) x86_64 machine for all WinMM builds, see [Windows Prerequisites](#windows-prerequisites) for more info

### GNU/Linux Cross Compiling

To cross compile for GNU/Linux `armhf` and `aarch64` you need some additional steps.

The below steps are for an Ubunutu 20.04 based machine.

1. Add the desired architectures as follows:

    `sudo dpkg --add-architecture armhf`

    `sudo dpkg --add-architecture arm64`

2. Create a new `.list` file in `/etc/apt/sources.list.d`:

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

4. Update `/etc/apt/sources.list` to include your default architecture (if it doesn't already), otherwise apt will try to use your newly added architectures in those sources which may cause errors as it did with me.
   
   Add `[arch=amd64]` **for each line** in `/etc/apt/sources.list` as follows:

    `deb [arch=amd64] http://us.archive.ubuntu.com/ubuntu/ focal main restricted universe multiverse`

5. Run `sudo apt update` and make sure you get no errors

6. Install the required libraries, namely:

    `sudo apt install libasound2-dev:armhf libasound2-dev:arm64 libjack-jackd2-dev:armhf libjack-jackd2-dev:arm64`

7. Install the cross compile tools, if not already installed:

    `sudo apt install g++-8-arm-linux-gnueabihf g++-8-aarch64-linux-gnu`

### Windows Prerequisites

To build for Windows, you need to install some additional software to *"emulate"*
a GNU environment, namely:

1. [`mingw-w64`](http://mingw-w64.org/doku.php) which provides GCC for Windows.
   
   After installation, add the `bin` directory containing `g++` to your
   system `PATH` variable.

2. [`MSYS2`](https://www.msys2.org/) which provides some additional GNU/Linux
   utilities, namely `bash` to run the [`buildscript`](./buildscript).
   
   As before,
   add the directory containing the `bin` directory containing `bash` to 
   your system `PATH` variable.

3. Now you can open a Windows PowerShell terminal and use `bash`, from which,
   you can execute the [`buildscript`](./buildscript) which will then be able
   to call `mingw-w64`'s `g++`


## LICENSE

While this project uses the [MIT License](./LICENSE), [RtMidi is subject to its own license](https://github.com/thestk/rtmidi/blob/master/LICENSE) which is similar to the MIT License, with the added *feature* that modifications be sent to the developer.