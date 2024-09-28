

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

1. Delay Function
   
       -   void delay(void) {
             for (uint32_t i = 0; i < 300000; i++);
            }

   
3. Key Detection:
    - The program uses specific addresses to directly interact with the STM32 GPIO registers. These addresses are defined in the code as follows:

          -  uint32_t volatile *const pGPIODModeReg  = (uint32_t*)(0x40020C00);     // GPIO Mode Register
             uint32_t volatile *const pInPutDataReg  = (uint32_t*)(0x40020C00 + 0x10); // GPIO Input Data Register
             uint32_t volatile *const pOutPutDataReg = (uint32_t*)(0x40020C00 + 0x14); // GPIO Output Data Register
             uint32_t volatile *const pClockCtrlReg  = (uint32_t*)(0x40023800 + 0x30); // Clock Control Register
             uint32_t volatile *const pPullupDownReg = (uint32_t*)(0x40020C00 + 0x0C); // Pull-up/Pull-down Register

    - These registers control the configuration and behavior of the GPIO pins for Port D on the STM32F407. The base address for GPIOD is 0x40020C00.
      
4. Debouncing:
   
    - A simple for-loop-based delay is used to avoid bouncing effects common in mechanical keypads.

This project provides a foundational understanding of how to control hardware through software, serving as an introductory step
