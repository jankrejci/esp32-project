
# ESP32 Project template

## About This template
This template is forked from [Mair/esp32-starter](https://github.com/Mair/esp32-starter) template.

## Prerequisities
It is expected you have already installed following packages. If not install it to your system and try to run it from command line.

[Python 3.7+](https://www.python.org/) \
[VS code](https://code.visualstudio.com/) \
[GIT](https://git-scm.com/)

It is expected that these commands works before instalation.
```
python --version
git --version
```

## ESP-IDF installation
Setup your toolchain and ESP-IDF as described in the [official documentation](https://docs.espressif.com/projects/esp-idf/en/latest/get-started/#step-1-set-up-the-toolchain). You can also follow instructions below.

**Windows**:
```
mkdir c:\esp
cd c:\esp
git clone --recursive https://github.com/espressif/esp-idf.git
cd esp-idf
install.bat
pip install -r requirements.txt
export.bat
```
set enviroment variables, if you have different installation folders, change paths respectively
```
setx IDF_PATH "C:\esp\esp-idf"
setx IDF_TOOLS "C:\Users\uzivatel\.espressif\tools"
setx GIT_EXECUTABLE "\"C:\Program Files\Git\bin\git.exe\""
```
write PATH permanently
```
setx path "%PATH%"
```

**Linux**:
```
mkdir ~/esp
cd ~/esp
git clone --recursive https://github.com/espressif/esp-idf.git
cd esp-idf
./install.sh
pip install -r requirements.txt
. export.sh
```

## VS code settings
3. In VSCODE add the c++ extension 
https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools
intellisense should just work so long as you have set up the IDF_PATH environment variable as described in the [official documentation](https://docs.espressif.com/projects/esp-idf/en/latest/get-started/#step-1-set-up-the-toolchain) and the IDF_TOOLS as described above.

>NB. you may meed to do an initial build and restart vscode before it can resolve all variables.

## Tasks

## Toolchain

4. ensure tour ESP32 is plugged in and that a COM PORT is established (You may need a driver for your ESP32 dev board)

1. in vs code, open a new terminal by pressing ctrl + \` (or pressing F1 and typing `open new terminal`)
2. type the following command


## Debuging

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
