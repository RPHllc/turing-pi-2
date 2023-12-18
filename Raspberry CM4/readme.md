## Here are the initialization of the CM4 board(s)

### Prepare Mac
#### Download and Install Raspberry Pi imager
https://www.raspberrypi.com/software/
#### Certify you have ssh public-key
- on a mac terminal use: cat ~/.ssh/id_rsa.pub  --> if there is something skip creation
- if cat above did not find anything, create one from the terminal as follows:
  ssh-keygen -t rsa -b 4096 -C pontual@gmail.com (press enter 3 times)


### Get the CM4 OS image, customize it and flash a SD card
- Launch imager,
- device: raspberry pi 4
- Operating System: raspberry pi os lite (64-bit) - it is in "other"
- Storage: pick the flash card
- Edit settings:
  - say no to WiFi settings   
  - General   
    - set hostname (turingNN-master, turingNN-worker-1, turingNN-worker-2)
      where NN are your initials to allow multiple turing boards in same network
    - set username and password
    - set locale settings
  - Services
    - set Enable SSH, choose allow public-key (the key should already be loaded)
