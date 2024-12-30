# Kludge-Z80

A custom and completely kludged together Z80 project.

Table of Contents:
- [Kludge-Z80](#kludge-z80)
  - [About](#about)
  - [Backplane](#backplane)
  - [Card List](#card-list)
    - [Compact Flash Card](#compact-flash-card)
    - [IDE Card](#ide-card)
    - [CPU Card](#cpu-card)
    - [Memory/RAM Card](#memoryram-card)
    - [Network Card](#network-card)
    - [Protoboard Card](#protoboard-card)
    - [PS/2 Card](#ps2-card)
    - [Real-time Clock Card](#real-time-clock-card)
    - [Serial Card](#serial-card)
    - [Sound Card](#sound-card)
    - [Video Card](#video-card)
  - [Bill of Materials](#bill-of-materials)


## About
I've been working on this project off and on since 2017 or, though it was mostly off until recently!
I've designed all of the hardware from scratch, though I'm totally new to this and have no idea what I'm doing.
That's why the project is called Kludge :)

## Backplane
The backplane is a 12-slot board with a full breakout of the Z80 bus. It also has a few spare pins on the bus for future use as well.

I wanted this backplane to be "motherboard-like". At first I was even going to put the CPU and ROM directly on the board! But to make it "motherboard-like" I designed it with status lights (with a breakout too in case I ever put this in a case and want case lights), the reset button on-board, and address decoding on-board as well.

I have designed it to support 5V at 2A load (actually has 3A rated power components!) with a big chunky sliding power switch. This should allow the use of hard disks in the future if they are 5V-only.

NOTE: Because my backplane board length is so long AND the system clock is supplied on the bus directly, I worry about signal reflections. So the backplane features an active termination on-board that holds all of the signals at 2.7V in a push-pull arrangement. 

## Card List
### Compact Flash Card
Compact flash actually has an 8-bit mode built into the spec, which makes interfacing it with vintage 8-bit CPUs pretty easy.

However, in the case of the Z80 the I/O timing differences between the CF and Z80 CPU don't line up perfectly. If you don't account for this in your design you will encounter a decent amount of compact flash cards that will refuse to work, especially newer and faster cards.

The solution is to properly delay the Z80 timings to fit the compact flash true IDE spec.

Someone a lot smarter than me named Tadeusz Pycio came up with a delay circuit to fix this issue.

You can find his blog about it [here](http://www.vtsys.pl/interface-compact-flash/). If you want to read it in English you will need to enter it into google translate though. Google Translate does an excellent job though and its very understandable!

After implementing his circuit into my design I haven't came across a single compact flash card that wouldn't work.

### IDE Card
This is basically the compact flash card circuit but with an 40-pin IDE port instead of compact flash port.

### CPU Card
This is just simply the Z80 CPU broken out onto the bus. There are some pull-ups for the various control signals. It is running off of a 10 MHz oscillator.

I originally designed the RTC circuit to be included but it took up almost all the space on the board and over crowded the CPU and wasn't aesthetically pleasing.

### Memory/RAM Card
This card holds the RAM and EEPROM chips. RAM is bank switched using I/O and also includes the option to totally deactivate the ROM after boot (useful if you are loading a binary on boot from elsewhere).

I adapted some of John's banking and shadow select circuitry into my own.
His documentation and videos have been incredibly useful.

You can visit his awesome Z80 Retro! project [here](https://github.com/Z80-Retro/2063-Z80).

### Network Card
This really should be called "Fast SPI Card" because it's just a parallel
to SPI interface with a header. This circuit was very tricky to build and
I referenced a LOT of other similar builds to piece it together.

### Protoboard Card
A card used to prototype circuits with the Kludge bus.

It's just a 38 x 32 array of 2.54mm spaced pin holes for prototyping.

Why 38 x 32? Because its as much as I could fit in a 100mm x 100mm board to save fab costs :D

### PS/2 Card
This card granted support for both a mouse and keyboard.
It uses a HT6542B to handle all of the PS/2 communication and timing.

### Real-time Clock Card
Like the network card, this is just an SPI circuit as well but the 
RTC IC is embedded on board and this runs a LOT slower than the network card circuit does.

### Serial Card
This card has a single 16550DN UART on-board for serial communication.

### Sound Card
This is a sound card built around the class AY-3-8910.

I am looking to add a second chip in V2 for 3 channel stereo output.

### Video Card
This is centered around an Upduino v3.1 to drive a VGA display. 
The Upduino uses a Lattice iCE40 UP5K UG48 FPGA.
The verilog code for this is available in its own dedicated repo.

## Bill of Materials
The list is pretty large for this whole project. I will compile it and update this later.