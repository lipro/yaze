yaze - Yet Another Z80 Emulator
===============================

Yaze is a Z80 and CP/M emulator designed to run on Unix systems.

The package consists of an instruction set simulator, a CP/M-2.2
bios written in C which runs on the Unix host, a monitor which
loads CP/M into the simulated processor's ram and makes Unix
directories or files look like CP/M disks, and a separate program
(`cdm`) which creates and manipulates CP/M disk images for use with
`yaze`.

Yaze emulates all documented and most undocumented Z80 instructions
and flag bits.  A test program is included in the package which
compares machine states before and after execution of every
instruction against results from a real Z80.  Yaze is independent
of the host machine architecture and instruction set, written in
ANSI standard C, and is provided with full source code under the
GNU General Public License.  It supports CP/M disk geometries as
images in Unix files or as read-only disks constructed on-the-fly.
These disks are indistinguishable from real disks for even the most
inquisitive, low-level CP/M programs and can be mounted and
unmounted at will during emulation.

## Compilation

### Requirements

You will need an ANSI standard C compiler, prefered is the GNU CC.
Yaze was developed under SunOS5 and was briefly tried it under Linux
and FreeBSD.  You will have to do some hacking if your system does not
support the termios tty interface, for example bare Windows machines
or the MinGW build and runtime environment.

### Get the Code

```bash
git clone https://github.com/lipro-cpm4l/yaze.git
cd yaze
```

### Build the binary and execute

```bash
make all
echo -en "DIR\nSYS QUIT\n" | ./yaze -v
```
> ```
> Yet Another Z80 Emulator version 1.14, Copyright 1995,1998 Frank D. Cringle.
> yaze comes with ABSOLUTELY NO WARRANTY; for details
> see the file "COPYING" in the distribution directory.
>
> Running 'yaze.boot'
> bootfile:     yaze.boot
> startup file: .yazerc
> basepage:     e4
> ccp_base:     e400
> bdos_base:    ec00
> bios_base:    fa00
> bios_top:     fa66
> dptable:      fd90
> dirbuf:       ff80
>
> A>DIR
> ZEXDOC  .Z80  |  PRELIM  .COM  |  ZEXDOC  .COM  |  SAVAGE  .COM
> ZEXLAX  .PL   |  ZEXALL  .Z80  |  PRELIM  .Z80  |  SYS     .AZM
> ZASM          |  TIMEX   .COM  |  SYS     .COM  |  SAVAGE  .PAS
> ZEXALL  .COM
> A>SYS QUIT
> ```

## Execute test programs

First of all, start the emulator:

```bash
./yaze 
```
<details>
  <summary>Click to expand and see results!</summary>

  ```
  Yet Another Z80 Emulator version 1.14, Copyright 1995,1998 Frank D. Cringle.
  yaze comes with ABSOLUTELY NO WARRANTY; for details
  see the file "COPYING" in the distribution directory.
 
  Running 'yaze.boot'
 
  A> _
  ```
</details>

## Documented Z80 instructions

Exit the emulator with the SYS command on end of test session:

```
ZEXDOC
SYS QUIT
```
<details>
  <summary>Click to expand and see results!</summary>

  ```
  Z80 instruction exerciser
  <adc,sbc> hl,<bc,de,hl,sp>....  OK
  add hl,<bc,de,hl,sp>..........  OK
  add ix,<bc,de,ix,sp>..........  OK
  add iy,<bc,de,iy,sp>..........  OK
  aluop a,nn....................  OK
  aluop a,<b,c,d,e,h,l,(hl),a>..  OK
  aluop a,<ixh,ixl,iyh,iyl>.....  OK
  aluop a,(<ix,iy>+1)...........  OK
  bit n,(<ix,iy>+1).............  OK
  bit n,<b,c,d,e,h,l,(hl),a>....  OK
  cpd<r>........................  OK
  cpi<r>........................  OK
  <daa,cpl,scf,ccf>.............  OK
  <inc,dec> a...................  OK
  <inc,dec> b...................  OK
  <inc,dec> bc..................  OK
  <inc,dec> c...................  OK
  <inc,dec> d...................  OK
  <inc,dec> de..................  OK
  <inc,dec> e...................  OK
  <inc,dec> h...................  OK
  <inc,dec> hl..................  OK
  <inc,dec> ix..................  OK
  <inc,dec> iy..................  OK
  <inc,dec> l...................  OK
  <inc,dec> (hl)................  OK
  <inc,dec> sp..................  OK
  <inc,dec> (<ix,iy>+1).........  OK
  <inc,dec> ixh.................  OK
  <inc,dec> ixl.................  OK
  <inc,dec> iyh.................  OK
  <inc,dec> iyl.................  OK
  ld <bc,de>,(nnnn).............  OK
  ld hl,(nnnn)..................  OK
  ld sp,(nnnn)..................  OK
  ld <ix,iy>,(nnnn).............  OK
  ld (nnnn),<bc,de>.............  OK
  ld (nnnn),hl..................  OK
  ld (nnnn),sp..................  OK
  ld (nnnn),<ix,iy>.............  OK
  ld <bc,de,hl,sp>,nnnn.........  OK
  ld <ix,iy>,nnnn...............  OK
  ld a,<(bc),(de)>..............  OK
  ld <b,c,d,e,h,l,(hl),a>,nn....  OK
  ld (<ix,iy>+1),nn.............  OK
  ld <b,c,d,e>,(<ix,iy>+1)......  OK
  ld <h,l>,(<ix,iy>+1)..........  OK
  ld a,(<ix,iy>+1)..............  OK
  ld <ixh,ixl,iyh,iyl>,nn.......  OK
  ld <bcdehla>,<bcdehla>........  OK
  ld <bcdexya>,<bcdexya>........  OK
  ld a,(nnnn) / ld (nnnn),a.....  OK
  ldd<r> (1)....................  OK
  ldd<r> (2)....................  OK
  ldi<r> (1)....................  OK
  ldi<r> (2)....................  OK
  neg...........................  OK
  <rrd,rld>.....................  OK
  <rlca,rrca,rla,rra>...........  OK
  shf/rot (<ix,iy>+1)...........  OK
  shf/rot <b,c,d,e,h,l,(hl),a>..  OK
  <set,res> n,<bcdehl(hl)a>.....  OK
  <set,res> n,(<ix,iy>+1).......  OK
  ld (<ix,iy>+1),<b,c,d,e>......  OK
  ld (<ix,iy>+1),<h,l>..........  OK
  ld (<ix,iy>+1),a..............  OK
  ld (<bc,de>),a................  OK
  Tests complete
  A> _
  ```
</details>

## Undocumented Z80 instructions

Exit the emulator with the SYS command on end of test session:

```
ZEXALL
SYS QUIT
```
<details>
  <summary>Click to expand and see results!</summary>

  ```
  Z80 instruction exerciser
  <adc,sbc> hl,<bc,de,hl,sp>....  OK
  add hl,<bc,de,hl,sp>..........  OK
  add ix,<bc,de,ix,sp>..........  OK
  add iy,<bc,de,iy,sp>..........  OK
  aluop a,nn....................  OK
  aluop a,<b,c,d,e,h,l,(hl),a>..  OK
  aluop a,<ixh,ixl,iyh,iyl>.....  OK
  aluop a,(<ix,iy>+1)...........  OK
  bit n,(<ix,iy>+1).............  OK
  bit n,<b,c,d,e,h,l,(hl),a>....  OK
  cpd<r>........................  OK
  cpi<r>........................  OK
  <daa,cpl,scf,ccf>.............  OK
  <inc,dec> a...................  OK
  <inc,dec> b...................  OK
  <inc,dec> bc..................  OK
  <inc,dec> c...................  OK
  <inc,dec> d...................  OK
  <inc,dec> de..................  OK
  <inc,dec> e...................  OK
  <inc,dec> h...................  OK
  <inc,dec> hl..................  OK
  <inc,dec> ix..................  OK
  <inc,dec> iy..................  OK
  <inc,dec> l...................  OK
  <inc,dec> (hl)................  OK
  <inc,dec> sp..................  OK
  <inc,dec> (<ix,iy>+1).........  OK
  <inc,dec> ixh.................  OK
  <inc,dec> ixl.................  OK
  <inc,dec> iyh.................  OK
  <inc,dec> iyl.................  OK
  ld <bc,de>,(nnnn).............  OK
  ld hl,(nnnn)..................  OK
  ld sp,(nnnn)..................  OK
  ld <ix,iy>,(nnnn).............  OK
  ld (nnnn),<bc,de>.............  OK
  ld (nnnn),hl..................  OK
  ld (nnnn),sp..................  OK
  ld (nnnn),<ix,iy>.............  OK
  ld <bc,de,hl,sp>,nnnn.........  OK
  ld <ix,iy>,nnnn...............  OK
  ld a,<(bc),(de)>..............  OK
  ld <b,c,d,e,h,l,(hl),a>,nn....  OK
  ld (<ix,iy>+1),nn.............  OK
  ld <b,c,d,e>,(<ix,iy>+1)......  OK
  ld <h,l>,(<ix,iy>+1)..........  OK
  ld a,(<ix,iy>+1)..............  OK
  ld <ixh,ixl,iyh,iyl>,nn.......  OK
  ld <bcdehla>,<bcdehla>........  OK
  ld <bcdexya>,<bcdexya>........  OK
  ld a,(nnnn) / ld (nnnn),a.....  OK
  ldd<r> (1)....................  OK
  ldd<r> (2)....................  OK
  ldi<r> (1)....................  OK
  ldi<r> (2)....................  OK
  neg...........................  OK
  <rrd,rld>.....................  OK
  <rlca,rrca,rla,rra>...........  OK
  shf/rot (<ix,iy>+1)...........  OK
  shf/rot <b,c,d,e,h,l,(hl),a>..  OK
  <set,res> n,<bcdehl(hl)a>.....  OK
  <set,res> n,(<ix,iy>+1).......  OK
  ld (<ix,iy>+1),<b,c,d,e>......  OK
  ld (<ix,iy>+1),<h,l>..........  OK
  ld (<ix,iy>+1),a..............  OK
  ld (<bc,de>),a................  OK
  Tests complete
  A> _
  ```
</details>

---

This is an unofficial fork!
===========================

Original written by Frank D. Cringle <fdc@cliwe.ping.de> and
distributed under the GNU General Public License version 2.

*Primary-site*: ftp://ftp.ping.de/pub/misc/emulators/

**Various trademarks are the property of various organisations.**
