+++
title = "Generating Embeddable Terminal Sessions"
date = "2023-01-24T21:11:10-06:00"
author = ""
authorTwitter = "" #do not include @
cover = ""
tags = ["terminal"]
keywords = ["", ""]
description = "Learn how to embed visually appealing terminal sessions on the web."
showFullContent = false
readingTime = false
hideComments = false
color = "" #color from the theme settings
ToC = true
+++

## Overview

There are several tools that allow you to generate image (GIF) or video (WebM, MP4) recordings of a terminal session.

You can then embed these recordings in a blog to illustrate the input and output of a CLI app.

Our ideal tool would:
- Be (relatively) easy to install
- Be configurable via easy to understand text files
- Generate high quality recordings
- Perform typing automatically, so we don't have to re-record if we make a mistake

The tool I found that best meets these criteria is [VHS](https://github.com/charmbracelet/vhs).

## Installing VHS with Homebrew
If you have Homebrew installed, you can install VHS and all its dependencies easily:
```bash
brew install charmbracelet/tap/vhs ffmpeg
brew install ttyd --HEAD
```

## Installing VHS without Homebrew
If you don't have Homebrew installed, you can download the binary releases of VHS and ttyd to somewhere on your `$PATH`, and install FFmpeg using your package manager.
1. Release page for [VHS](https://github.com/charmbracelet/vhs/releases)
2. Release page for [ttyd](https://github.com/tsl0922/ttyd/releases)
3. `sudo dnf install ffmpeg-free` on Fedora or `sudo apt install ffmpeg` on Ubuntu

## Generate an example Tape file
Tape files are just text files that contain commands VHS understands. The file extension `.tape` is optional.

Generate an example Tape file and view it in your editor to see what's possible:
```bash
vhs new example.tape
```

## Record a Tape file
Alternatively, you can record a Tape file of you issuing terminal commands:
```bash
vhs record > myfile.tape
```

If you make any mistakes typing, you can easily fix them in the Tape file.

## Converting a Tape file to an embeddable asset
When you're satisfied with the content of your Tape file, you can generate an embeddable asset like so:
```bash
vhs < myfile.tape
```

If your Tape file doesn't have an `Output` command, VHS defaults to creating the file `out.gif`.

If you want to create a WebM file, you'll need to add a command to your Tape file, e.g. `Output myfile.webm`.

## Quick Tape file reference
```bash
# You can generate multiple assets at once
Output demo.gif
Output demo.webm
Output demo.mp4

# See all available themes with `vhs themes`
Set Theme Dracula

# You can use any font available to your terminal
Set FontFamily "Droid Sans Mono Slashed for Powerline"
Set FontSize 32

# Set the asset dimensions
Set Width 1200
Set Height 600

# Enter your command as text
Type "echo 'Hello, World'"

# Optionally sleep between commands to improve viewability of the recording
Sleep 500ms
Sleep 5s

# Send a special key or control sequence
Enter
Ctrl+C
```

## Example recording
And now for the payoff:

![VHS Example](/vhs-example.gif)
