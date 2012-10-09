Onduino is an open-source MIDI controller intended to replicate the 
tactile experience of playing an Ondes Martenot, an early 20th 
century electronic musical instrument.

http://en.wikipedia.org/wiki/Ondes_Martenot

The name Onduino combines the "Ondes Martenot" and the Arduino, which 
is used to realize the MIDI cntroller.

MIDI makes no sound by itself, so the controller needs to be used with 
some sort of MIDI-enabled instrument. I use the Soniccouturte VSTi 
Ondes Martenot.

http://www.soniccouture.com/en/products/28-ancient-rare-and-experimental/g27-ondes/

The initial implementation just covers the 'tiroir' - the switches to select 
different oscillators, different speakers, the low-pass filter, and to control 
the volume envelope. Unlike the original hardware (but like the Soniccouture VTi) 
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

The volume envelope is implemented using a high-resolution optical mouse
sensor.

