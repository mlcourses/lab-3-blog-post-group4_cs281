# Lab 3: Voltage Divider, Potentiometer and Building a 7-Segment Display

## Overview and Motivation
The goal of this lab is to design a more complex circuit and to learn more about the function of a voltage divider inside a potentiometer. The potentiometer is different from the other types of inputs we have used so far because it has a range of values (1-1023) instead of just on and off. This lab will help us understand how to understand how a voltage divider works inside a potentiometer, read values from a potentiometer and how to use the output of the potentiometer in a circuit.

## Materials
1. PB-503 (breadboard)
2. Electrical Wires
3. 7-Segment Display
4. 7 330 Ohm Resistor (each per segment)
5. Arduino Kit
6. 7408 AND Gate
7. 7404 NOT Gate
8. 7432 OR Gate

## Project Steps

## Part 1: Voltage Divider and Potentiometer
We first designed a simple circuit for the potentiometer. The potentiometer is another part of the breadboard that can supply a variable amount of voltage. A potentiometer works based on the concept of the voltage divider, which relies on two resistors and an output voltage in the middle of the two. A voltage divider can be represented by the diagram below:

<img width="340" alt="voltage divider concept" src="https://github.com/mlcourses/lab-3-blog-post-group4_cs281/assets/67582698/1727542b-5ca9-4c7c-bb32-351f84684972">

The voltage divider (the V in the diagram) is the output voltage of the circuit. Ohm's law gives us the equation: V = IR, where V is voltage, I is current and R is resistance. Rearranging the formula, we have V1 (the part with R1 in the diagram before V divides it) = I x R1 and V2 (the part with R2 in the diagram before V divides it) = I x R2. Rearranging the equation with I as a common factor, we have V = R1/(R1+R2) * Vcc. This equation shows that we can have variable voltage by changing the values of R1 and R2.

The concept of a potentiometer is similar, with there being a knob that turns. This is represented by V in the image above. By changing the location of the output voltage, we can change the resistance combination of R1 and R2, and thus, make voltage variable. The picture below shows the potentiometer on our breadboard, with Vcc and GND attached.

<img width="261" alt="potentiometer" src="https://github.com/mlcourses/lab-3-blog-post-group4_cs281/assets/67582698/aba7d6c0-2065-4ab3-b646-db3e23e3ddfe">

## Part 2: Potentiometer with Arduino
We used the Arduino to convert the analog input of the potentiometer into a digital representation.

First, we connected the potentiometer to the Arduino to calibrate it. 

We wrote the included program into our Arduino, and then began to test it by turning the knob of the potentiometer. As we turned the knob, we saw on our computer that the Arduino was converting it to values between 0 and 5. This was a digital output, the values 0 to 5 were actually 3 binary bits, which could be written to represent values from 0 to 7. These three binary bits are the input into our circuit which converts this binary information into its proper representation on the 7 Segment Display.

## Part 3: 7-segment display circuit
#### Goal
The goal of this part is to design construct a 7-segment circuit to get used to building complex circuits with more than one output. In this case, we have 7! Through the construction of the 7-segment circuit, we learnt how to use the same gates twice (we had multiple AND and OR gates in our Logisim designs but only used 4 when physically building the circuit). Being able to build this circuit means we are one step closer to building more complex circuits.

#### Project Steps

A 7 segment circuit is basically 7 separate LED lights (which we number 1-7) that turn on and off based on different inputs. We then code these numbers into 3-bit binary numbers (1 = 001, 2 = 010, etc.) and make a truth table for each LED light corresponding to each variation of these bits. The truth table would look like the following:

<img width="678" alt="truth table" src="https://github.com/mlcourses/lab-3-blog-post-group4_cs281/assets/67582698/c53a92bc-b7bb-4bd3-85e4-127958b359b0">

From this truth table, we then wrote Sum of Product (SOP) expression for each LED segment. SOP expressions are a combination of possible inputs that would result in the light turning on and combines these inputs using the OR operators. They are then simplified, either by using boolean algebra rules or by K-maps, and are then used to construct circuits. For example, the SOP expression for LED light B will be:

<img width="357" alt="SOP for LED B" src="https://github.com/mlcourses/lab-3-blog-post-group4_cs281/assets/67582698/e5f152ec-bbcf-4968-8cd6-74936cf04120">

<img width="433" alt="Kmap for LEDB" src="https://github.com/mlcourses/lab-3-blog-post-group4_cs281/assets/67582698/a8a01939-d7b4-4026-9b88-42354d0c80f8">

We then create simple circuits that satisfy each simplified equations and then combine these simple circuits in Logisim to create a larger circuit that only uses the three inputs. Because these circuits are combined, there would be a total of 7 outputs from this circuit, each connected to one leg of the 7-segment display. The Logisim diagram would look something like this:

<img width="812" alt="Untitled" src="https://github.com/mlcourses/lab-3-blog-post-group4_cs281/assets/67582698/5ec7c965-f084-4d07-a5d3-0c4d0bcb6304">

We then transformed the Logisim diagram into a wiring diagram. There is no functional difference between these diagrams, though a wiring diagram more realistically represents the number of gates needed to construct a circuit (since, for example an a 7408 AND gate actually has 4 sets of inputs and outputs). Therefore, we can minimize the amount of chips used in the circuit by planning ahead. this also makes circuit construction easier because if the wiring diagram is drawn correctly, we can just look at each “leg” of the gate and plug in the correct input without having to think. This is the result of our wiring diagram:

<img width="1018" alt="wiring diagram" src="https://github.com/mlcourses/lab-3-blog-post-group4_cs281/assets/67582698/064c6ae8-705b-4092-8b39-d71d82881a46">

After the wiring diagram is complete, we got onto the construction of the circuit. Combining it with our Arduino and potentiometer setup from part 2, we were able to get the three inputs we needed to form the 3-bit number and we ended up with the following circuit:

![IMG_7598](https://github.com/mlcourses/lab-3-blog-post-group4_cs281/assets/67582698/c275ed26-1d4d-4494-9e78-ba8114d55bef)


#### Testing

After we constructed our circuit, we tested it with the potentiometer. While it was probably wiser to test each LED segment, we decided to construct the entire thing before testing it. The potentiometer starts off at 0 and it changes to 1, 2, 3, 4 and 5 after the knob is turned little by little. Our 7-segment display reflects this. The video below shows the arduino output as the knob is turned and how our 7-segment circuit responds to the arduino output.

https://github.com/mlcourses/lab-3-blog-post-group4_cs281/assets/67582698/ef681913-2d08-4804-b85d-348c54bdca82

## Conclusion
Through this lab. we learnt the concept of a voltage divider, understood what a potentiometer does and finally integrating it into a circuit and displaying the output of a potentiometer using a complex circuit that powers 7-segment display.





