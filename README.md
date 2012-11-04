Onduino is an open-source MIDI controller intended to replicate the 
tactile experience of playing an Ondes Martenot, an early 20th 
century electronic musical instrument.

http://en.wikipedia.org/wiki/Ondes_Martenot

The name Onduino combines the "Ondes Martenot" and the Arduino, which 
is used to realize the MIDI controller.

MIDI makes no sound by itself, so the controller needs to be used with 
some sort of MIDI-enabled instrument. I use the Soniccouturte VSTi 
Ondes Martenot.

http://www.soniccouture.com/en/products/28-ancient-rare-and-experimental/g27-ondes/

The initial implementation just covers the 'tiroir' - the switches to select 
different oscillators, different speakers, the low-pass filter, and to control 
the volume envelope. Unlike the original hardware (but like the Soniccouture VSTi) 
the switches are replaced by sliders. So instead of a simple on-off, each oscillator 
and each speaker has a 0..127 range, controlled by MIDI.

A full implementation would also include a keyboard (the Ones Martenot 
used a smaller than full size, 5-octave keyboard), vibrato (the keyboard 
moves from side to side), and the 'bague' or ring, a continuous pitch controller.
This last aspect does not map well to MIDI.

The Onduino is implemented using an Arduino Mega2560

http://arduino.cc/en/Main/ArduinoBoardMega2560

which has 16 10-bit analog inputs. 14 of them are used in the initial design.
12 slider potentiometers, and a switch are used for speaker and oscillator 
selection plus one rotary potentiometer for the filter and another switch to 
select between keyboard and 'bague'. Another analog input is reserved for 
a keyboard-shake sensor. 

The analog inputs are buffered with unity-gain stages using the MCP 6231 
rail-to-rail op-amp. The analog stage has a dedicated 5V power supply. This design 
allows the ADC to be updated later to a  16-bit design (MIDI can theoretically 
deal with 14-bit controller changes) without having to change the analog board 
or front panel hardware.

28 digital outputs are used to control 14 bicolor (red/green/amber) status LEDs. 
These are high brightness, but driven at a fairly low current.

The volume envelope is implemented using a high-resolution optical mouse
sensor, the ADNS3080, which reports on movement of the volume control ("touche 
d'intensité") since the last time it was polled. The sensor connects over an SPI bus.

MIDI over USB is handled by a Teensy 2.0 Arduino-comatible board, set to native 
USB MIDI mode. The Mega2560 connects to this over serial.

User interface for setup and calibration is handled by an Arduino Uno with a 
Snootlabs Deuligne 16x2 LCD display sheild. Config information is passed to the
Mega 2560 over serial. The Uno will also handle the 'bague' controller, using 
an I2C 16-bit ADC and a ten-turn high linearity wirewound potentiometer. The 
result is sent directly to the PC, since MIDI can't represent continuous-note 
controllers.

