# ice40hx8k-evb-prog-if

![2022-09-17-182023_751x451_scrot](https://user-images.githubusercontent.com/44300715/190866536-572b4098-bab8-4b28-83ec-5b2d2c6a9b61.png)
![2022-09-17-182009_756x452_scrot](https://user-images.githubusercontent.com/44300715/190866542-d409e447-4a2c-4719-a986-5e8022baa7b2.png)
![signal-2022-09-17-181949_002](https://user-images.githubusercontent.com/44300715/190866549-0c66c733-47b1-4bdf-8699-ef01ad4a3365.jpeg)
![signal-2022-09-17-181949_004](https://user-images.githubusercontent.com/44300715/190866564-5bbf08c2-9c8c-4e6b-87a6-9750baba8a9b.jpeg)

This is a programming interface for Olimex ICE40HX8K-EVB, that should work with most SBCs on the market (with 40 GPIO pin headers). Tested with Odroid M1.

The board is completely passive and contains only one header and one socket. It may be recreated with a bunch of 2.54mm female-female wires.

It works by writing on-board EEPROM directly through SBC's SPI pins. The EVB's RESET pin is also routed and pulled by the GPIO during programming. The whole process is automated by a makefile crafted for this purpose.

Furthermore, two UART pins on SBC are routed to appropriate pins on FPGA EVB, so with simple UART Verilog modules, one gets a nice debugging interface, all in the same cable. For that, I recommend    [uart_tx](https://github.com/tomek-szczesny/ice40_lib/blob/main/uart_tx.v) Verilog module from my library. Alternatively, user may use these two pins as GPIO and put them to some other use.

### The Makefile

A template makefile is included, that can do the following things:

- Build a project, using yosys, nextpnr and so on,

- Burn a project (write onto a EVB connected to a remote SBC)

- Setup the remote SBC to act as a programmer.

This template obvoiusly must be configured to work with your project, by manipulating a bunch of variables at the very beginning of the file.

The "setup" is meant to be run only once. It creates a special user account on remote SBC, that gets rights to use SPI port and one GPIO that operates RESET pin.

### Requirements

In order to use this interface, the remote SBC requires:

- SSH server

- One sudoer (setup only)

- `flashrom`.

### Disclaimer

Whatever is in this repository is fiction and should not be taken seriously. All similarities with real world designs and coding was not intentional.

##### PCBs

I've got a few to spare, contact me if you're interested.
