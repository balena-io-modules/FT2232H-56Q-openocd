# FT2232H-56Q-openocd

```bash
git clone https://github.com/resin-io-modules/FT2232H-56Q-openocd.git
```

### STEP 1 - Program FTDI

```bash
apt-get install ftdi-eeprom
modprobe -r ftdi_sio
ftdi_eeprom --flash-eeprom FT2232H-56Q-openocd/other/jtag.conf
```

Shutdown and remove power

### STEP 2 - Build custom OpenOCD

```bash
sudo apt-get install make
sudo apt-get install libtool
sudo apt-get install pkg-config
sudo apt-get install autoconf
sudo apt-get install automake
sudo apt-get install texinfo
sudo apt-get install libusb-1.0
sudo apt-get install libftdi-dev

cd FT2232H-56Q-openocd

./configure

sudo make
sudo make install
```

### STEP 3 - Flash binary

```bash
sudo apt-get install screen
screen
sudo openocd -f interface/ftdi/2232h-cp.cfg -f target/efm32.cfg
```

press CTRL-A+C to create a new window

```bash
sudo telnet localhost 4444
```

Inside the new cli run:

```
reset
program other/soc-empty.bin
```

