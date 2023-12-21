## Here are the initialization of the CM4 board(s)

### Prepare Mac

#### Download and Install Raspberry Pi imager

https://www.raspberrypi.com/software/

#### Certify you have ssh public-key

- on a mac terminal use: cat ~/.ssh/id_rsa.pub --> if there is something skip creation
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

### Boot the beasts!

- Install the CM4 with the respective adaptors, I suggest master in node 1, worker 1 in node 2, worker 2 in node 3
- The selection of nodes is not random, using the suggestion will simplify our lives
- Apply power to the turing board and make sure it is connected to the network
- Goto to http://turingpi.local, section power, select Node 1, 2, 3 to power the nodes. A red led will turn on by each node

### Find out if the beasts survived all this...

- ssh username:turingNN-master.local
- respond "yes" when asked and you should get to the CM4 command prompt
- this is a good time for:

  ```
  sudo apt update && sudo apt -y upgrade
  ```

- type exit
- repeat the process for turingNN-worker-1 and turingNN-worker-2

### If everything worked you are one of the lucky guys!!!
