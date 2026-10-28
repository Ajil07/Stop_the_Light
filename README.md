# Stop the Light: Hardware Arcade Reaction Game

This project is a hardware-based arcade reaction game built entirely from discrete integrated circuits on a breadboard, requiring zero microcontrollers, Arduinos, or software code. Originally developed as a digital electronics laboratory coursework demonstration, "Stop the Light" challenges players to freeze a rapidly chasing light sequence on a target color. By splitting the timing, counting, and decoding tasks across separate logic ICs, the circuit visually exposes the raw digital signals at work, offering a highly interactive way to explore hardware timing and binary logic.

https://github.com/user-attachments/assets/cc125233-aa29-4bd1-9b74-f480b6a5fa93
<img width="1600" height="1200" alt="034577f6-54c5-4ed6-a7c3-78c2521ab3de" src="https://github.com/user-attachments/assets/a2fff7e3-d85c-440f-8b9f-c83a157f32cc" />

## Bill of Materials (BOM)

**Integrated Circuits**

* 1× NE555 Timer (DIP-8)


* 1× 74HC74 Dual D-Type Flip-Flop (DIP-14)


* 1× 74HC139 Dual 2-to-4 Line Decoder (DIP-16)



**Passive Components & Hardware**

* 1× 100 kΩ Potentiometer


* 1× 100 µF Electrolytic Capacitor


* 1× 10 nF Ceramic Capacitor


* 1× 10 kΩ Resistor


* 1× 1 kΩ Resistor


* 4× 330 Ω Resistors


* 4× LEDs (Red, Green, Blue, Yellow)


* 1× Rocker Switch


* 1× 4.5V Battery Supply (3× AA battery holder)


* 1× Breadboard and insulated jumper wires



## IC Pinout Reference
<img width="860" height="484" alt="NE555-Pinout-1024x576" src="https://github.com/user-attachments/assets/d8175bba-05fc-44bc-97f8-4c3660f3830f" />
<img width="1024" height="615" alt="74x74_package-and-pinout-1024x615" src="https://github.com/user-attachments/assets/8e0a0d2c-3ff1-436b-9650-f6b4c2e220cb" />
<img width="1024" height="585" alt="74x139_package-and-pinout-1024x585" src="https://github.com/user-attachments/assets/b21369ba-0732-499c-b899-49c16b80048f" />
## Circuit Logic Explanation

* **The Heartbeat (NE555 Timer):** Operates in astable mode to generate continuous clock pulses. The speed of these pulses—and thus the game's difficulty—is manually tuned by adjusting the 100 kΩ potentiometer, which alters the resistance in the timing circuit.


* **The Memory (74HC74 Dual Flip-Flop):** Acts as a 2-bit binary counter. With each clock pulse received from the timer, the flip-flops advance through a repeating sequence of four binary states (00, 01, 10, 11).


* **The Translator (74HC139 Decoder):** Reads the 2-bit binary output from the flip-flops and translates it into four individual output channels. As the counter cycles, the decoder pulls one output LOW at a time, illuminating the Red, Green, Blue, and Yellow LEDs in a repeating chase sequence.


* **The Action (Hardware Reset):** The rocker switch is wired to the reset pin of the NE555 (Pin 4). Pressing the switch shorts the pin to ground, instantly halting the clock pulses and freezing the counter on the currently illuminated LED.



## Core Connection Guide

**Power and Ground**

* Route all IC power pins (NE555 Pin 8, 74HC74 Pin 14, 74HC139 Pin 16) to the +V rail.


* Route all IC ground pins (NE555 Pin 1, 74HC74 Pin 7, 74HC139 Pin 8) to the GND rail.



**Clock and Counter Routing**

* Connect the clock output (NE555 Pin 3) directly to the first flip-flop clock input (74HC74 Pin 3).


* Cascade the flip-flops by wiring the first output (74HC74 Pin 6) to the second clock input (74HC74 Pin 11).


* Create a toggle state by wiring Pin 2 to Pin 6, and Pin 8 to Pin 12 on the 74HC74. Ensure all Preset and Clear pins are tied HIGH.



**Decoder and LEDs**

* Connect the 2-bit counter outputs (74HC74 Pins 5 and 9) to the decoder inputs (74HC139 Pins 2 and 3).


* Wire the LED cathodes directly to the decoder outputs (74HC139 Pins 4, 5, 6, 7) and tie all LED anodes to a common node connected to +V via a 330 Ω resistor.

<img width="1536" height="1024" alt="Stop the Light IC Pinout Reference" src="https://github.com/user-attachments/assets/df517133-7a4f-46f6-9bac-eac9c1f67124" />
Would you like to include an "Expanded Features" section in this README detailing how others could modify the circuit (like adding a piezo buzzer for sound) if they fork the project?
