## Here are the initialization of the CM4 board(s)

### Prepare Mac
#### Download and Install Raspberry Pi imager
https://www.raspberrypi.com/software/
#### Certify you have ssh public-key
- cat ~/.ssh/id_rsa.pub  --> if there isn't one,
- create one from the terminal as follows:
  ssh-keygen -t rsa -b 4096 -C pontual@gmail.com (press enter 3 times)


### Get the CM4 OS image, customize it and flash a SD card
- Launch imager,
- device: raspberry pi 4
- Operating System: raspberry pi os lite (64-bit)
- Storage: pick the flash card
- Edit settings:
  - General   
    - set hostname (turing-master, worker-01, worker-02)
    - set username and password
    - set locale settings
  - Services
    - set Enable SSH, choose allow public-key (the key should already be loaded)
