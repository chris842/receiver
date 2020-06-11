# SDR Project
* Software-defined radio receiver, Engineering Electronics ii, Spring 2020
* Partners: Chrisner Garcesa and Andrew Nascimento

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
[This mixer was designed by Dan Tayloe]
(https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwjM6-jRtvjpAhXiQzABHfqkA9wQFjAAegQIARAB&url=http%3A%2F%2Fwww.norcalqrp.org%2Ffiles%2FTayloe_mixer_x3a.pdf&usg=AOvVaw3V9iSmiFxa8wcdVf5OEluL)

It is simple to implement, is low noise, and allows the bandwidth to be adjusted. The first part of this circuit, the multiplexer, breaks the incoming signal into four outputs, at 0˚, 90˚, 180˚, and 270˚. Then the op-amp, shown below, inverts the redundant sections of the wave and diffferentiates them with their same-phase pair, then outputs two signals, which he calls the In-Phase and Quadrature signals. The op-amp filters the output to the audio-frequency range of up to 25kHz.  
![Op Amp](https://github.com/andrewtnas/receiver/blob/master/Images/op%20amp.png)

### Clock Generator and Johnson Counter
![Clock](https://github.com/andrewtnas/receiver/blob/master/Images/clock.png)  
The purpose of this circuit is to drive the multiplexer used in the Tayloe Mixer. The Johnson Counter arrangement of the flip-flops is used to activate the multiplexer switches, selecting the portion of the incoming wave to be inverted and differentiated. The switching frequency is set by an Arduino program.

### Voltage Smoother
![Voltage](https://github.com/andrewtnas/receiver/blob/master/Images/voltage%20copy.png)  

Dr. Frohne designed this section of the schematic to provide a stable, ripple-free voltage source. It takes 5 volts from the Arduino and powers the multiplexer, op amp, and DC bias circuit.

### Complete Schematic
![Schematic](https://github.com/andrewtnas/receiver/blob/master/Images/complete.png)  

## PCB
### Board Schematic
![PCB](https://github.com/andrewtnas/receiver/blob/master/Images/pcb.png)  
PCB design in KiCAD

### Board Render
![render](https://github.com/andrewtnas/receiver/blob/master/Images/render.png)  

### Assembled Board
![board](https://github.com/andrewtnas/receiver/blob/master/Images/board.png)  

## Tests & Results
### Bandpass Filter
![bandpass](https://github.com/andrewtnas/receiver/blob/master/Images/Bandpass%20Filter.png)  
The bandpass filter seems to work as expected. There is attenuation up to around 5MHz, where our band begins. A 500mV test signal was used.

### Transformer
![transformer](https://github.com/andrewtnas/receiver/blob/master/Images/Transformer.png)  
Our initial winding configuration seemed to only produce noise. An updated winding configuration is shown further below.


### Tayloe Mixer
![mixer](https://github.com/andrewtnas/receiver/blob/master/Images/Tayloe%20Mixer%20Output.png)  
This is not the expected output of the Tayloe mixer. We expected to  a quadrant of a sine wave on each output. Since we cannot verify if the oscillator circuit is working properly, this error may be due to the oscillator.

### Op Amp
![op amp](https://github.com/andrewtnas/receiver/blob/master/Images/OP%20Amp%20Output.png)  
The op amp seems to be functioning. We can only verify if it works as intended when the Tayloe mixer is working.


### Arduino & Oscillator
![arduino](https://github.com/andrewtnas/receiver/blob/master/Images/arduino%20out.png)  
![arduino](https://github.com/andrewtnas/receiver/blob/master/Images/arduino.png)  
Arduino 5V and 3V3 signals appear as expected. Gauging by the serial output, the SDR program seems to be working, but we were not able to capture a signal on the SDA and SCL ports.


## Problems & Things to Fix
### Transformer
We tried a different configuration for the transformer, by winding 18 turns on the primary and 18 on the secondary, and placing a center tap from the 2.15V pad to the middle point of the transformer. We were able to capture a clean sine wave at the transformer input, but not the output. 

### Voltage Divider
We were able trace the 4.3V signal up to where it meets R1 at the voltage divider, but we did not see any voltage across R1 or R2. This can explain why the transformer secondary is not working.

### Tayloe Mixer
The Tayloe mixer is likely not working due to the transformer issue. Since 4.3V is being produced, the output is likely due to the lack of signal reaching the mixer.

### Oscillator
We assume the issue with the oscillator is due to the Arduino program, although it seems to be working fine. It may also be due to improperly placing the surface mount IC on the board. 

## Lessons Learned
### PCB Design
We learned how to design a PCB from start to finish using KiCAD.

### Test Points
Having more test points would make debugging the circuit much easier. We did not include enough test points on the board so it was difficult to get measurements in certain places, and that made it harder to narrow down where issues were originating.

### Trial & Error
While it is important to simulate as much as possible so that a working design is achieved when the board is printed, some things were only able to be debugged when we put the circuit together. Simulation also doesn't account for our personal errors and mishaps, so having extra parts for a future project is important in case we damage parts.






