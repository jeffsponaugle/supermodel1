# TRS-80 Supermodel1
## A replacement TRS-80 Model 1 Motherboard, with enhancements, buildable new in 2023.

This project is focused around building a replacement TRS-80 Model 1 motherboard using modern through-hole components available new in 2023.  This work will include the design and building of the motherboard PCB as well as the development of the CPLD code and the firmware to support both OEM and non-OEM ROM images.

This work is Open-Source, Open-Hardware, and free for anyone to use.

### Specifications:

+ Z80 CPU DIP 40, 1-16 MHz software adjustable based on installed oscillator. 

  - With a 28.332MHz oscillator you can get original spec 1.77Mhz operation, and multiples of that.
  - With a 32MHz oscillator you can get 1,2,4,8,16 Mhz operation.

+ 512K SRAM, bankable across all 4 16K regions, write protectable as well.

+ 512K FLASH, bankable across all 4 16K regions, write protectable as well. 

+ 16K of Video memory to support 64x16, 32x16, 80x24 text modes and 512x384 bitmap graphics modes.

+ No interference on video access from the CPU.  Video access from both CPU and video is full speed.

+ 256K of FONT RAM with direct CPU access to allow software fonts (8x16)

+ Compatible exeternal inteface port for original Tandy/RadioShack Expansion Interface

+ Cassette interface

+ Work with original keyboard

+ Video output: NTSC Composite B&W or VGA 640x480.

+ Onboard power regulation from DC input 7-36V.  Switching regulator, 94% efficient.  

### Status as of Oct 4, 2023:

We have completed the design and build of the first prototype PCBs.  The video section was built on a seperate PCB from the main CPU to allow for revisions to the video section if needed... and it turns out to not be an issue.  We were able to get both NTSC composite output and VGA output from the video interface.  


The first prototype PCB has been built and tested!  It works with the Level 2 R/S 1.3 ROMs allowing BASIC execution.  Next up will be testing with a few different variations of the EIs.

Once validation of all of the interconnects and compatibilty a new PCB will be build in the original case form factor.

On the current PCB power usage is about 2.6 watts running VGA output and an 8Mhz CPU.

![First Prototype PCB](SM1_ProtoA.jpeg)

![First Prototype PCB](SM1_ProtoB.jpeg)

### Technical Notes

Video memory is shared between the CPU and the Video Drive Processor (the CPLD that creates video) via a shared timeslot clock.  The timeslot clock runs at 12.5875 Mhz (25.175/2), and each full clock period is allocated to either the CPU or the VDP.  This clock perios is much smaller than the minumum access time needed by either requested so it allows completion of the transaction within to allocated time without adding wait_states or skipping pixels on the output.  This gives access to the video memory from the CPU without the aritifacts present on the original TRS-80 model 1.

Video out is either NTSC B&W Composite *or* VGA 640x480.  Due to resource limiations in the CPLD it is not possible to do both at the same time.  The actual video pixel output is 512x384 using a 8x12 font resource in the default 64x16/32x16 text mode.  Support is also possible for 80x24 using 640x480 using 8x10 font resouces, as well as a bitmap 512x384 direct bit access.  All output is currently B&W only.


(Authors:  Jeff Sponaugle, Neil Bradley)
