FFmpeg README

FFmpeg is a collection of libraries and tools to process multimedia content such as audio, video, subtitles and related metadata.
Libraries

    libavcodec provides implementation of a wider range of codecs.
    libavformat implements streaming protocols, container formats and basic I/O access.
    libavutil includes hashers, decompressors and miscellaneous utility functions.
    libavfilter provides a mean to alter decoded Audio and Video through chain of filters.
    libavdevice provides an abstraction to access capture and playback devices.
    libswresample implements audio mixing and resampling routines.
    libswscale implements color conversion and scaling routines.

Tools

    ffmpeg is a command line toolbox to manipulate, convert and stream multimedia content.
    ffplay is a minimalistic multimedia player.
    ffprobe is a simple analisys tool to inspect multimedia content.
    Additional small tools such as aviocat, ismindex and qt-faststart.

Documentation

The offline documentation is available in the doc/ directory.

The online documentation is available in the main website and in the wiki.
Examples

Conding examples are available in the doc/example directory.
License

FFmpeg codebase is mainly LGPL-licensed with optional components licensed under GPL. Please refer to the LICENSE file for detailed information.

Notes on Building on Linux:

1.Download and install the NVIDIA NVENC SDK for Windows (Yes, that is correct). Extract the SDK's content, navigate to nvenc-xx.0/samples/nvEncoder/inc and copy the header files therein to /usr/include.

2.Ensure that the NVIDIA CUDA SDK is installed, and copy cuda.h to /usr/include.

3. Download and copy the file D3D9.h to /usr/include

4. Install and configure the MXE cross-compiler from https://github.com/mxe/mxe

You can then run ./configure with your customization options as is deemed necessary.

In my case, I built it with NVENC enabled with the following configuration options on Ubuntu 14.04 LTS:

Option 1: (Builds a 64-bit binary)

./configure --enable-memalign-hack --arch=x86_64 --target-os=mingw32 --cross-prefix=i686-w64-mingw32- --pkg-config=pkg-config --enable-nonfree --enable-gpl --enable-version3 --enable-libmp3lame  --enable-libopus --enable-libtheora --cpu=native  --enable-libnvenc

Option 2: (Builds a 32-bit binary)

./configure --enable-memalign-hack --arch=x86 --target-os=mingw32 --cross-prefix=i686-w64-mingw32- --pkg-config=pkg-config --enable-nonfree --enable-gpl --enable-version3 --enable-libmp3lame  --enable-libopus --enable-libtheora --cpu=native  --enable-libnvenc

Happy building. 

Notes on this build:

1. No libx264 as fallback. Uses libnvenc exclusively. You've been warned ;-)
2. NVENC is for Kepler and Maxwell GPUs ONLY.
3. Note the cross-compile option highlighted in the configure script above. It must NO be omitted. 
