# SDR Project
Software-defined radio receiver, Engineering Electronics ii, Spring 2020
Partners: Chrisner Garcesa and Andrew Nascimento

## Goal
The goal of this project was to design the schematic for a radio receiver and implement it on a PCB.

## Specifications
The specific goals to achieve given by our professor were as follows:  
* Minimum discernible signal of less than 1uV  
* Image rejection of over 48kHz of band greater than 30dB  
* Tunable range of frequencies greater than 48kHz  
* Band frequency greater than 540kHz  
* Spurious signals below 10uV  

Additional equipment we would have at our disposal would be the Arduino Nano Every

## Block Diagram
![Block Diagram](https://github.com/andrewtnas/receiver/blob/master/Images/Picture1.png)
This is the general design we would follow in order to have a simple, working receiver. It would be our choice on how to implement each element of this design, however we often chose solutions that the professor suggested or other classmates were using as well, but adapted to our needs.

## Schematic
Here is a breakdown of our schematic:

### Bandpass-filter
![Butterworth Filter](https://github.com/andrewtnas/receiver/blob/master/Images/filter.png)
This part of the schematic is to filter our choice of frequencies to capture. We chose a range of 5-10MHz to listen to, so the incoming frequency is filtered through a 2nd order Butterworth filter. The transformer at the end sets the DC operating point of the incoming signal around at 2.15V.