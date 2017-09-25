# Control Einstein Robot from a PC with python scripts

## Force robot in Mobile mode (with firmware version of 2017-09-19)
Configure with Stein-O-Matic with an internet AP that will no longer exist after config.

Like using a temporary config of an AP on your home WiFi router and then after complete config of the robot, then change back to the original AP.

This will force  the robot to fail on going Online, stop trying and then Go Mobile as failsafe.

Go Mobile : That is to say the robot will set his Wifi in AP mode and if pressed on the chest button it will verbose credential

Example

AP = EINSTEIN3333\
PSK = genius1234

## Direct control from a PC
1. connect to the robot's AP from the WiFi adapter of your PC
2. simple control python script

  - usage : trivial.py "commandline"
```
#!/usr/bin/python3
import sys
import json
import socket
import time
print("Contacting Einstein Robot")

msg = {
    "data": {
        "output": sys.argv[1]
    },
    "cmd": "activity.recieved",
}

jmsg = json.dumps(msg, separators=(',', ':'))
fullmsg = str(len(jmsg)).zfill(5) + jmsg

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(("192.168.1.1", 8080))
time.sleep(3)
s.send(fullmsg.encode('utf-8'))
```
3. example of commands

| command line  |     effect    |
| --------------- | ------------- |
| "Hello, world"  | say the text  |
|  "<WK=WK2>" | make the robot walk  |
|  "<MO=EL,1.0,0.3><PM><MO=EL,0.0,0.3>" | blink eyes  |

4. full documentation

More examples to be added soon.


