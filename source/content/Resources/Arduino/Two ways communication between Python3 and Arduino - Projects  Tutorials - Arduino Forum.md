---
title: "Two ways communication between Python3 and Arduino - Projects / Tutorials - Arduino Forum"
source: "https://forum.arduino.cc/t/two-ways-communication-between-python3-and-arduino/1219738?_gl=1*hrx9yb*_up*MQ..*_ga*MjM5NDM1NTU2LjE3MzcxNDUxNTg.*_ga_NEXN8H46L5*MTczNzE0NTE1Ni4xLjAuMTczNzE0NTE1Ni4wLjAuMTI2OTQ3NDYwOA"
author:
  - "[[J-M-L]]"
published: 2024-02-04
created: 2025-02-23
description: "Hello everyone, As the use of Python is becoming more widespread in schools, many of you are looking to connect your Arduino to your Mac or PC using Python. Using the serial port of your computer with Python is not com&hellip;"
tags:
  - "clippings"
---
Hello everyone,

As the use of Python is becoming more widespread in schools, many of you are looking to connect your Arduino to your Mac or PC using Python.

Using the serial port of your computer with Python is not complicated, but doing it in a robust way is a bit more challenging if you want to handle the inherent asynchronous operation of serial connections.

The purpose of this tutorial is to provide you with minimal code on both the Python and Arduino sides to manage communication in the form of "command lines". Once this communication is mastered, you can modify the code to enable binary communication if desired (with a somewhat robust protocol).

For those unfamiliar with the concept of serial communication with Arduino (or managing asynchronous flow in general), you can take a look [Serial Input Basics](http://forum.arduino.cc/index.php?topic=396450.0). It will give you some ideas about how to manage an asynchronous communication.

---

An important point to know about Arduino boards like UNO, MEGA, or Nano is that by default, they perform a software reset (reboot) when the serial communication is opened.

Arduino has designed this feature so that it's easy to upload code (the IDE opens the serial port, the board reboots, the bootloader takes control for a while and checks if a code needs to be installed in memory. If yes, it receives the code, copies it to flash memory, and then reboots. If not, it stops listening and runs the existing code on Arduino).

As a consequence, if you connect your Arduino, already loaded with your program, to the USB port of your computer, it will start and begin running. Then, when you launch the Python code that opens the serial port, your Arduino will restart.

Therefore, if your Python code sends information to your Arduino immediately (within a few nanoseconds, as your computer is fast) after opening the serial port, the Arduino will still be booting, and `Serial` will not be activated yet. This means that the Arduino will miss the communication.

To overcome this, you can make a physical modification to the Arduino (for example, by adding a 10 μF capacitor between GND and RESET) or, more permanently, change to a smaller pull-up resistor on the reset or cut the track used by CTS to trigger the reset.

These physical modifications can be useful in some cases and are good to know, but in the majority of projects, it's not a bad thing for the Arduino to start after the application on the PC has started. This way, you know exactly where you stand.

Since we don't know how long it will take for the Arduino to start, the simplest solution is to add a message from the Arduino to Python at the end of the setup() to say "OK, I'm ready." On the Python side, you wait for this message before starting.

The timeline is as follows:

[![image](https://europe1.discourse-cdn.com/arduino/optimized/4X/e/7/1/e71e890f64bd48690ef42af972776dd1bd5c45c7_2_690x300.png)](https://europe1.discourse-cdn.com/arduino/original/4X/e/7/1/e71e890f64bd48690ef42af972776dd1bd5c45c7.png "image")

Let's zoom into the steps to get there.

---

**1/ The first question is how to access the serial port in Python.**

For this, you need a Python library. We will use [PySerial](https://pythonhosted.org/pyserial/), which requires Python 2.7 or Python 3.4 (or later) and at least Windows 7 if you are on a PC with Windows.

You can install it, for example, by typing the following in a terminal:

On Mac, for example: ` pip install pyserial`  
From Python: `python -m pip install pyserial`  
From conda: `conda install pyserial`

If you have an old version, you may need to do:  
`python3 -m pip install --upgrade pip`

(➜ see [the documentation](https://pyserial.readthedocs.io/en/latest/pyserial.html))

(Edit: removed sudo)

---

**2/ The second question is how to choose the right serial port in the Python program to open it.**

For this, we will import the serial library and ask it to list the accessible ports.

If you type the following in the Python3 command line:

```python
import serial
import serial.tools.list_ports
ports = serial.tools.list_ports.comports()
print(ports)
```

You will see a list appear. For example, with a UNO, an ESP32, and an MKR1000 connected to my Mac, it looks like this:

```arduino
[
<serial.tools.list_ports_common.ListPortInfo object at 0x1069920f0>, 
<serial.tools.list_ports_common.ListPortInfo object at 0x106992160>, 
<serial.tools.list_ports_common.ListPortInfo object at 0x1069921d0>, 
<serial.tools.list_ports_common.ListPortInfo object at 0x1069922e8>, 
<serial.tools.list_ports_common.ListPortInfo object at 0x106992358>, 
<serial.tools.list_ports_common.ListPortInfo object at 0x106992668>
]
```

Not very informative, but it means that the computer has detected 6 serial interfaces and filled an array with objects representing these interfaces (see [the documentation on available information](https://pyserial.readthedocs.io/en/latest/tools.html#serial.tools.list_ports.ListPortInfo)).

So, we can loop through and extract information.

```python
for index, value in enumerate(sorted(ports)):
    print(index, '\t', value.name, '\t', value.manufacturer)
```

I get

```plaintext
PORT	DEVICE			 	   	   	  MANUFACTURER
0  	   	cu.BLTH 	  	  	   	   	  None
1 	    cu.Bluetooth-Incoming-Port 	  None
2       cu.ESP32test 	  	   	   	  None
3 	    cu.usbmodem14101 	  	   	  Arduino LLC
4 	    cu.usbmodem14201 	  	   	  Arduino (www.arduino.cc)
5 	    cu.usbserial-0001 	  	   	  Silicon Labs
```

For example, we could build a list by removing unknown "MANUFACTURER".

```python
choices = []
print('PORT\tDEVICE\t\t\tMANUFACTURER')
for index, value in enumerate(sorted(ports)):
  if (value.hwid != 'n/a'):
    choices.append(index)
    print(index, '\t', value.name, '\t', value.manufacturer)
```

➜

```plaintext
PORT	DEVICE               MANUFACTURER
3 	    cu.usbmodem14101 	 Arduino LLC
4 	    cu.usbmodem14201 	 Arduino (www.arduino.cc)
5 	    cu.usbserial-0001 	 Silicon Labs
```

And then, propose to the user to choose one of the known ports.

```python
choice = -1
while choice not in choices:
    answer = input("➜ Select your port: ")
    if answer.isnumeric() and int(answer) <= int(max(choices)):
        choice = int(answer)
print('selecting: ', ports[choice].device)
```

So, it doesn't exactly tell us which Arduino is connected, but if there is only one, it will be simple. Put this in a function, and you have a way to choose one of the serial ports.

(EDITED based on discussion further down this thread)

```python
class NoValidPortError(Exception):
    """Exception raised when no valid Arduino ports are found."""
    pass

def selectArduino():
    ports = serial.tools.list_ports.comports()
    valid_ports = [port for port in ports if port.hwid != 'n/a']  # Filter out ports with 'n/a' hwid
    
    if not valid_ports:
        raise NoValidPortError("No valid Arduino ports found.")  # Raise an error if no valid ports

    print('PORT\tDEVICE\t\t\tMANUFACTURER')
    for index, value in enumerate(sorted(valid_ports)):
        print(f"{index}\t{value.name}\t{value.manufacturer}")  # Display sorted list with index

    choice = -1
    while choice < 0 or choice >= len(valid_ports):
        answer = input("➜ Select your port: ")
        if answer.isnumeric():
            choice = int(answer)

    selectedPort = sorted(valid_ports)[choice]  # Map the user's choice to the filtered list
    print(f"selecting: {selectedPort.device}")
    return selectedPort.device
```

Then, create a configuration function.

```python
baudRate = 115200

def selectArduino():
    ports = serial.tools.list_ports.comports()
    choices = []
    print('PORT\tDEVICE\t\t\tMANUFACTURER')
    for index, value in enumerate(sorted(ports)):
        if (value.hwid != 'n/a'):
            choices.append(index)
            print(index, '\t', value.name, '\t', value.manufacturer)

    choice = -1
    while choice not in choices:
        answer = input("➜ Select your port: ")
        if answer.isnumeric() and int(answer) <= int(max(choices)):
            choice = int(answer)
    print('selecting: ', ports[choice].device)
    return ports[choice].device

def configureArduino():
    global arduinoPort
    arduinoPort = selectArduino()
    global arduino
    arduino = serial.Serial(arduinoPort, baudrate=baudRate, timeout=.1)

# ---- MAIN CODE -----

configureArduino()
```

---

**3/ OK, so now we know that Arduino and the computer are connected via this serial port. How are we going to communicate?**

Since your Python program runs on a powerful and multitasking computer, a very efficient way is to listen to the serial port in a separate task and record the messages coming from the Arduino in a queue (a Python queue).

The background task receives characters arriving on the serial port one by one and adds them to a buffer. When the message is complete, it is added to the queue.

How do we know when the message is complete? If you have read the tutorial on the serial port, you know that it's good if the commands/messages have an end marker ➜ Here we will use the end of line '\\n' as the end marker so that from the Arduino, it's enough to do a `println()` to send a command.

The main Python task will simply check if there is a new message in the queue, and if so, remove it from the queue and do what is requested.

Therefore, we need to use some advanced Python classes that can speak to your computer's operating system and manage queues. Our Python code will start by importing the following elements:

```python
#!/usr/bin/python3
import sys, threading, queue, serial
import serial.tools.list_ports
```

The task that will listen to what the Arduino "*says*" can be defined simply:

Create an empty message buffer. Loop infinitely over listening to the serial port. When we receive the end marker, add the message to the queue; otherwise, add the received character to our message.

```python
def listenToArduino():
    message = b''
    while True:
        incoming = arduino.read()
        if (incoming == b'\n'):
            arduinoQueue.put(message.decode('utf-8').strip().upper())
            message = b''
        else:
            if ((incoming != b'') and (incoming != b'\r')):
                 message += incoming
```

To launch this background task, the main code should do:

```python
    arduinoThread = threading.Thread(target=listenToArduino, args=())
    arduinoThread.daemon = True
    arduinoThread.start()
```

Note that you can do the same for managing the computer's keyboard interface. If you want to send commands from the PC to the Python program, you could also have a task and a keyboard listening queue, on a similar principle.

For example, here I manage keyboard listening and record commands in uppercase (with `.upper()`).

```python
def listenToLocal():
    while True:
        command = sys.stdin.readline().strip().upper()
        localQueue.put(command)

def configureUserInput():
    localThread = threading.Thread(target=listenToLocal, args=())
    localThread.daemon = True
    localThread.start()
```

---

**4/ So now we know how to listen to our Arduino or what the user says. Let's focus on the synchronization point with the Arduino we talked about at the beginning.**

For this, you just need to agree on the baud rate (115200 in the example) and, at the end of the `setup()`, send a known and expected message by the Python code, which will simply wait in a loop by scanning the message queue to see if it receives this message, for example, just "OK".

```python
print("Waiting for Arduino")
while True:
    if not arduinoQueue.empty():
        if arduinoQueue.get() == "OK":
            break
print("Arduino Ready")
```

The basic Arduino code:

```cpp
void setup() {
  Serial.begin(115200);
  Serial.println("OK"); // tell Python that the setup has been executed
}

void loop() {
  // your program
}
```

---

**5/ The main Python code**

Now that everything is set up, the main Python code can be very simple:

- Check if there is a message in the Arduino queue and manage it (by removing it from the queue).
- Check if there is a message in the user queue and manage it (by removing it from the queue).
- Do something else that is non-blocking.

```python
while True:
    if not arduinoQueue.empty():
        handleArduinoMessage(arduinoQueue.get())

    if not localQueue.empty():
        handleLocalMessage(localQueue.get())

     # do something else here if you want, as long as it's non-blocking
```

The functions `handleArduinoMessage()` and `handleLocalMessage()` are where you manage the commands.

---

**6/ Now all that's left is to put it all together**

to create a small demo code that does ping-pong: what you type on the Python side is converted to uppercase (during entry by the background task), then sent to the Arduino, which simply echoes it on the serial port back to the Python program.

The Python3 program: (slightly edited to take into account feedback from further down in the discussion)

**arduino.py**

```python
#!/usr/bin/python3

# ============================================
# code is placed under the MIT license
#  Copyright (c) 2023 J-M-L
#  For the Arduino Forum : https://forum.arduino.cc/u/j-m-l
#
#  Permission is hereby granted, free of charge, to any person obtaining a copy
#  of this software and associated documentation files (the "Software"), to deal
#  in the Software without restriction, including without limitation the rights
#  to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
#  copies of the Software, and to permit persons to whom the Software is
#  furnished to do so, subject to the following conditions:
#
#  The above copyright notice and this permission notice shall be included in
#  all copies or substantial portions of the Software.
#
#  THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
#  IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
#  FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
#  AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
#  LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
#  OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
#  THE SOFTWARE.
#  ===============================================

import sys, threading, queue, serial
import serial.tools.list_ports

baudRate = 115200
arduinoQueue = queue.Queue()
localQueue = queue.Queue()

class NoValidPortError(Exception):
    """Exception raised when no valid Arduino ports are found."""
    pass

def selectArduino():
    ports = serial.tools.list_ports.comports()
    valid_ports = [port for port in ports if port.hwid != 'n/a']  # Filter out ports with 'n/a' hwid
    
    if not valid_ports:
        raise NoValidPortError("No valid Arduino ports found.")  # Raise an error if no valid ports

    print('PORT\tDEVICE\t\t\tMANUFACTURER')
    for index, value in enumerate(sorted(valid_ports)):
        print(f"{index}\t{value.name}\t{value.manufacturer}")  # Display sorted list with index

    choice = -1
    while choice < 0 or choice >= len(valid_ports):
        answer = input("➜ Select your port: ")
        if answer.isnumeric():
            choice = int(answer)

    selectedPort = sorted(valid_ports)[choice]  # Map the user's choice to the filtered list
    print(f"selecting: {selectedPort.device}")
    return selectedPort.device

def listenToArduino():
    message = b''
    while True:
        incoming = arduino.read()
        if incoming == b'\n':
            try:
                arduinoQueue.put(message.decode('utf-8').strip().upper())
            except UnicodeDecodeError as e:
                # Handle the error: log it, ignore the message, or take other action
                print(f"UnicodeDecodeError: {e}. Message skipped.")
            message = b''
        else:
            if incoming not in (b'', b'\r'):
                message += incoming

def listenToLocal():
    while True:
        command = sys.stdin.readline().strip().upper()
        localQueue.put(command)

def configureUserInput():
    localThread = threading.Thread(target=listenToLocal, args=())
    localThread.daemon = True
    localThread.start()

def configureArduino():
    global arduinoPort
    arduinoPort = selectArduino()
    global arduino
    arduino = serial.Serial(arduinoPort, baudrate=baudRate, timeout=.1)
    arduinoThread = threading.Thread(target=listenToArduino, args=())
    arduinoThread.daemon = True
    arduinoThread.start()

# ---- CALLBACKS UPON MESSAGES -----

def handleLocalMessage(aMessage):
    print("=> [" + aMessage + "]")
    arduino.write(aMessage.encode('utf-8'))
    arduino.write(bytes('\n', encoding='utf-8'))

def handleArduinoMessage(aMessage):
    print("<= [" + aMessage + "]")

# ---- MAIN CODE -----

configureArduino()                                      # will reboot AVR based Arduinos
configureUserInput()                                    # handle stdin 

print("Waiting for Arduino")

# --- A good practice would be to wait for a know message from the Arduino
# for example at the end of the setup() the Arduino could send "OK"
while True:
    if not arduinoQueue.empty():
        if arduinoQueue.get() == "OK":
            break
print("Arduino Ready")

# --- Now you handle the commands received either from Arduino or stdin
while True:
    if not arduinoQueue.empty():
        handleArduinoMessage(arduinoQueue.get())

    if not localQueue.empty():
        handleLocalMessage(localQueue.get())
```

The Arduino program:  
**pingpong.ino**

```cpp
void setup() {
  Serial.begin(115200); Serial.println();
  Serial.println("OK"); // let the python code know we are ready
}

void loop() {
  // echo back in uppercase what we received
  if (Serial.available())
    Serial.write(Serial.read());
}
```

---

A small example of what you see in the terminal with a UNO connected to `cu.usbmodem14201` (I intentionally enter fake numbers at the beginning to choose the port; you can see that it waits correctly):

The "Arduino Ready" message arrives after about 1 to 2 seconds, which is the time it takes for my UNO to boot.

```plaintext
python3 arduino.py
PORT	DEVICE			MANUFACTURER
3 	 cu.usbmodem14201 	 Arduino (www.arduino.cc)
➜ Select your port: 7
➜ Select your port: 22
➜ Select your port: xxx
➜ Select your port: 3
selecting:  /dev/cu.usbmodem14201
Waiting for Arduino
Arduino Ready
hello
=> [HELLO]
<= [HELLO]
hello from Python
=> [HELLO FROM PYTHON]
<= [HELLO FROM PYTHON]]
```

Now, you have the building blocks in Python to communicate with your Arduino, all you need to add is your business logic for your code and commands.

---

hope this helps!