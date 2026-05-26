# Internal 32KB RAM Expansion
My attempt to create a FAT VIC with a full 32KB internal RAM expansion without need for an external cartridge.<br>

## Status
26-May-2026: complete re-design of my original idea, pending farbication & testing

## Purpose
- Save having to source replacement 2114 chips in case RAM is faulty;
- Upgrade the internal RAM unexpanded 5KB to a full 32KB, but switchable from outside the case depending on software requirements;
- Reduce power consumption/waste heat generation;
- Use as a learning experience to understand how the VIC's memory works and using a PLD;
- 100% reversible, no cutting of tracks required.

## YouTube Videos
- [Simple KiCad For Simple Vintage Computer Hobbyists: Part 5 (VIC-20 RAM Expansion)](https://youtu.be/WQpgBGNAkP0)
- [Commodore VIC-20 Internal RAM Replacement: Part 1](https://youtu.be/0KduuzFBmz8)

## Important Note
This information is provided to you completely free - use at your own risk.<br>
It is assumed that you kind-of know what you're doing - it is tricky removing chips from the VIC-20 motherboard as the top-layer tracks can lift up if there is still solder attached, so please be very careful.<br>
I've been using the Japanese-made ENGINEER SS-03 solder sucker a lot lately and highly recommend it.<br>

## Design
The VIC's memory is allocated in eight 8KB blocks named BLK0 to BLK7.  The RAM is normally found in BLK0 to BLK3.
```
Unexpanded VIC Memory
BLK0
0000   0000 0000 0000 0000 RAM0
03FF   0000 0011 1111 1111

1000   0001 0000 0000 0000 
1FFF   0001 1111 1111 1111 RAM4-7


Expanded VIC Memory
BLK0 (+3KB)
0400    0000 0100 0000 0000 RAM1
07FF    0000 0111 1111 1111

0800    0000 1000 0000 0000 RAM2
0BFF    0000 1011 1111 1111

0C00    0000 1100 0000 0000 RAM3
0FFF    0000 1111 1111 1111

BLK1 (+8KB)
2000    0010 0000 0000 0000
3FFF    0011 1111 1111 1111

BLK2 (+16KB)
4000    0100 0000 0000 0000
5FFF    0101 1111 1111 1111

BLK3 (+24KB)
6000    0110 0000 0000 0000
7FFF    0111 1111 1111 1111
```

[Commodore VIC-20 Memory Map](https://vic20reloaded.com/commodore-vic-20-memory-map/)

The daughterboard is designed to plug in to the VIC's motherboard where two of the original 2114 chips were located - expectation is that all ten 2114 chips are removed, and two replaced with an IC socket. <br>

The two 74LS138 decoders on the VIC motherboard are also removed and replaced with breakouts so the signals can be handled on the expansion daughterboard.<br>

### BLK0 Expansion
In order to fill in the missing 3KB in BLK0 we need to intercept the ~RAM1, ~RAM2 and ~RAM3 select signals and direct them to our RAM.<br>

This is done by relocating the 74LS138 to the expansion daughterboard and using all ~RAMx select signals for our RAM.<br>

### BLK1/2/3 Expansion
We should be able to fill in the BLK1/2/3 RAM by intercepting the associated ~BLK1, ~BLK2 and ~BLK3 select signals from the BLK decoder and using as the select signal for our RAM.<br>

Importantly we want to also be able to disable this additional RAM to allow software designed for the unexpanded/+3KB expanded VIC-20 to work correctly.  This can be done by connecting the ~BLK0/~BLK1/~BLK2 select signals via a multiplexor connected to an external switch that determines if the ~BLK1/2/3 select signals are passed back to the VIC or not.<br>



