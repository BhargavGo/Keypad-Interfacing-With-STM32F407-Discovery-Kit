

Name: BHARGAV GORIVALE

Company: FastBit Embedded Brain Academy

Domain : Embedded Systems

Duration : Sept 2024

Mentor : Kiran Nayak

# **Overview of the Project**

## **Project :  Keypad Interfacing With STM32F407 Discovery-Kit**

### **Objective**
The project interfaces a 4x4 matrix keypad with the STM32F407 Discovery Board, scanning rows and columns to detect key presses, without using the HAL library.

### **Key Activities**
Low-Level Register Manipulation:

Configuring GPIO pins and reading input/output values using direct register access.

Row-Column Scanning: 

Sequentially activating rows and checking columns to detect which key is pressed.

Debouncing:

Implemented with a simple delay to prevent multiple detections from one keypress.

### **Technologies Used**

1. Arduino Platform:
    - Arduino Board: A microcontroller board with a built-in LED, typically connected to digital pin 13.
    - Arduino IDE: The integrated development environment used to write, compile, and upload code to the Arduino board.
      
2. Programming Languages:
    - C++ : The programming languages used to write the Arduino sketch.

This project provides a foundational understanding of how to control hardware through software, serving as an introductory step
