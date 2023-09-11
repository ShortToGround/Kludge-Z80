# Overview
This is my Z80 homebrew project. I am a total beginner and I'm learning as I go, but the goal is to create a functional kernel and OS based on a Z80 CPU.
The first goal is to get it working for my specific hardware set, the next goal will is to dynamically scan and load drivers as needed, depending on what "cards" are present on boot.

When I say "functional kernel" I mean a real (as real as you can get with a Z80) kernel. Complete with syscalls and memory management.

Programming wisdom says to write your code first and optimize later. I have no doubts that there are many places my code can be optimized.
I don't have a full grasp of every instruction so I will try to get it running first, then go back and make it faster/better later.

**I couldn't have finished this project without help from the user Erlend_LB6MI at #electronics on libera IRC or the help from the man behind the Zeal 8-Bit computer project.
Check out the Zeal 8-bit computer [here](https://zeal8bit.com). His project is seriously impressive and he even created his own VFS from scratch. His kernel is complete with syscalls and everything. This project is what re-inspired me to finish mine!**

## Current hardware list
I recently switched from LS to HCT ICs for full CMOS Z80 and CF compatiblity.

### CPU/System:
* 1x Z80 CPU - Z84C0010PEG (CMOS)
* 1x Z80/System Clock - ECS-2100AX-100 (10MHz)
* 1x SRAM - CY62256NLL-70PXC (32K)
* 1x EEPROM - AT28C64B-15PU (Unused atm, I'm running everything off of RAM using my rom-uploader program)
* 1x Hex Inverter - SN74AHCT04N
* 1x NAND Gate (Used for some address "decoding")
* 1x OR Gate (Used to combine IOREQ RD/WR into IORD and IOWR. Same for MEMREQ)
* 1x 3-8 Address Decoder - SN74HCT138N
* A crap load of small and medium sized wire
* and a crap load of 104 ceramic capacitors for decoupling (before /u/1Davide on /r/ask_electronics says anything)
UART:
* 1x UART - PC16550DN/NOPB (I have a second one I will probably use for a tape interface one day)
* 1x UART Clock - ECS-100AX-018


### Programming "board"
* 1x Arduino Nano
* 2x Shift Register (Serial In, Parallel Out) - 7SN74HC595N (Wish these were HCT but it seems to work fine)

### Compact Flash:
* CF IDE breakout module
