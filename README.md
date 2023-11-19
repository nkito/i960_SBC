[![GitHub Workflow Status (with event)](https://img.shields.io/github/actions/workflow/status/nkito/i960_SBC/docker-image.yml?label=docker-image&logo=github&style=flat-square)](https://github.com/nkito/i960_SBC/actions?workflow=docker-image)
[![GitHub Workflow Status (with event)](https://img.shields.io/github/actions/workflow/status/nkito/i960_SBC/build-test.yml?label=sample-binary&logo=github&style=flat-square)](https://github.com/nkito/i960_SBC/actions?workflow=build-test)

# i960 Single Board Computer

It is a hobby project. Please use it at your own risk.

## Hardware

### Parts

| Functions | Chips |
|----|----|
| Processor                          | Intel i960 <br>(N80960SA16 or N80960SB16) |
| Peripheral (UART, Timer, and GPIO) | Motorola MC68901P |
| Controller                         | Altera EPM7032SLC44-10 <br>(or Atmel ATF1502AS-7JX44) |
| RAM                                | Infineon CY7C1021BN-12ZXC (64K x 16)  |
| ROM                                | 27C512 (64K x 8) with access time below 120ns |

### Schematic

Schematis is [here](schematic/i960_Dev.pdf).
Though boards built as the schematic is are working correctly, there are issues related to voltage levels.
* 74HCT573 is better for U1, U4 and U11.
* Generation of RW̅ from WR̅ with a schmitt-trigger inverter 74HC14 might not work.
* The voltage level for clk2 pin is not the same for the other pins. Please care about clk2.

### Controller 

Controller source is [here](controller/).


## Software

### Cross compiler

Docker container image of cross compiler is available. 

* binutils 2.21.1
* gcc 2.95.3
* newlib 1.8.2

Install from the command line
```
$ docker pull ghcr.io/nkito/i960_sbc:latest
$ docker run -it --rm -v /path_to_src_folder_in_host:/src -u (host uid):(host gid) ghcr.io/nkito/i960_sbc:latest
```
Compiler binaries are in /usr/local/cross/bin.
