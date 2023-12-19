## Initialize and optimize the turing-pi-2 board

### Start by bringing the board to current firmware

    Download the .img file from https://firmware.turingpi.com/turing-pi2/

    Burn the image onto the SD card, follow steps from https://docs.turingpi.com/docs/turing-pi2-bmc-v1x-to-v2x

    Power off the board and remove the SD card if you did not do yet.

### Add the CR1220 button cell battery for the real time clock

    CR1220 is used in the board V2.4 with the cell adaptor installed.

### Power the board and find the Board Managment C (BMC)

    Once the board is powered and ethernet cable connected two LEDs will be activate: a green LED next to the ATX power connection and orange blinking LED near the red power LED of Node 1

    Type https://turingpi.local on a browser in the same network. If there are multiple turing boards on same network, type https://turingpi2.local
    To login, user: root, password: turing

### Define the USB node settings

    As the mini PCI-Express will be used, we need to set the USB HOST MODE to Node 3, use the USB tab on the BMC (while Nodes are Off!!!)

    https://docs.turingpi.com/docs/turing-pi2-automating-node-and-usb-settings

### Nodes power

    The nodes start in "off" state. They can be turned on via BMC or via command line. Leave them off for now until the modules are installed.
