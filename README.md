# Brother P-touch D600 Label Maker

This document details the USB communication trace between a Brother P-touch D600
label maker and the P-touch Editor program.

Upon startup, the program sends `1b 69 58 47`, which seems to be a system status
query command.

The printer responds with `71 02` which is 625 in little endian binary encoding.
This is the length of the next message which comes in 40 byte chunks with the
last one being less - not padded.

The message uses CRLF for newlines.

```ini
<<PRINTER CONFIGURATION>>
[Printer]
FormVer =1.00
Printer =PT-D600
PrintID =6430
SerialNo=D6Z608109
ProgVer =V1.01
BootVer =V1.00
FontVer =V1.00
ColorVer=V1.00
SymVer  =V1.00
EromVer =V0.010
PV      =        1,466
PN      =          202
LC      =            1
BC      =            0
FR      =            0
SB      =            5
NB      =            0
MR      =            0
LL      =            0
AF      =            0
CC      =          236

[Printer Settings]
Auto Power Off =480Minute(s)

[File Memory]
Available =2260char
Files     = 0/99

[Label Collection Memory]
Categories = 0/30

```

The program then sends `1B 69 53` and the printer responds with 32 bytes:

```hex
80 20 42 30 6a 30 00 00 00 00 09 01 00 00 00 00
00 00 00 00 00 00 00 00 01 08 00 00 00 00 00 00
```
