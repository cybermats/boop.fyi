+++ 
draft = true
date = 2025-09-03T21:08:31+02:00
title = "Getting started with Atari ST and 68000"
description = "How to get started setting up a development environment for the Atari ST and the 68000 CPU"
slug = ""
authors = []
tags = ["68000", "Atari ST"]
categories = []
externalLink = ""
series = []
+++

I have previously done some coding for the 8bit
[Z80](http://www.z80.info/) processor and wanted to revisit another
old classic, the [Atari ST](https://en.wikipedia.org/wiki/Atari_ST)
system. I know the Z80 CPU pretty well and were looking for
documentation on how to break into the 68000 world. The stuff I found
was either a bit old or was primarily aimed at beginners with no prior
knowledge of 8 bit or 16 bit CPUs and/or assembler.

I decided to try to document my journey learning the Atari ST
system. The first goal is to get a Hello World program running, and
then try to get some graphics working. This means that it wont be
limited to the 68000 world only, but also include
[TOS](https://en.wikipedia.org/wiki/Atari_TOS) and
[GEM](https://en.wikipedia.org/wiki/GEM_(desktop_environment))
programming where needed.

What makes me fascinated with these old machines is that a single
person can understand the entire system in much more details than
what's possible on a modern machine. This in turn influences how I
wish to interact with the machine, which is writing code in assembly,
instead of in C, Pascal, Basic or other more high level languages.

# Where to run the stuff #

Unless you have an Atari laying around since you were young, you can
easily find one on ebay or similar sites. Occasionally you can find
them in thrift stores. 

## Monitors ##

Monitors are also available but they are not as
common. The Atari was often plugged in to a TV back in the days, which
is something that can be done today too. Unfortunately the image
quality is pretty poor.

The alternative is to either solder your own Atari -> VGA adapter, or
buy one online. There are plenty of options out there, just google for
"atari st vga adapter" or something similar. The signal coming out of
the Atari is unfortunately a pretty non-standard version, 15kHz, and
it's not supported by all monitors. To know which works, there are
plenty of sites listing which monitors that should work,
<http://15khz.wikidot.com/> and <https://15khz.net/> to name a few.

## Floppys and Hard Drives ##

Something about
* Gotek
* UltraSatan etc



## Emulators ##
An alternative to hardware is to run an emulator. There are a few good
ones, most notably is [Hatari](https://www.hatari-emu.org/). This
will also make it faster to test out your cross compilated binaries,
where you can easily set up a shared drive instead of copying the
files to an SD card for transfer to a Atari ST machine.

# Development Environment #

Now we have a full system to run our things on. Let's look at what's
needed to start coding. The tutorial I have been following and which I here intend 
to add to, is the blog by [Steven Tattersall](http://clarets.org/steve/tutorials/getting_started_with_st_coding.html). He lists emulators, assemblers and other tools.

The assembler that I will use in this series is [vasm](http://www.compilers.de/vasm.html), since I have positive experience from using it for the Z80. 

Which text editor doesn't much matter. As Steven mentions on the post I linked, most modern text editors have support for syntax highlighting for assembler in general, and the 68000 in particular. Be that Visual Studio Code, Emacs, vim or Sublime Text.

# Prerequisites #

These tutorials assumes that you have a basic understanding of how
CPUs work. For example, you know what a register is, how stacks works,
and that we have different addressing modes. You are not expected to
know anything about the 68000, or how the memory registers are laid
out in the Atari ST. That's what we will explore together.

With this we should be ready to start learning! Continued in the next post.
