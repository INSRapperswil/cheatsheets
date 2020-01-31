# Simple Linux commands

## Connect to device via serial cable
```bash
# Replace <adapter> with your device
sudo screen /dev/tty<adapter>
```
Mostly you will use /dev/ttyUSB0.

## open a root terminal
```bash
# start shell /bin/bash
sudo bash
```

## Write/Send output to a device
```bash
# Send self defined output to device
echo "Here the output" > /dev/tty<adapter>

# Write output of an command to device
ip a  > /dev/tty<adapter>
```
## open a root terminal
```bash
# start shell /bin/bash
sudo bash
```



