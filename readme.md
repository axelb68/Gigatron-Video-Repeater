# Gigatron Video Repeater

The video repeater is a small add-on board to offload the task of duplicating video lines. Every first line out of four is written to an on-board memory and autonomously transmitted 4 times to the VGA output. By this the Gigatron can always be run in mode 3 and is still producing a screen output without blanked lines.

Main component is the asynchronous FIFO memory chip SN74ACT7201 (or compatible, see below) which is constructed with dual-port SRAM and internal write and read address counters. The read pointer can be reset independently of the write pointer for retransmitting previously read data.

![alt text](https://github.com/TCSPC/Gigatron-Video-Repeater/Asynchronous FIFO.png?raw=true)
