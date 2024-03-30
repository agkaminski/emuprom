# emuprom
DIY ATmega8 based 27C256 EEPROM emulator. Human accessible UART interface
(19200N1, CH340 on USB C).

# Target connection

Via ribbon cable with DIP-28 adapter. Uses 40 pin IDC connector, but only 28
pins are used. Target power state detection is supported (external bus is
resistant to high-z state).

Adapter pictures and details TBD.

# UART interface

Available via USB C UART port, 19200 baud, no parity, 1 stop bit. Interface is
human friendly, but also easy to script. Available commands:

- ? - help
- ! - claim bus, memory edit, assert /RST\n");
- . - release bus, deassert /RST\n");
- @ - set address mode\n");
- # - set data mode\n");
- = - dump 256 bytes @addres\n");
- t - memory test\n");
- + - echo on\n");
- t- - echo off\n");
- s - clear memory (all 0xff)\n");
- r - reset target (pulse /RST)\n");

Example sequence with comments:
- - - echo disable,
- ! - claims the bus,
- @0000 - sets address to zero,
- # - selects data mode,
- 0102030405060708 - 8 bytes are written at address 0,
- . - release the bus and start the target,
- + - enable echo.

Or all at once: -!@0000#0102030405060708.+

# Uploading FW

avr-gcc, avr-libc and avrdude are needed.

- make (build FW),
- make fuse (set fuses to set internal RC @8MHz),
- make install (upload FW).

# Pictures

This a picture of rev A with fixed applied in rev B.

<img src="img/top.jpeg">
