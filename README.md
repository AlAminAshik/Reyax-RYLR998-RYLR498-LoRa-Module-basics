# Reyax-RYLR998-RYLR498-LoRa-Module-basics
This repo contains all the basics and resources for the RYLR998 and RYLR498 modules via uart and AT commands

# Important notes:
* The modules works by directly sending AT commands via its RX TX terminal at a default baudrate of 115200.
* The connection diagram are attached in the same repository. It does not require any additional hardware/MCU while sending data directly through terminal.
* The address number(0 to 65535) is what defines a module on a network group. it can adjusted by sending "AT+ADDRESS=<number>" through the terminal and it will keep it stored on its memory.
* The networkID is very important as it is a group function and only the modules with the same networkID are allowed to communicate to each other. i.e a module with networkID 18 cannot send or received data with another module with networkID 15 even with same address.
It is useful to create a mesh of networks.
The default networkID(3 to 15,and 18) is 18 and it can be changed by sending "AT+NETWORKID=15"
* you can reset and set every parameters to default factory values by sending "AT+FACTORY" and it will respond "+FACTORY"

# Basic test
* connect both modules via two CP2102 modules.
* ensure that both are on same frequency and on same networkID.
Check individually but by sending "AT+BAND?" and "AT+NETWORKID?".
note: you can reset to factory settings by sending "AT+FACTORY"
* set the baud rate to 115200
* Send "AT" and both modules should respond "ok". if using ArduinoIDE and you send by typing on the serial monitor, then make sure "Both NL & CR" are selected otherwise it will return "+ERR=1" which means there was not "enter" after the AT command.
* lets say both are on address 0, to send a data (max 240 bytes) type "AT+SEND=0,5,hello" (send to address=0, dataLength=5, and data=hello) and the other will output "+RCV=0,5,hello,0,11" which means is received from a device with address 0, dataLength=5, data=hello, RSSI=0dBm, SNR=11.

# connection diagram for RYLR998 with USB to UART with level shifter module
![Alt text](images/connection_with_usbToUart_and_level_shifter_module_cp2102.jpg)

# connection diagram for RYLR998 with USB to UART CP2102 module
![Alt text](images/connection_with_usb_to_uart_cp2102_module.jpg)