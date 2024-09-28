

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
1.Low-Level Register Manipulation:Configuring GPIO pins and reading input/output values using direct register access.

2.Row-Column Scanning: Sequentially activating rows and checking columns to detect which key is pressed.

3.Debouncing:Implemented with a simple delay to prevent multiple detections from one keypress.

### **Technologies Used**

1. Embedded C:
    - Low-level programming for register control.
      
2. STM32F407 Discovery Board:
    - ARM Cortex-M4-based microcontroller.
  
### **Programming Details :**

1. GPIO Configuration:
   
    - GPIOD pins PD0-PD3 are configured as output for rows, and PD8-PD11 are set as input for columns.
   
2. Key Detection:
    
    - Rows are sequentially driven low, and the program checks if any column goes low to detect a key press.

3. Debouncing:
   
    - A simple for-loop-based delay is used to avoid bouncing effects common in mechanical keypads.

This project provides a foundational understanding of how to control hardware through software, serving as an introductory step
