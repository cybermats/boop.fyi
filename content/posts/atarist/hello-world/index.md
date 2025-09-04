+++ 
draft = true
date = 2025-09-03T22:04:56+02:00
title = "Graphical Hello World"
description = "A very simple, graphical program for the Atari ST"
slug = ""
authors = []
tags = ["68000", "Atari ST"]
categories = []
externalLink = ""
series = []
+++

Let's write a minimal assembler program which cycles the background color. 

To understand this code we have to go through a few things:

* What registers are there in the 68000
* Where the stack is located
* How you move (or load) data into registers
* How to call a software interrupt
* How to branch

### Registers ###
We have 8 data registers (d0-d7), and 8 address register
(a0-a7). These are all general-purpose 32 bit registers.

Then we have the program counter (PC) and the condition code register
(CCR).

All registers can be used for bit fields, byte (8 bits), word (16
bits), long-word (32 bits) and quad-word (64 bits) operations. 

### Stack  ###
To simplify things at the start the stack pointer is in the `a7`
register. There are actually two types of stack pointers, "User Stack
Pointer" and "Supervisor Stack Pointer", but we will not go into that
right now.


### Load data ###
Loading, or moving, data in and out of registers is done with the
`move` operation. You will also have to specify the width of the data
you are moving as well, which is done using a suffix to the
mnemonic. For example, `move.l #$ff8240,a0` moves a long-word (32
bits) value of $ff8240 into the `a0` register, and `move.w #$000,(a0)`
moves a word (16 bits) into the memory location that `a0` points at.

### Software interrupts ###
To call a software interrupt you use the `trap` operator. Calling
routines from GEMDOS is done this way.

### Branching ###
The most basic branching is the Branch Always operator, which is given
a displacement. This can be 8 bit or 16 bits long allowing for shorter
or longer jumps. The shorter version is using the suffix `.s` for
single-precision. In this example we're using `bra.s loop` to jump to
a loop that is close by.

The code is available in a [git repo](https://github.com/cybermats/atarist-tutorial/tree/main/part01).



``` nasm
	;; A very simple example Atari ST program

	;; Put the CPU in the "Supervisor" mode by calling the GEMDOS
	;; routine "Super", which you do by calling trap with argument $20.
	
	move.l #0,-(a7)		; Argument to "Super", which tells it to switch 
		                ; to "Supervisor" mode.
	move.w #$20,-(a7)	; $20 is the routine number for "Super".
	trap #1 		    ; Call GEMDOS

	;; Now we're in supervisor mode, which gives us full control
	;; of the machine.
				
	move.l #$ff8240,a0	; Store the address of the background
				        ; color register in a0

	move.w #$000,(a0) 	; Set the background to black

loop:
	add.w #$1111,(a0) 	; Circle the colors
	nop 			    ; Wait a short while
	bra.s loop 		    ; Loop forever
```

Let's break it down!

The 68000 has two modes, User and Supervisor. The User Mode limits
what you can do in order to give an OS more control and make it harder
for user programs to crash the computer. To get out of it and into the
"Supervisor Mode" we can use a GEMDOS System Function called
"[Super](https://freemint.github.io/tos.hyp/en/gemdos_system.html#Super)".

GEMDOS Functions are invoked through Software Traps, specifically
`trap #1`. The parameters to the functions are given in inverse order
on the stack, so the last argument is stored as the first on the
stack. The last thing added to the stack is the GEMDOS Function
number.

Sending `0` as argument will ask `super` to switch between "User" and
"Supervisor", and we put that on the stack, followed by the opcode for
`super` which is `$20` hex. Finally we issue `trap #1` to call GEMDOS.


``` nasm
	move.l #0,-(a7)
	move.l #$20,-(a7)
	trap #1
```

# References #
* [68000 Reference Manual](https://www.nxp.com/docs/en/reference-manual/M68000PRM.pdf)
* [TOS References](https://freemint.github.io/tos.hyp/en/tos_about.html)
* [Atari ST Internals, The authoritative insider's guide](https://www.synacktiv.com/ressources/Atari-ST-Internals.pdf)
