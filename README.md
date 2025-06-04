# AT89S52_Microcontroller

__1. Title: LED Blinking using AT89C51 Microcontroller__

_Objective:_ To interface an LED with the AT89C51 microcontroller and create a basic embedded application that continuously toggles the LED state (ON/OFF) with a 1-second delay, demonstrating GPIO control and delay implementation using nested loops.

__Hardware Connection:__
 - Microcontroller: AT89C51 / AT89S52
 - LED Connection:
    - Anode (longer leg) of LED → P1.7 (pin 17) of AT89C51
    - Cathode (shorter leg) of LED → 330Ω resistor → GND
 - Power Supply: 5V regulated

__Software Simulation:__

__Hardware Simulation:__

__code:__
```
#include <reg51.h>
sbit LED = P1^7;
void delay_s(unsigned int seconds)
{
    unsigned int i, j;
    while(seconds--)
    {
        for(i=0; i<1275; i++)
				for(j=0; j<100; j++);
    }
}
void main(void)
{
    while(1)
    {
        LED = 1;
        delay_s(1);
        LED = 0;
        delay_s(1);
    }
}
```
__________________________________________________________________________________________________________________________________________________________________

__2. Title: Traffic Light Signal Simulation using AT89S52 Microcontroller__

_Objective:_ To simulate a traffic light system using three LEDs (Red, Yellow, and Green) interfaced with the AT89S52 microcontroller. The system cycles through the traffic signals with a 5-second delay for each color, demonstrating GPIO control and time-based state transitions in embedded systems.

__Hardware Connection:__
Component	Connection Detail
 - Red LED	Anode → P1.0 (Pin 1), Cathode → 330Ω → GND
 - Yellow LED	Anode → P1.1 (Pin 2), Cathode → 330Ω → GND
 - Green LED	Anode → P1.2 (Pin 3), Cathode → 330Ω → GND
 - Power	VCC = 5V, GND = 0V
 - Clock	11.0592 MHz Crystal + 2x33pF capacitors
 - Reset	Pull-up via 10kΩ resistor + capacitor

__Software simulation:__


__Hardware Simulation:__


__code:__
```
#include <reg51.h>
sbit RED_LED = P1^0;
sbit YELLOW_LED = P1^1;
sbit GREEN_LED = P1^2;
void delay_ms(unsigned int ms)
{
    unsigned int i, j;
    for(i = 0; i < ms; i++)
        for(j = 0; j < 127; j++);
}
void main(void)
{
    while(1)
    {
        RED_LED = 1;
        YELLOW_LED = 0;
        GREEN_LED = 0;
        delay_ms(5000);
        RED_LED = 0;
        YELLOW_LED = 1;
        GREEN_LED = 0;
        delay_ms(5000);
        RED_LED = 0;
        YELLOW_LED = 0;
        GREEN_LED = 1;
        delay_ms(5000);
    }
}
```
_________________________________________________________________________________________________________________________________________________________________

__3.Title: Running LED Pattern Display using AT89S52 Microcontroller__

_Objective:_ To create a running LED pattern on Port 1 (P1) of the AT89S52 microcontroller using bitwise shifting logic, demonstrating how to control multiple LEDs simultaneously via port programming and simulate binary count-based LED effects.

__Hardware Connection:__
Component	Connection Detail
 - 8 LEDs	Anodes → P1.0 to P1.7 (Pins 1 to 8) of AT89S52
 - Cathodes → 330Ω resistors → GND
 - Power Supply	VCC = 5V, GND = 0V
 - Other	Crystal (11.0592 MHz), Capacitors (33pF), Reset circuit

__Software Simulation:__


__Hardware Simulation:__

__Code:__
```
#include <reg51.h>
#define LED_PORT P1

void delay_ms(unsigned int ms)
{
    unsigned int i, j;
    for(i = 0; i < ms; i++)
        for(j = 0; j < 127; j++);
}

void main(void)
{
    unsigned char i;
    while(1)
    {
        for(i = 1; i <= 255; i++)
        {
            LED_PORT = ~i; // Active LOW for common cathode LEDs
            delay_ms(100);
        }
    }
}
```
__________________________________________________________________________________________________________________________________________________________________

