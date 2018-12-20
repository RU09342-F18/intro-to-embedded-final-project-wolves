# Lego LED Christmas Tree
This project was created under the assumption of a theoretical customer who wanted a festive assembly of lights. Formed like
a christmas tree, this light assmebly will require around 12 different LEDs to be illuminated. In order to light this many LEDs
an I/O expander, the PCA9532, was used. This device is a 16-bit I2C bus with 16 LED drivers and two user-programmable PWM rates
on the chip. Considering the PCA9532 can only communicate through I2C, this device will be the slave of the system and we chose
the MSP430F5529 to be the master. This entails that the micro-controller will send the SDA, SCL, and reset signals to the PCA
and these three lines must all be pulled up to 5 volts using 10k ohm resistors. For ease in the system, power is generated from
a laptop to the micro-controller, and then to the circuit via the MSP's 5 volt and ground pins. The final step in constucting
the circuit to run this code is to also pull any LEDs being used up to 5 volts with a 120 ohm resistor, and to connect the
negative end of the diode to the desired PCA pin.

The current code within this repository is capable of illuminating a single LED which is on the LED3 pin of the PCA9532. This
is also pin 7 on the device. In order to setup a different assembly of LEDs, the code must be slightly altered to send
different bits to the PCA through the UCB0TXBUF buffer register. To send more than 4 LEDs, or more than one LED separated by
4 or more LEDs, the auto-increment bit must be driven high in the command byte, and more than one data byte must be sent
depending on the desired lighting scheme. In order to set one or both of the PWM registers in the PCA, the command byte on the
SDA line must first slightly be altered, and then the desired PWM rate sent in the data byte, followed by command byte for the
deesired LED resgiter, ending with the data byte for the specific LED once again. In this case, the auto-increment bit will
remain a 0 since different functions within the PCA are being used.
