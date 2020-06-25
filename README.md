LM75 Sensor for the Raspberry Pi

This repository contains file for an LM75 sensor that connects to a Raspberry Pi full project detail can be seen
Bash Script to read LM75 on the raspberry pi

It is intended for use with the raspbian operating system

First please update your system with

      apt-get update
      
From the termial type
      
    nano /etc/modprobe.d/raspi-blacklist.conf
    
and place a hash before the I2C and SPI commands to enable them

Next get a package called I2C tools

    apt-get install i2c-tools

Next step is to Modprobe the broadcom chip and i2C-dev

    modprobe i2c-bcm2708
    modprobe i2c-dev


Next grant permision for non root users to access the i2c commands


     usermod -a -G i2c pi # replace pi with your username


Exit the root terminal and reboot for the changes to take effect.

After reboot we need to Modprobe again

    modprobe i2c-bcm2708
    modprobe i2c-dev


To check the hardware is working correctly run the 12cget command if using a Rev A board use 

    i2cget -y 0 0x48 0x00 w

If using a Rapberry pi Rev B board or higher

    i2cget -y 1 0x48 0x00 w

If the hardware is working then the following code should be returned

    0x7e16


If this has happened then Raspbian talking to the device so the basic hardware is working.

Now lets see if the Magpi code can convert that to a temperature, be very careful with the syntax here I got it wrong multiple times.....(Change the i2cget -y 0 to i2cget -y 1 if using a rev B Board.

Clone the bash script LM75.sh

Run the command

    chmod +x lm75.sh
    ./lm75.sh
    
    
    
