# TASK-5
# PROJECT :- OBJECT DISTANCE DETECTOR & DISPLAY IT ON I2C LCD





# OVERVIEW

The Object Detector project integrates an ultrasonic sensor with the CH32V003 RISC-V processor to detect nearby objects. 
 An ultrasonic sensor measures the distance to an object by emitting ultrasonic waves and calculating the time it takes for the waves to return after bouncing off the object. This time is then converted into a distance measurement.The I2C LCD display allows for efficient communication between the microcontroller and the display, enabling the system to present the measured distance or object detection status.

![Screenshot 2025-02-16 165033](https://github.com/user-attachments/assets/e1e6dfbd-3ea4-4152-bbd3-586de31eb6fe)

# Components Required:

Microcontroller: CH32V003F4U6


Ultrasonic Sensor: HC-SR04

I2C LCD Display: 16x2

Jumper Wires

Breadboard


# HARDWARE CONNECTION

# Pin Connections:

# Ultrasonic Sensor (HC-SR04) Connections:

VCC: Connect to 5V power supply on VSDSquadron Mini


GND: Connect to ground on VSDSquadron Mini


TRIG PIN to PA1 on VSDSquadron Mini


ECHO PIN to PA2 on VSDSquadron Mini



# I2C LCD Display Connections:

VCC: Connect to 5V power supply


GND: Connect to ground


SDA: Connect to GPIO pin to PC1


SCL: Connect to GPIO pin to PC2

# Connected Circuit
![WhatsApp Image 2025-02-17 at 9 23 47 PM](https://github.com/user-attachments/assets/2b392dbe-5ae1-4cc0-8948-a8c1445bfa22)

# CODE

#include <ch32v00x.h>

#include <debug.h>

#include <stdio.h>

#define I2CLCD_H

#include "i2clcd.h"


#define LCD_ADDRESS 0x27

#define TRIG_PIN  GPIO_Pin_1  // PA1 - Trigger

#define ECHO_PIN  GPIO_Pin_2  // PA2 - Echo

#define GPIO_Pin_9  (1 << 9)

#define GPIO_Pin_10 (1 << 10)



// Function prototypes
void Ultrasonic_Init(void);

uint32_t Measure_Distance();

void DelayUs(uint32_t us);

void DelayMs(uint32_t ms);

void Ultrasonic_Init(void) {

    GPIO_InitTypeDef GPIO_InitStruct;

    RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOA, ENABLE);

    // Configure TRIG pin as Output
    
    GPIO_InitStruct.GPIO_Pin = TRIG_PIN;
    
    GPIO_InitStruct.GPIO_Mode = GPIO_Mode_Out_PP;
    
    GPIO_InitStruct.GPIO_Speed = GPIO_Speed_50MHz;
    
    GPIO_Init(GPIOA, &GPIO_InitStruct);

    // Configure ECHO pin as Input
    
    GPIO_InitStruct.GPIO_Pin = ECHO_PIN;
    
    GPIO_InitStruct.GPIO_Mode = GPIO_Mode_IN_FLOATING;
    
    GPIO_Init(GPIOA, &GPIO_InitStruct);
}

uint32_t Measure_Distance() {
    uint32_t time, distance;

    // Send Trigger Pulse
    GPIO_ResetBits(GPIOA, TRIG_PIN);
    DelayUs(2);
    GPIO_SetBits(GPIOA, TRIG_PIN);
    DelayUs(10);
    GPIO_ResetBits(GPIOA, TRIG_PIN);

    // Wait for Echo to go HIGH
    while (GPIO_ReadInputDataBit(GPIOA, ECHO_PIN) == 0);
    
    // Measure pulse duration
    time = 0;
    while (GPIO_ReadInputDataBit(GPIOA, ECHO_PIN) == 1) {
        time++;
        DelayUs(1);
    }

    // Convert to distance (cm)
    distance = (time * 0.0343) / 2;
    return distance;
}

void USART1_Init(void) {

    GPIO_InitTypeDef GPIO_InitStruct;
    
    USART_InitTypeDef USART_InitStruct;
    
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOA | RCC_APB2Periph_USART1, ENABLE);

    // Configure PA9 (TX) as alternate function push-pull
    GPIO_InitStruct.GPIO_Pin = GPIO_Pin_9;
    GPIO_InitStruct.GPIO_Mode = GPIO_Mode_AF_PP;
    GPIO_InitStruct.GPIO_Speed = GPIO_Speed_50MHz;
    GPIO_Init(GPIOA, &GPIO_InitStruct);

    // Configure PA10 (RX) as input floating
    GPIO_InitStruct.GPIO_Pin = GPIO_Pin_10;
    GPIO_InitStruct.GPIO_Mode = GPIO_Mode_IN_FLOATING;
    GPIO_Init(GPIOA, &GPIO_InitStruct);

    USART_InitStruct.USART_BaudRate = 115200;
    USART_InitStruct.USART_WordLength = USART_WordLength_8b;
    USART_InitStruct.USART_StopBits = USART_StopBits_1;
    USART_InitStruct.USART_Parity = USART_Parity_No;
    USART_InitStruct.USART_Mode = USART_Mode_Rx | USART_Mode_Tx;
    USART_InitStruct.USART_HardwareFlowControl = USART_HardwareFlowControl_None;
    USART_Init(USART1, &USART_InitStruct);
    
    USART_Cmd(USART1, ENABLE);
}

void USART1_SendString(char *str) {

    while (*str) {
    
        USART_SendData(USART1, *str++);
        
        while (USART_GetFlagStatus(USART1, USART_FLAG_TXE) == RESET);
    }
}

int main(void) {
    SystemInit();
    Ultrasonic_Init();
    USART1_Init();
    I2C_LCD_Init();

    LCD_Clear();
    LCD_SetCursor(0, 0);
    LCD_Print("Ultrasonic Sensor");

    while (1) {
        uint32_t distance = Measure_Distance();
        
        char buffer[20];
        sprintf(buffer, "Distance: %d cm", distance);

        // Print to LCD
        LCD_Clear();
        LCD_SetCursor(0, 0);
        LCD_Print("Distance:");
        LCD_SetCursor(0, 1);
        LCD_Print(buffer);

        // Print to Serial (for debugging)
        USART1_SendString(buffer);
        USART1_SendString("\n");

        DelayMs(500);
    }
}

// Microsecond delay function

void DelayUs(uint32_t us) {

    for (volatile uint32_t i = 0; i < us * 10; i++);
}

// Millisecond delay function

void DelayMs(uint32_t ms) {

    for (volatile uint32_t i = 0; i < ms * 10000; i++);
}


// Function Declarations

void lcdInit();

void setCursor(uint8_t col, uint8_t row);

void printLCD(const char* str);

void clear(); // Add this line for clear function

// Internal Functions

void lcdCommand(uint8_t cmd);

void sendI2C(uint8_t data, uint8_t mode);

void writeNibble(uint8_t nibble);
