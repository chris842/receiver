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
This part of the schematic is to filter our choice of frequencies to capture. We chose a range of 5-10MHz to listen to, so the incoming frequency is filtered through a 2nd order Butterworth filter. The transformer at the end sets the DC operating point of the incoming signal at 2.15V.

### Mixer
![Tayloe Mixer](https://github.com/andrewtnas/receiver/blob/master/Images/mixer.png)
[This mixer was designed by Dan Tayloe](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwjM6-jRtvjpAhXiQzABHfqkA9wQFjAAegQIARAB&url=http%3A%2F%2Fwww.norcalqrp.org%2Ffiles%2FTayloe_mixer_x3a.pdf&usg=AOvVaw3V9iSmiFxa8wcdVf5OEluL)

It is simple to implement, is low noise, and allows the bandwidth to be adjusted. The first part of this circuit, the multiplexer, breaks the incoming signal into four outputs, at 0˚, 90˚, 180˚, and 270˚. Then the op-amp, shown below, inverts the redundant sections of the wave and diffferentiates them with their same-phase pair, then outputs two signals, which he calls the In-Phase and Quadrature signals. The op-amp filters the output to the audio-frequency range of up to 25kHz.
![Op Amp](https://github.com/andrewtnas/receiver/blob/master/Images/op%20amp.png)

### Clock Generator and Johnson Counter
![Clock](https://github.com/andrewtnas/receiver/blob/master/Images/clock.png)
The purpose of this circuit is to drive the multiplexer used in the Tayloe Mixer. The Johnson Counter arrangement of the flip-flops is used to activate the multiplexer switches, selecting the portion of the incoming wave to be inverted and differentiated. The switching frequency is set by an Arduino program.

### Voltage Smoother