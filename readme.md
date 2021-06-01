# Gigatron Video Repeater

The video repeater is a small add-on board to offload the task of duplicating video lines. Every first line out of four is written to an on-board memory and autonomously transmitted 4 times to the VGA output. By this the Gigatron can always be run in mode 3 and is still producing a screen output without blanked lines.

Main component is the asynchronous FIFO memory chip SN74ACT7201 (or compatible, see below) which is constructed with dual-port SRAM and internal write and read address counters. The read pointer can be reset independently of the write pointer for retransmitting previously read data.

![Working principle of the asynchronous FIFO memory chip](AsynchronousFIFO.png?raw=true)

The first video line (out of four) writes each pixel to the memory which is followed by an immediate read. This is like a flow-through operation
which simply copies the pixel information back to the output.
A retransmit of the complete line is then performed for the next three HSYNC cycles.

![Video Repeater schematics](gtfifo4.png?raw=true)

The schematics of the repeater shows connector U1A which can be plugged into the U37 output register socket of the Gigatron. HSYNC is divided by two JK flipflops (U2). The result is used to initialize the internal read and write pointers of the SN74ACT7201 to the first location. A 74HCT574 latches the memory output and passes it back to connector U1A for VGA output.
By means of a "scanlines on/off" jumper (JP1) the primary line can be blanked-out in order to create a "scanline look" similar to mode 1 of the Gigatron.

![Assembled repeater](VideoRepeater.jpg?raw=true)

So far I tested the board with different clones/extensions of the SN74ACT7201. IDT7201-15, IDT7202-25, and QS7204-15 worked fine.
The picture shows a mixture of 74F, 74ACT, and 74LS components which is not important, however. It is sufficient to use the HCT versions or even LS for the flipflops and the logic.
