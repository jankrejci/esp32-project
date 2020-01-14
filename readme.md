
# ESP32 Starter template

## About This template

This template can be used as is but, its intended as a quick start for the students learning the ESP32-IDF through the Udemy course [Getting started with the ESP32 and the IDF](https://github.com/Mair/esp32-starter/blob/master/misc/commingsoon.md)
## prerequisites

1. setup your toolchain and ESP-IDF as described in the [official documentation](https://docs.espressif.com/projects/esp-idf/en/latest/get-started/#step-1-set-up-the-toolchain)

Windows:
```
mkdir c:\esp
cd c:\esp
git clone --recursive https://github.com/espressif/esp-idf.git
cd esp-idf
install.bat
pip install -r requirements.txt
export.bat
```
set enviroment variables
```
setx IDF_PATH "C:\esp\esp-idf"
setx IDF_TOOLS "C:\Users\uzivatel\.espressif\tools"
setx GIT_EXECUTABLE "C:\Program Files\Git\bin\git.exe"
```
to permanently write PATH wariable run command
```
setx path "%PATH%"
```

Linux:
```
mkdir ~/esp
cd ~/esp
git clone --recursive https://github.com/espressif/esp-idf.git
cd esp-idf
./install.sh
pip install -r requirements.txt
```

3. In VSCODE add the c++ extension 
https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools
 
4. ensure tour ESP32 is plugged in and that a COM PORT is established (You may need a driver for your ESP32 dev board)

## vs code intellisense

intellisense should just work so long as you have set up the IDF_PATH environment variable as described in the [official documentation](https://docs.espressif.com/projects/esp-idf/en/latest/get-started/#step-1-set-up-the-toolchain) and the IDF_TOOLS as described above.

>NB. you may meed to do an initial build and restart vscode before it can resolve all variables.

## flashing the esp32

1. in vs code, open a new terminal by pressing ctrl + \` (or pressing F1 and typing `open new terminal`)
2. type the following command

### for setups with idf.py

```bash
idf.py -p [your com port] flash monitor
```

### or other versions -
*to set your com port*
```bash
make menuconfig 
```
set your com port in the menu under serial
then
```
make flash monitor
```
## debuging

You will need an FT2322 in order to use a jtag. you can get them for about $10.00 on ali express.

wire up the FT2322 and the esp32 as follows

![FT2322 jtag debugging][FT2322-jtag]

[FT2322-jtag]: /misc/pin%20mapping.svg "Logo Title Text 2"

| FT2322 Pin Name | FT2322 pin number | ESP32 pin name| ESP32 pin number
| --------------- |:-----------------:|:-------------:|:-------------:|
| TCK             | ADBUS 0           | 13            | MTCK  
| TDI             | ADBUS 1           | 12            | MTDI
| TDO             | ADBUS 2           | 15            | MTDO
| TMS             | ADBUS 3           | 14            | MTMS
| GND             |                   | GND           |

start the debugger by using

```
openocd -f debug\ftdi_ft2322.cfg -f debug\esp-wroom-32.cfg
```
