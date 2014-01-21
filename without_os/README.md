# Ajhc code running without OS

## Setup enviroment

Install summon-arm-toolchain.

```
$ git clone https://github.com/vedderb/summon-arm-toolchain.git
$ apt-get install flex bison libgmp3-dev libmpfr-dev libncurses5-dev \
  libmpc-dev autoconf texinfo build-essential libftdi-dev zlib1g-dev \
  git zlib1g-dev python-yaml
$ cd summon-arm-toolchain/
$ ./summon-arm-toolchain
$ export PATH=$HOME/sat/bin:$PATH
```

Install stlink.

```
$ sudo apt-get install libsgutils2-dev libusb-1.0-0-dev
$ git clone https://github.com/texane/stlink.git
$ cd stlink/
$ ./autogen.sh
$ ./configure
$ make
$ sudo make install
```

Install Ajhc.

```
$ sudo apt-get install haskell-platform gcc m4 patch libncurses5-dev
$ cabal install drift
$ export PATH=$PATH:$HOME/.cabal/bin
$ cabal install ajhc
$ ajhc --version
ajhc 0.8.0.10 (66a602abc10dec74e2c0bb9289819a015bf21e4f)
compiled by ghc-7.4 on a x86_64 running linux
```

## Build

```
$ git clone https://github.com/fpiot/stm32f4dis-ajhc.git
$ cd stm32f4dis-ajhc/without_os
$ make
$ file main.elf
main.elf: ELF 32-bit LSB  executable, ARM, EABI5 version 1 (SYSV), statically linked, not stripped
```

## Write to flash

Connect the board and your PC with USB cable.
At one terminal, start the connection to the board.

```
$ sudo st-util
```

At another terminal, connect to the debugger and flash program.

```
$ make gdbwrite
--snip--
Loading section .fini_array, size 0x4 lma 0x8001088
Loading section .data, size 0x458 lma 0x800108c
Loading section .jcr, size 0x4 lma 0x80014e4
Start address 0x8001004, load size 5352
Transfer rate: 3 KB/sec, 764 bytes/write.
(gdb) c
```

## Original source code

https://github.com/jeremyherbert/stm32-templates
