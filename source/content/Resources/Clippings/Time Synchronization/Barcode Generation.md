---
title: "Barcode Generation"
source: "https://optogeneticsandneuralengineeringcore.gitlab.io/ONECoreSite/projects/DAQSyncro/BarcodeGeneration/"
author:
  - "[[Andrew Scallon]]"
published: 2021-11-30
created: 2025-02-19
description: "Align and synchronize data acquisition systems"
tags:
  - "clippings"
---
[Projects](https://optogeneticsandneuralengineeringcore.gitlab.io/ONECoreSite/projects/) | 2021 | Links:

![Barcode Generation](https://optogeneticsandneuralengineeringcore.gitlab.io/ONECoreSite/assets/img/projects/DAQSyncro/1200px-UPC-A-036000291452.svg.png)

Align and synchronize data acquisition systems

Herein is an expansion on barcode generation for the [DAQ Synchronization project](https://optogeneticsandneuralengineeringcore.gitlab.io/ONECoreSite/projects/DAQSyncro/DAQSyncronization/). This can be a standalone project or can be considered part of the overall DAQ Synchronization Project. With this project, a simple Arduino is used to generate a random 32-bit barcode. This barcode can then be output on one of the Arduino’s 5V pins (hey look, a TTL!) as a ‘synchronization’ signal. The Arduino then increases the barcode by one bit and outputs that signal, either ad infinitum or after a set number of intervals, depending on whether you want to use a trigger to initiate barcode generation.

The Arduino chosen was the [Beetle](https://www.dfrobot.com/product-1075.html) due to its low cost, size, power, and overall cool factor. The more common Arduino Uno could also be used, but should be considered less cool. Note: the Beetle should be programmed as “Arduino Leonardo” (in the Arduino IDE go to Tools > Board > Arduino AVR > Arduino Leonardo).

All DAQ Synchronization project code (with example data!) can be found within [this zip file](https://gitlab.com/OptogeneticsandNeuralEngineeringCore/daqsyncro/-/raw/main/DAQSyncronization.zip?inline=false). Simply download and extract. Or, if you want just the code for this part of the project, see [here](https://gitlab.com/OptogeneticsandNeuralEngineeringCore/daqsyncro/-/raw/main/DAQSyncronization/arduino_barcodes.ino?inline=false).

---

## Barcode and Wrapper Signal Permalink

The randomly generated barcode is a 32-bit barcode, and each of the 32 bits is output as a TTL “HIGH” or “LOW” signal for 30 milliseconds. In order to assure that we can clearly read this barcode and separate its HIGH/LOW states from any inter-barcode HIGH/LOW state, we wrap the beginning and end of the barcode in a known, distinct LOW/HIGH/LOW ‘wrapper’ with three 10 millisecond bits. Then, when we read the synchronization signal, we can identify the beginning and end of each barcode, and because each bit of the wrapper is of different duration than the barcode bits, it is well distinct from any previous state of the TTL. This is important because if a barcode starts off in the LOW state for a couple bits, it would be difficult to distinguish this from a LOW inter-barcode state.

---

## Hardware Permalink

Nothing should be connected to the A0 pin. We read this pin as noise to make the barcode *totally* random. That is, rather than just use a computer to generate some random number, we read some noise signal on this pin, and then ask the computer to generate a random number based on this random. *Totally* random.

We output our TTL barcode synchronization signal on Pin 9.

The Arduino (Beetle and Uno) has an onboard LED (pin 13). We use this as a signal of when a barcode is being output, with the LED off when the barcode is being generated, and on for the inter-barcode duration.

Optional: The Beetle can be programmed to output its barcodes only after a button is pressed, or an input TTL into the Beetle goes HIGH. For this, choose the arduino\_barcodes\_trigger.ino file. This requires the use of the [Bounce2 library](https://github.com/thomasfredericks/Bounce2). This ‘input pin’ is Pin 11.

![IMG_0060.png](https://optogeneticsandneuralengineeringcore.gitlab.io/ONECoreSite/assets/img/projects/DAQSyncro/IMG_0060.png "IMG_0060.png")

Fun side note: when the LJ is plugged into a USB, VS is 5V. This means that you can power the Arduino Beetle by connecting the ‘+’ pin (red wire in the pic above) to VS and the Beetle ‘-‘ to GND (either green wire in the pic above). Then you can have an entire system generating and outputing a barcode to both the LJ and some other DAQ *and* recording all your other signals across a *single* USB cord. Neat.

---

## Sketch Permalink

The Arduino sketch arduino\_barcodes.ino is the standard code that will output barcodes at fixed intervals without any input. Simply save the file somewhere, and set the board to “Arduino Leonardo” (in the Arduino IDE go to Tools > Board > Arduino AVR > Arduino Leonardo). Look at the boards currently connected to your computer (Tools > Port), plug in your Arduino, see what shows up as a new port, select it, and then hit upload (right arrow).

The Arduino sketch arduino\_barcodes\_trigger.ino is a supplementary code that will only output barcodes after either a button is pressed or a TTL input trigger goes HIGH. The code can be uploaded similar to the above paragraph, but you must also include the Bounce2 library (Tools > Manage Libraries > search for Bounce2 > Install).

Direct links: [arduino\_barcodes.ino](https://gitlab.com/OptogeneticsandNeuralEngineeringCore/daqsyncro/-/raw/main/DAQSyncronization/arduino_barcodes.ino?inline=false) or [arduino\_barcodes\_trigger.ino](https://gitlab.com/OptogeneticsandNeuralEngineeringCore/daqsyncro/-/raw/main/DAQSyncronization/arduino_barcodes_trigger.ino?inline=false).

---

## User Variables Permalink

In general, the user need not update the code, but it may be useful to have barcodes be generated at intervals other than the default 5 seconds (5000 milliseconds). Therefore, we listed that variable at the top of the sketch under “User Variables”. The total time for a single barcode with wrappers is 1020 milliseconds, so if you choose to go faster than that…well, good luck, and if you are using the other code from the DAQ Synchronization project, be sure to update all related time variables that have been changed.

A user using the arduino\_barcodes\_trigger.ino should also set whether or not they are using a button or an input TTL. They should also set how many barcodes to output after a trigger event is detected.

---

## ONE Core acknowledgment Permalink

Please acknowledge the ONE Core facility in your publications. An appropriate wording would be:

*“The Optogenetics and Neural Engineering (ONE) Core at the University of Colorado School of Medicine provided engineering support for this research. The ONE Core is part of the NeuroTechnology Center, funded in part by the School of Medicine and by the National Institute of Neurological Disorders and Stroke of the National Institutes of Health under award number P30NS048154.”*