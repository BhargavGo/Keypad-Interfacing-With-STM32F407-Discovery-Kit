

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

1. Delay Function:
   - This delay function is used to create a small time interval (debouncing) when a keypress is detected. In mechanical keypads, bouncing can occur when a key is pressed, which can lead to multiple 
     false detections. The delay prevents that by adding a short pause.
   
            void delay(void) {
             for (uint32_t i = 0; i < 300000; i++);
            }

   
2. Key Detection:
    - The program uses specific addresses to directly interact with the STM32 GPIO registers. These addresses are defined in the code as follows:

             uint32_t volatile *const pGPIODModeReg  = (uint32_t*)(0x40020C00);     // GPIO Mode Register
             uint32_t volatile *const pInPutDataReg  = (uint32_t*)(0x40020C00 + 0x10); // GPIO Input Data Register
             uint32_t volatile *const pOutPutDataReg = (uint32_t*)(0x40020C00 + 0x14); // GPIO Output Data Register
             uint32_t volatile *const pClockCtrlReg  = (uint32_t*)(0x40023800 + 0x30); // Clock Control Register
             uint32_t volatile *const pPullupDownReg = (uint32_t*)(0x40020C00 + 0x0C); // Pull-up/Pull-down Register

    - These registers control the configuration and behavior of the GPIO pins for Port D on the STM32F407. The base address for GPIOD is 0x40020C00.
      
3. Clock Signal:
   
    - Before interacting with GPIO pins, the peripheral clock for GPIOD must be enabled.

            *pClockCtrlReg |= (1 << 3);

4. GPIO Pin Configuration :

   a. Configuring PD0-PD3 as Output (Rows)

        *pGPIODModeReg &= ~(0xFF); // Clear mode bits for PD0-PD3
        *pGPIODModeReg |= 0x55;   // Set PD0-PD3 as output (01 for each pin)

    - The GPIO mode register configures the behavior of each pin.
      
    - &= ~(0xFF) clears the mode bits for pins PD0 to PD3.
      
    - |= 0x55 sets these pins as outputs by configuring 2 bits for each pin as 01 (which corresponds to output mode in STM32).

   b. Configuring PD8-PD11 as Input (Columns)

        *pGPIODModeReg &= ~(0xFF << 16);
   
     - The same mode register is modified to configure PD8-PD11 as input pins by clearing their mode bits. No need to set them, as the reset value for these bits corresponds to input mode (00).

5. Pull-up Resistors for Columns:

       *pPullupDownReg &= ~(0xFF << 16);  // Clear
       *pPullupDownReg |=  (0x55 << 16);  // Enable pull-up resistors for PD8-PD11

     - The Pull-up/Pull-down register enables internal pull-up resistors for the input pins PD8-PD11.
       
     - This prevents floating inputs when no button is pressed, ensuring stable high readings when no key is pressed.
       
6. Keypad Scanning:

     The keypad consists of rows (connected to PD0-PD3) and columns (connected to PD8-PD11). To detect which key is pressed, the program sequentially makes each row low and checks which column goes 
     low. This corresponds to a specific key press.

     a. Making All Rows High

       *pOutPutDataReg |= 0x0f;

     - This sets all rows (PD0-PD3) to a high state before starting the scan.

     b. Scanning Each Row
   
      For each row, the program sets one of the row pins low and checks the state of the column pins.

      Example for Row 1 (PD0):

       *pOutPutDataReg &= ~(1 << 0);  // Set PD0 (R1) low

      - Row 1 (PD0) is set low while the other rows remain high.
        
      - Then, it checks each column to see if it has gone low, indicating a key press.

     c. Checking Columns:

       if (!(*pInPutDataReg & (1 << 8))) {
           delay();
           printf("1\n");
       }
   
      - The program checks if column C1 (PD8) is low.
        
      - If PD8 is low, key 1 (which corresponds to Row 1 and Column 1) is pressed. A short delay is added to debounce, and the result is printed.
        
     d. Repeating for Other Rows:
   
      - After scanning Row 1, the program sets Row 2 (PD1) low and repeats the process for columns, and so on for Row 3 (PD2) and Row 4 (PD3).

7. Debouncing:
   
      - The delay() function is called after each detection to ensure that mechanical bouncing of the keypad doesn't cause false detections.


### **Keypad Layout Corresponding to the Program:**
![KeypadInterfacing](https://github.com/user-attachments/assets/9f43bada-9755-48a8-b3ac-e141686fe3cd)


        
