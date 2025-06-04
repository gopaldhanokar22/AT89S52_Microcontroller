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

__4. Title: Random Dice Value Display on LEDs using AT89S52 Microcontroller__

_Objective:_ To simulate a dice roll using 3 LEDs connected to AT89S52 microcontroller. Each second, a random number from 1 to 6 is generated and its binary representation is displayed using 3 LEDs. This demonstrates the use of rand(), bit masking, and GPIO control.

__Hardware Connection:__
Component	             Connection
- LED1	        Anode → P1.0 (pin 1), Cathode → 330Ω → GND
- LED2	        Anode → P1.1 (pin 2), Cathode → 330Ω → GND
- LED3          Anode → P1.2 (pin 3), Cathode → 330Ω → GND
- Power Supply	VCC = +5V, GND = 0V
- Clock	11.0592 MHz crystal + 2 × 33pF capacitors
- Reset Circuit	10kΩ resistor + 10µF capacitor

__Software Simulation:__

__Hardware Simulation:__

__code:__
```
#include <reg51.h>
#include <stdlib.h>

sbit LED1 = P1^0;
sbit LED2 = P1^1;
sbit LED3 = P1^2;

void delay_ms(unsigned int ms)
{
    unsigned int i, j;
    for(i = 0; i < ms; i++)
        for(j = 0; j < 127; j++);
}

void main(void)
{
    unsigned char faceVal;
    unsigned int seed = 0;

    while(1)
    {
        faceVal = (rand() % 6) + 1;
        P1 = (P1 & 0xF8) | (~faceVal & 0x07); // Clear P1.0 to P1.2, then write inverted dice value
        delay_ms(1000);
        srand(seed++);
    }
}
```
_____________________________________________________________________________________________________________________
__5. Title: Switch-Controlled LED Using AT89S52 Microcontroller__

_Objective:_ To interface a push-button switch and an LED with the AT89S52 microcontroller. The LED turns ON when the switch is pressed and OFF when it is released. This demonstrates basic digital input and output control using GPIO pins.

__Hardware Connection:__
Component        Connection Description
- Switch (SW) One terminal → P1.0 (pin 1) of AT89S52
- Other terminal → GND
- Use 10kΩ pull-up resistor between P1.0 and VCC
- LED (Active LOW) Anode → +5V
- Cathode → P1.4 (pin 5) via 330Ω resistor
- Power Supply VCC = +5V, GND = 0V
- Crystal 11.0592 MHz + 2 × 33pF capacitors
- Reset Circuit	10kΩ resistor + 10µF capacitor

__Hardware Simulation:__

__Software Simulation:__

__Code:__
```
#include <reg51.h>
sbit SW = P1^0;
sbit LED = P1^4;

void main(void)
{
    while(1)
    {
        if(SW == 0)
            LED = 0;
        else
            LED = 1;
    }
}
```
________________________________________________________________________________________________________________________________________________
__6. Title: Dual Switch-Controlled LED Using AT89S52 Microcontroller__

_Objective:_ To interface two push-button switches and one LED with the AT89S52 microcontroller. The LED turns ON if any one of the switches is pressed. This project demonstrates multiple digital input handling using logical OR (||) and control of a digital output.

__Hardware Connection:__
Component Connection Description
 - Switch 1 (SW1) One terminal → P1.0 (pin 1)
 - Other terminal → GND
 - 10kΩ pull-up resistor between P1.0 and VCC
 - Switch 2 (SW2) One terminal → P1.1 (pin 2)
 - Other terminal → GND
 - 10kΩ pull-up resistor between P1.1 and VCC
 - LED (Active LOW) Anode → +5V
 - Cathode → P1.4 (pin 5) via 330Ω resistor
 - Power Supply	VCC = +5V, GND = 0V
 - Crystal Oscillator 11.0592 MHz + 2 × 33pF capacitors
 - Reset Circuit 10kΩ resistor + 10µF capacitor

__Hardware Simulation:__


__Software Simulation:__

__Code:__
```
#include <reg51.h>
sbit SW1 = P1^0;
sbit SW2 = P1^1;
sbit LED = P1^4;

void main(void)
{
    while(1)
    {
        if(SW1 == 0 || SW2 == 0)
            LED = 0;
        else
            LED = 1;
    }
}
```
_________________________________________________________________________________________________________________________________
__7. Title: 4 Switches Controlling 4 LEDs Using AT89S52 Microcontroller__

Objective:
To interface four push-button switches with four individual LEDs such that each switch controls one LED. This demonstrates basic one-to-one digital input-output mapping using GPIO pins in embedded C.

Hardware Connection (AT89S52):
Component	Connection Description
SW1	One terminal → P1.0 (pin 1)
Other terminal → GND
10kΩ pull-up resistor between P1.0 and VCC
SW2	One terminal → P1.1 (pin 2)
Other terminal → GND
10kΩ pull-up resistor between P1.1 and VCC
SW3	One terminal → P1.2 (pin 3)
Other terminal → GND
10kΩ pull-up resistor between P1.2 and VCC
SW4	One terminal → P1.3 (pin 4)
Other terminal → GND
10kΩ pull-up resistor between P1.3 and VCC
LED1	Anode → +5V, Cathode → P1.4 (pin 5) via 330Ω resistor
LED2	Anode → +5V, Cathode → P1.5 (pin 6) via 330Ω resistor
LED3	Anode → +5V, Cathode → P1.6 (pin 7) via 330Ω resistor
LED4	Anode → +5V, Cathode → P1.7 (pin 8) via 330Ω resistor
Power Supply	VCC = +5V, GND = 0V
Crystal Oscillator	11.0592 MHz + 2 × 33pF capacitors
Reset Circuit	10kΩ resistor + 10µF capacitor
