## Here are the settings needed to initialize and optimize the turing-pi-2 board

### Let's start by bringing the board to current firmware
Download the .img file from https://firmware.turingpi.com/turing-pi2/
Burn the image onto the SD card, follow steps from https://docs.turingpi.com/docs/turing-pi2-bmc-v1x-to-v2x

### Define the node settings https://docs.turingpi.com/docs/turing-pi2-automating-node-and-usb-settings
As the mini PCI-Express will be used, we need to set the USB HOST MODE to Node 3 (before turning the Nodes ON)
The nodes start in "off" state, the automation can turn them on automatically after power up

### Add the CR1220 button cell battery for the real time clock
This is the cell size used in the board V2.4 with the cell adaptor installed.

### WE NEED TO DECIDE IF WE WILL LEAVE THE SD CARD INSTALLED
What would be the use cases?

