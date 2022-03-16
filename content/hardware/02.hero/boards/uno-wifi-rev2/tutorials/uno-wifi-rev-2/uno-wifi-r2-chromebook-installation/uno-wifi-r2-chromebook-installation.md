---
title: 'UNO WiFi Rev 2 Chromebook Setup'
difficulty: easy
description: 'A quick tutorial on how to setup your UNO WiFi Rev 2 board with a Chromebook, using the Web Editor & the Arduino Chrome App.'
tags: 
  - Chromebook
  - Installation
author: 'Karl Söderby'
hardware:
  - hardware/03.hero/boards/uno-wifi-rev-2
software:
  - web-editor
---

## Introduction 

> This tutorial is only relevant for Chromebook users that uses an Arduino UNO WiFi Rev 2 board.  

The [UNO WiFi Rev 2](https://store.arduino.cc/arduino-uno-wifi-rev2) is the connected version of the classic UNO board. If you are using a **Chromebook**, setting up your board is a bit different for this particular board:

- You will need to upgrade the firmware using either a **Windows/Mac/Linux** computer, prior to programming it via a Chromebook. Detailed instructions are provided in this tutorial, and the process only takes a few minutes!
- It is only possible to use the [Web Editor](https://create.arduino.cc/editor), an online IDE that is part of the [Arduino Cloud](https://cloud.arduino.cc/).

***Note that only the Web Editor is supported in Chromebooks. It is not possible to configure and upload to UNO WiFi Rev 2 boards via the [IoT Cloud](https://create.arduino.cc/iot/things).***

## Goals

The goals of this project are:

- Learn how to upgrade the firmware on your UNO WiFi Rev 2, so it can be used with a Chromebook.
- Learn how to install the [Arduino Create for Education](https://chrome.google.com/webstore/detail/arduino-create-for-educat/elmgohdonjdampbcgefphnlchgocpaij) app from Chrome Web Store.
- Learn how to upload a sketch to your board using a Chromebook and the Web Editor.

## Hardware & Software Needed

- [Arduino IDE 1.8.x](https://www.arduino.cc/en/software).
- [Arduino Web Editor](https://create.arduino.cc/).
- [Arduino Create for Education](https://chrome.google.com/webstore/detail/arduino-create-for-educat/elmgohdonjdampbcgefphnlchgocpaij) (Chrome Web Store)
- [Arduino UNO WiFi Rev 2](https://store.arduino.cc/arduino-uno-wifi-rev2).

***While you won't be using the Arduino IDE directly, you will be utilizing a tool called AVRDUDE that is included in each version of the IDE. If you wish to install just AVRDUDE, please refer to the [GitHub repository](https://github.com/avrdudes/avrdude).***

## Upgrading Firmware

Since Chromebooks cannot run executables, the firmware upgrade for the UNO WiFi Rev 2 needs to be done through a Windows/Mac/Linux computer. 

**1.** Make sure you have installed [Arduino IDE 1.8.x](https://www.arduino.cc/en/software).

**2.** Download the [optiboot_atmega4.hex](/resources/firmware/optiboot_atmega4809.hex) file, and move it to your **Desktop folder**. 

![.hex file in your Desktop folder.](assets/hex-file-desktop.png)

**3.** Connect your UNO WiFi Rev2 board to your computer and open your Command Prompt (Windows) or Terminal (Mac/Linux), copy paste the command for your OS from the snippets below.

### Mac

```
/Users/$(whoami)/Library/Arduino15/packages/arduino/tools/avrdude/6.3.0-arduino17/bin/avrdude -C/Users/$(whoami)/Library/Arduino15/packages/arduino/tools/avrdude/6.3.0-arduino17/etc/avrdude.conf -v -patmega4809 -cxplainedmini_updi -Pusb -b115200 -e -D -Ufuse2:w:0x01:m -Ufuse5:w:0xC9:m -Ufuse8:w:0x02:m -Uflash:w:/Users/$(whoami)/Desktop/optiboot_atmega4809.hex:i
```

### Windows

```
"C:/Program Files (x86)/Arduino/hardware/tools/avr/bin/avrdude.exe" -C "C:/Program Files (x86)/Arduino/hardware/tools/avr/etc/avrdude.conf" -v -patmega4809 -cxplainedmini_updi -Pusb -b115200 -e -D -Ufuse2:w:0x01:m -Ufuse5:w:0xC9:m -Ufuse8:w:0x02:m -Uflash:w:%userprofile%\Desktop\optiboot_atmega4809.hex:i
```

### Linux

In the terminal, navigate to your root directory.

```
cd /
```

Then, run the following command:

```
home/$(whoami)/Downloads/arduino-1.8.19-linux64/arduino-1.8.19/hardware/tools/avr/bin/avrdude -C home/$(whoami)/Downloads/arduino-1.8.19-linux64/arduino-1.8.19/hardware/tools/avr/etc/avrdude.conf -v -patmega4809 -cxplainedmini_updi -Pusb -b115200 -e -D -Ufuse2:w:0x01:m -Ufuse5:w:0xC9:m -Ufuse8:w:0x02:m  -Uflash:w:/home/$(whoami)/Desktop/optiboot_atmega4809.hex:i
```

***Please note that on Linux, the path to the AVRDUDE tool may vary.***

This will start a process of uploading the `.hex` file to your board. This will not take long, but make sure you do not disconnect the board from your computer. When finished, you should see the following output in the terminal (screen capture from Windows): 

![Successful upgrade](assets/windows-success.png)

Now that your firmware is upgraded, you should see your board blinking (1 second off, followed by a quick blink). This is another proof that it was successful. You can now disconnect your board, and **plug it into your Chromebook.** 

### Check AVRDUDE Installation

The above commands utilizes a tool called **AVRDUDE**, which is included in each version of the IDE. To check whether it is accessible on your computer, you can run the following commands. 

**Windows:**

```
"C:/Program Files (x86)/Arduino/hardware/tools/avr/bin/avrdude.exe"
```

**Mac:**

```
/Applications/Arduino.app/Contents/Java/hardware/tools/avr/bin/avrdude
```

**Linux:**

```
/home/$(whoami)/Downloads/arduino-1.8.19-linux64/arduino-1.8.19/hardware/tools/avr/bin/avrdude
```

### Troubleshoot

If the command fails to upgrade the firmware, please make sure that:

- Arduino IDE / AVRDUDE is installed.
- That you are using a Windows/Mac/Linux computer (remember, this cannot be performed on a Chromebook).
- That you have the `.hex` file in the Desktop folder. The command is written to look for it in that specific folder, so if it is not present, it will not work.

## Install Arduino App (Chrome Store)

To program your Arduino via a Chromebook, you will need the [Arduino Create for Education app](https://chrome.google.com/webstore/detail/arduino-create-for-educat/elmgohdonjdampbcgefphnlchgocpaij). This is downloaded and installed via the Chrome Web Store.

![Install the app.](assets/chromestore.png)

***If you have previously installed the app, make sure your version is up to date.***

## Web Editor

***To use the [Web Editor](https://create.arduino.cc/editor), you will need to be logged into your Arduino account. If you don't have an account, you will need to register one.***

**1.** Head over to the [Web Editor](https://create.arduino.cc/editor).

**2.** Create a new sketch, and write your program.

**3.** When you want to upload, connect your board to your computer via USB.

![Connect your board to your computer.](assets/circuit.png)

**4.** After connecting, the board's **name** and **port** is visible at the top of the editor (next to upload button). In this case, it is `COM32`.

![Board discovered.](assets/board-discovered.png)

**5.** Click the upload button. This will start the **compilation process**, and then upload the sketch to your board. 

Congratulations, you have now uploaded a sketch to your UNO WiFi Rev 2 using the Web Editor on a Chromebook.

### Troubleshoot

If things are not working as expected:

- Make sure you have the latest version of the [Arduino Create for Education App](https://chrome.google.com/webstore/detail/arduino-create-for-educat/elmgohdonjdampbcgefphnlchgocpaij) installed.
- Make sure your board is connected to your computer properly.

## Conclusion

In this tutorial, we learned how to upload sketches to the UNO WiFi Rev 2 board, using the Web Editor on a Chromebook. For more tutorials on the UNO WiFi Rev 2 board, visit the [official documentation](/hardware/uno-wifi-rev2).
