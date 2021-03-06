# mircapture

Wrapper for `mirscreencast` and `ffmpeg` to record Unity 8 desktop videos.

## Introduction

Using `mirscreencast` to capture recordings of a Unity 8 desktop session
on my Dell XPS15, which has a UHD display, requires *tens of Gigabytes of
storage per minute* because `mirscreencast` captures the native resolution
using rawvideo at 60fps.

This script automatically determines (hopefully) sane defaults for
`mirscreencast` and directs its output at a
[FIFO](https://en.wikipedia.org/wiki/FIFO_(computing_and_electronics)),
then `ffmpeg` starts real-time encoding from the FIFO using similarly
sane defaults.

The result is that 1080p captures of a Unity 8 desktop session can now
be recorded using *tens of Megabytes per minute*.

## Requirements

Currently `mircapture` has only been tested on Ubuntu (Yakkety Yak) 16.10.

    apt install ffmpeg mir-utils netcat

## Usage

  * Clone this repository:
    * `git clone https://github.com/flexiondotorg/mircapture.git`

  * Log in to a Unity 8 desktop session.

  * Start a Terminal and run the following to capture the desktop:
    * `./mircapture`

  * When you've recorded what you want, return to the terminal where `mircapture` is running and just press `q` to stop `ffmpeg`.
    * `mircapture` will cleanly stop `mirscreencast` for you, no manual `pkill -9` required.
    
  * You'll have a new video in your home directory.
    * Named something like: `Mircapture_1920x1080-30.00fps-16304-0939-50.mp4`

## Changes

Summary of changes.

### 1.0 

  * Initial release.
  * Local capture and encoding only.

## To Do

  * Add options for `-local`, `-tx`, `-rx` so that captures can optionally be streamed to a remote host for encoding.
  * Add optional audio input selection for recording voice overs.
  * Make `mircapture` a snap. May require the utility interface which is not yet available.
