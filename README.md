# Commodore VIC-20 Hardware Projects
Hardware &amp; information for the VIC-20.<br>

## [MFJ-1258 Capacitance Meter](/MFJ-1258/)
By MFJ Enterprises<br>

## [HAMSOFT Cartridge](/HAMSOFT/)
By Kantronics<br>

## [VIKTRAK+ Software & AUTOTRAK Cartridge](/VIKTRAK/)
By K7NH/Neil Hill<br>

## [6560/6561 A/V Breakout Board](/VIC_6560/) - UNTESTED
The VIC's default video output is pretty bad.  I've long wanted to "go back to basics" and see how the output can be improved by, for example, wiring it up as per its original datasheet example circuit.<br>

The first step is to create this breakout board to isolate the A/V signals from the video output stage on the VIC's motherboard.<br>

![3D view of breakout board](/VIC_6560/VIC_AV_Breakout_3D.png)

I hope that it will allow me to see what signals the 6560 outputs natively, then start to build on that.<br>

BTW, yes I know there are boards out there that already do this.  I've not had much luck with the free or paid-for boards, so I want to ... TRY TO ... understand it myself.  Let's see ...

## [6502 to W65C02S Daughterboard](/6502-to-65C02/) - UNTESTED
Unlike the 6522 VIAs that can be directly swapped for modern CMOS 65C22s from WDC, the W65C02S can't be directly swapped - a daughterboard is required to buffer the data bus signals and also handle some other signals/pins that differ.

![3D view of 65C02S daughterboard](/6502-to-65C02/Images/6502-to-65C02S_3D.png)

## [Serial Port Breakout Board for Logic Analysers](/Serial_Breakout_2)
I'm curious how JiffyDOS does its thing so whipped up a simple breakout board for the serial port so I can quickly and very easily connect up my logic analyser to capture the signalling with & without JiffyDOS.<br>

Connect the board to the VIC & the disc drive with a DIN-6, and then a 2x4 Dupont-style cable for the logic analyser.<br>

![Serial breakout 3D](/Serial_Breakout/Serial_Breakout_DIN_3D.png)

# RAM Expansions
Okay, my mind is full of ideas so it's probably a bit confusing with all these different designs.<br>

My original intent/idea was to replace the orignal ten 2114 RAM chips in case they were faulty.  It then grew from there.<br>

The different designs are:
- Original 8KB (BLK0) expansion: Replace the original 5KB plus 3KB expansion, switchable on/off via external switch.  This used a PLD which, in hindsight, is more complication than really needed.
- New 8KB expansion: Replace the PLD with the 74LS138, replicating the original VIC design but intercepting the ~RAM1/2/3 select signals.
- Simpler 8KB expansion: For a full BLK0 we really only need the ~BLK0 select signal so this greatly simplifies design but isn't switchable on/off.
- Full 32KB (BLK0/1/2/3) expansion
- Really Full 40KB (BLK0/1/2/3/5) expansion: Two designs to give the full 32+3KB expansion.  The Rev. A uses SMD and a larger SRAM and is, IMHO, overly complicated.  The Rev. B design is through-hole and piggybacks an 8KB (6264) SRAM on-top of the 32KB (62256) so we don't need to widen the board.

## [Orignal Internal 8KB RAM Expansion](/Internal_8KB/) - TESTED
My attempt to replace the VIC's built in 5KB of RAM (ten 2114 chips) with a single 8KB chip, with an extra 3KB RAM as a free bonus.

![3D view of RAM upgrade board](/Internal_8KB/Images/VIC-20_BLK0_RAM_Expansion.png)

## [New Internal 8KB RAM Expansion](/Internal_8KB_New/) - DESIGN
Removes the PLD and re-uses the 74LS138.

![3D view of RAM upgrade board](/Internal_8KB_New/VIC-20_Internal_8KB_RAM_3D.png)

## [Simpler Internal 8KB RAM Expansion](/Internal_8KB_Simple/) - DESIGN
Just the 8KB for BLK0, nothing else.  As simple as my simple mind can make it.

![3D view of RAM upgrade board](/Internal_8KB_Simple/VIC-20_Internal_8KB_RAM_Simple.png)

## [Internal 32KB RAM Expansion](/Internal_32KB/) - DESIGNED
Let's see if we can make a FAT VIC with a full 32KB internal RAM that can be disabled externally when required.  I've only made the +24KB in BLK1/2/3 switchable ... the 40KB Rev. B has both BLK0 and BLK1/2/3 switchable.<br>

![3D view of RAM upgrade board](/Internal_32KB/VIC-20_Internal_32KB_3D.png)

## [Internal 40KB RAM Expansion](/Internal_40KB/) - DESIGNED
I was asked about 35KB expansion so I've attempted that here.<br>

There's two versions:
- [Rev. A](/Internal_40KB/RevA/): all surface mount because of the number of chips
- [Rev. B](/Internal_40KB/RevB/): a "simpler" version based on the 32KB design (so, thoughhole) with the additional 8KB (6264) piggybacked on top of the 32KB (62256)

![3D view of RAM upgrade board](/Internal_40KB/RevA/VIC-20_Internal_40KB_RAM_RevA_3D.png)

![3D view of RAM upgrade board](/Internal_40KB/RevB/VIC-20_Internal_40KB_RAM_RevB_3D_1.png)
