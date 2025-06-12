# AT89S52_Microcontroller


## INDEX
1. Title: LED Blinking using AT89C51 Microcontroller
2. Title: Traffic Light Signal Simulation using AT89S52 Microcontroller
3. Title: Running LED Pattern Display using AT89S52 Microcontroller
4. Title: Random Dice Value Display on LEDs using AT89S52 Microcontroller
5. Title: Switch-Controlled LED Using AT89S52 Microcontroller
6. Title: Dual Switch-Controlled LED Using AT89S52 Microcontroller
7. Title: 4 Switches Controlling 4 LEDs Using AT89S52 Microcontroller
8. Title: Single Digit Up Counter using Common Anode 7-Segment Display with AT89S52
9. Title: Digital Clock Simulation on 7-Segment Display Using AT89S52
10. Title: Static 4-Digit Number Display Using AT89S52 and 7-Segment Display
11. Title: Floating Point Number Display on 4-Digit 7-Segment Using AT89S52
12. Title: Scrolling Message Display on 4-Digit 7-Segment Using AT89S52
13. Title: LCD 16*2 Data Display with CGRAM and Multiple Formats Using AT89S52
14. Title: Alphabet Display with ASCII Values on LCD Using AT89S52
15. Title: Electronic Dice Simulation on LCD Using AT89S52
16. Title: Oscillating Message Display on 16x2 LCD Using AT89S52
17. Title: Fastest Finger First Timer Display on LCD Using AT89S52
18. Title: 4x3 Matrix Keypad Interface with 16x2 LCD on AT89S52
19. Title: Name Entry System Using 4x4 Keypad and 16x2 LCD on AT89C51
20. Title: LCD 20*4 Data Display with CGRAM and Multiple Formats Using AT89S52

_________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
__1. Title: LED Blinking using AT89C51 Microcontroller__

_Objective:_ To interface an LED with the AT89C51 microcontroller and create a basic embedded application that continuously toggles the LED state (ON/OFF) with a 1-second delay, demonstrating GPIO control and delay implementation using nested loops.

__Hardware Connection:__
 - Microcontroller: AT89C51 / AT89S52
 - LED Connection:
    - Anode (longer leg) of LED → P1.7 (pin 17) of AT89C51
    - Cathode (shorter leg) of LED → 330Ω resistor → GND
 - Power Supply: 5V regulated

__Software Simulation:__

![image](https://github.com/user-attachments/assets/1ffae2bc-d220-4d94-a222-3bbf385a764e)

__Hardware Simulation:__

![WhatsApp Image 2025-06-12 at 23 15 24_cf193dcc](https://github.com/user-attachments/assets/f2232657-d82c-4c6e-a870-109d01b193ad)

![WhatsApp Image 2025-06-12 at 23 15 25_830fc9ca](https://github.com/user-attachments/assets/77c44f7d-ff26-48fc-bea7-dd98ca4c5d19)


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

![image](https://github.com/user-attachments/assets/bbc1f86d-8192-46db-b0b2-5bb2e50e38b8)

__Hardware Simulation:__

![WhatsApp Image 2025-06-12 at 23 16 29_cd1ac0a0](https://github.com/user-attachments/assets/726c15c0-c47a-4aaa-80a4-850040246631)

![WhatsApp Image 2025-06-12 at 23 16 28_76ffa8c0](https://github.com/user-attachments/assets/efd4d704-6461-4d02-b6eb-a5d9e7a4fd4f)

![WhatsApp Image 2025-06-12 at 23 16 28_53e88ce0](https://github.com/user-attachments/assets/2573e8ee-83b2-4cbb-868b-a1cf2153b54e)

![WhatsApp Image 2025-06-12 at 23 16 28_8acdf19f](https://github.com/user-attachments/assets/29dd3a8d-6855-4dd1-b7fc-2f5531c035d0)


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

![image](https://github.com/user-attachments/assets/3ad72640-7900-4cd2-bdac-3d226c0e2443)

__Hardware Simulation:__

![WhatsApp Image 2025-06-12 at 23 18 22_075816db](https://github.com/user-attachments/assets/117bb831-9d72-4937-b17a-a8869643c0df)

![WhatsApp Image 2025-06-12 at 23 18 22_541856d2](https://github.com/user-attachments/assets/28eadc8a-2ba2-4841-93fa-1c8b9867a643)

![WhatsApp Image 2025-06-12 at 23 18 23_e26c1e72](https://github.com/user-attachments/assets/275569d8-fb54-4d3c-a3cb-5fa736626fbf)


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

![image](https://github.com/user-attachments/assets/d5e5848d-0434-4a44-91d3-f11d5cf569f5)

__Hardware Simulation:__

![Screenshot 2025-06-12 232143](https://github.com/user-attachments/assets/7b0616b5-cb60-45ec-a405-38ba59c9f04b)

![Screenshot 2025-06-12 232203](https://github.com/user-attachments/assets/0d32ff5a-e97b-41e7-a00a-dcd1535406f6)

![Screenshot 2025-06-12 232219](https://github.com/user-attachments/assets/fae6bbbe-a572-4d00-bc81-cf385bb2fe27)


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
Component Connection Description
- Switch (SW)
- One terminal → P1.0 (pin 1) of AT89S52
- Other terminal → GND

- Use 10kΩ pull-up resistor between P1.0 and VCC
- LED (Active LOW) Anode → +5V
- Cathode → P1.4 (pin 5) via 330Ω resistor
- Power Supply VCC = +5V, GND = 0V
- Crystal 11.0592 MHz + 2 × 33pF capacitors
- Reset Circuit	10kΩ resistor + 10µF capacitor

__Software Simulation:__

![image](https://github.com/user-attachments/assets/240e1162-0cf4-4bd0-8b41-47a056391d18)

__Hardware Simulation:__

![WhatsApp Image 2025-06-12 at 23 20 15_d4004a4d](https://github.com/user-attachments/assets/d2603936-5108-4ef8-bb0e-abdf01202923)

![WhatsApp Image 2025-06-12 at 23 20 16_c3dc15d4](https://github.com/user-attachments/assets/7e744362-5ed1-4437-b6b8-a7879aba61e1)


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
 - Switch 1 (SW1)
	 - One terminal → P1.0 (pin 1)
	 - Other terminal → GND
	 - 10kΩ pull-up resistor between P1.0 and VCC
 - Switch 2 (SW2)
	 - One terminal → P1.1 (pin 2)
	 - Other terminal → GND
	 - 10kΩ pull-up resistor between P1.1 and VCC
 - LED (Active LOW) Anode → +5V
 - Cathode → P1.4 (pin 5) via 330Ω resistor
 - Power Supply	VCC = +5V, GND = 0V
 - Crystal Oscillator 11.0592 MHz + 2 × 33pF capacitors
 - Reset Circuit 10kΩ resistor + 10µF capacitor

__Software Simulation:__

![image](https://github.com/user-attachments/assets/a46de680-f382-4ca4-bd07-f8f6e8553a0d)

__Hardware Simulation:__

![WhatsApp Image 2025-06-12 at 23 24 17_3a0ce9bc](https://github.com/user-attachments/assets/0c834b92-c3aa-40bf-92a2-cc263cd23b59)

![WhatsApp Image 2025-06-12 at 23 24 17_ffe858e4](https://github.com/user-attachments/assets/f209733f-304d-496c-ba33-13e5e53261d9)

![WhatsApp Image 2025-06-12 at 23 24 18_41787b4f](https://github.com/user-attachments/assets/e9b766d9-d1f2-4795-aa67-f36444a4d000)


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

_Objective:_ To interface four push-button switches with four individual LEDs such that each switch controls one LED. This demonstrates basic one-to-one digital input-output mapping using GPIO pins in embedded C.

__Hardware Connection:__
Component	Connection Description
 - SW1
	 - One terminal → P1.0 (pin 1)
	 - Other terminal → GND
	 - 10kΩ pull-up resistor between P1.0 and VCC
 - SW2
	 - One terminal → P1.1 (pin 2)
	 - Other terminal → GND
	 - 10kΩ pull-up resistor between P1.1 and VCC
 - SW3
	 - One terminal → P1.2 (pin 3)
	 - Other terminal → GND
	 - 10kΩ pull-up resistor between P1.2 and VCC
 - SW4
	 - One terminal → P1.3 (pin 4)
	 - Other terminal → GND
	 - 10kΩ pull-up resistor between P1.3 and VCC

 - LED1	Anode → +5V, Cathode → P1.4 (pin 5) via 330Ω resistor
 - LED2	Anode → +5V, Cathode → P1.5 (pin 6) via 330Ω resistor
 - LED3	Anode → +5V, Cathode → P1.6 (pin 7) via 330Ω resistor
 - LED4	Anode → +5V, Cathode → P1.7 (pin 8) via 330Ω resistor
 - Power Supply	VCC = +5V, GND = 0V
 - Crystal Oscillator 11.0592 MHz + 2 × 33pF capacitors
 - Reset Circuit 10kΩ resistor + 10µF capacitor

__Software Simulation:__

![image](https://github.com/user-attachments/assets/79c27f79-5775-4d24-9c00-fe411439036b)

__Hardware Simulation:__

![WhatsApp Image 2025-06-12 at 23 26 06_d7101942](https://github.com/user-attachments/assets/62458dad-6c93-4b66-bbe5-4f4bd770eba1)

![WhatsApp Image 2025-06-12 at 23 26 06_d4f92be4](https://github.com/user-attachments/assets/d8963152-e92e-4175-9e01-71ff5ecd2cd0)

![WhatsApp Image 2025-06-12 at 23 26 06_706c8bf7](https://github.com/user-attachments/assets/4dffc96c-b5f1-48ce-bab6-55b45c0ad823)

![WhatsApp Image 2025-06-12 at 23 26 07_abc343c7](https://github.com/user-attachments/assets/5515c075-abd0-4cef-afe8-ce023d81d114)

![WhatsApp Image 2025-06-12 at 23 26 07_c3e31635](https://github.com/user-attachments/assets/93f6ea7c-0f60-4914-9a62-660b197f9464)


__Code:__
```
#include <reg51.h>

sbit SW1 = P1^0;
sbit SW2 = P1^1;
sbit SW3 = P1^2;
sbit SW4 = P1^3;

sbit LED1 = P1^4;
sbit LED2 = P1^5;
sbit LED3 = P1^6;
sbit LED4 = P1^7;

void main(void)
{
    while(1)
    {
        LED1 = SW1;
        LED2 = SW2;
        LED3 = SW3;
        LED4 = SW4;
    }
}
```
___________________________________________________________________________________________________________________________
__8. Title:Single Digit Up Counter using Common Anode 7-Segment Display with AT89S52__

_Objective:_ To display digits from 0 to 9 in a loop on a single-digit common anode 7-segment display using an AT89S52 microcontroller. The counter updates every second.

__Hardware Requirements:__
Microcontroller: AT89S52
7-Segment Display: Common Anode type
Resistors: 330Ω – 1kΩ (for current limiting on segment pins)
Power Supply: 5V regulated
Crystal Oscillator: 11.0592 MHz (with two 33pF capacitors)
Miscellaneous: Breadboard, jumper wires, etc.

__Hardware Connections:__
7-Segment Display to Port P1 (Data Bus):\
7-Segment Pin	Segment	Connects To	Remarks\
a	Segment A	P1.0	Through 330Ω\
b	Segment B	P1.1	Through 330Ω\
c	Segment C	P1.2	Through 330Ω\
d	Segment D	P1.3	Through 330Ω\
e	Segment E	P1.4	Through 330Ω\
f	Segment F	P1.5	Through 330Ω\
g	Segment G	P1.6	Through 330Ω\
dp	Decimal	P1.7 or GND	Not used here\
Common Anode Pins	Vcc (5V)	5V	Both anode pins to Vcc

Ensure current-limiting resistors between segment pins and microcontroller.

Microcontroller:\
Pin	Function	Remarks\
P1.0–P1.6	Segment data lines	Connect to segments a–g\
P3.x (optional)	DIG1–DIG4 selection	Not used here, only single digit\
Vcc	+5V	Power supply\
GND	Ground	Common ground\
XTAL1, XTAL2	Crystal Oscillator	11.0592 MHz with caps\

__Software Simulation:__

![image](https://github.com/user-attachments/assets/84ce61fc-712d-4453-82dc-2bbad63cd7ec)

__Hardware Simulation:__

![WhatsApp Image 2025-06-12 at 23 27 25_6afa0393](https://github.com/user-attachments/assets/4c4feef3-ae33-4a17-85d4-7a72baec524c)

![image](https://github.com/user-attachments/assets/947cfb4a-7f00-47a2-9b78-26987d3462cb)

![image](https://github.com/user-attachments/assets/e11edfb0-1bbe-4c93-a8bc-db64f6180b7d)


__code:__
```
#include <reg51.h>
#include "delay.h"
#include "segment.h"

void main() {
    u8 i;
    while(1) {
        for(i = 0; i <= 9; i++) {
            segment_display(i);
            delay_ms(1000);
        }
    }
}
```
________________________________________________________________________________________________________________
__9.Title: Digital Clock Simulation on 7-Segment Display Using AT89S52__

_Objective:_ To simulate a digital clock (MM:SS format) using 4-digit multiplexed 7-segment display on AT89S52 by displaying minutes and seconds with real-time updates.

__Hardware Connection:__
 - Microcontroller: AT89S52
 - Segment Data Lines: P0 → Connected to 7-Segment Display segment lines (a–g, dp)
 - Digit Select Lines:
	 - P2^0 → Digit 1 (Tens of Minutes)
	 - P2^1 → Digit 2 (Units of Minutes)
	 - P2^2 → Digit 3 (Tens of Seconds)
	 - P2^3 → Digit 4 (Units of Seconds)
 - Common Anode 7-Segment Displays used
 - Segment driver functions used from segment.h
 - External header delay.h handles millisecond-level delays (not shown here)
 - Power Supply: +5V
 - Pull-down resistors for segment lines (if needed)
 - Ensure proper current limiting resistors (220Ω–330Ω) between segment lines and display pins.

__Software Simulation:__

![image](https://github.com/user-attachments/assets/2513160f-d619-48b2-b4f2-d62b5645e778)

__Code:__
```
#include<reg52.h>
#include "segment.h"
main()
{
	unsigned int i,j,k;
	while(1)
	{
		for(i=0;i<60;i++)
		{
			for(j=0;j<60;j++)
			{
				for(k=0;k<100;k++)
				{
					dispi_2_mux_segs(j,0);
					dispi_2_mux_segs(i,1);
				}
			}
		}
	}
}
```
__________________________________________________________________________________________________________
__10.Title: Static 4-Digit Number Display Using AT89S52 and 7-Segment Display__

_Objective:_ To display two static 4-digit numbers alternately (1264 and 8745) on a 4-digit 7-segment multiplexed display using AT89S52.

__Hardware Connection:__
 - Microcontroller used: AT89S52
 - Segment data lines connected to: Port P0
 - Digit select lines connected to:
	 - P2.0 → sel1 (1st digit)
	 - P2.1 → sel2 (2nd digit)
	 - P2.2 → sel3 (3rd digit)
	 - P2.3 → sel4 (4th digit)
 - Display type: Common Anode 7-Segment Displays
 - Resistors (220Ω–330Ω) used between P0 and segment pins
 - Power supply: +5V DC regulated

__Software Simulation:__

![image](https://github.com/user-attachments/assets/b581dc48-5b74-4ed2-a699-b86cbc282cd2)


__Code:__
```
#include<reg52.h>
#include "segment.h"
main()
{
	unsigned int k;
	while(1)
	{
		for(k=0;k<500;k++)
			dispi_4_mux_segs(1264);

		for(k=0;k<500;k++)
			dispi_4_mux_segs(8745);
	}
}
```
________________________________________________________________________________________________________________
__11.Title: Floating Point Number Display on 4-Digit 7-Segment Using AT89S52__

_Objective:_ To display floating point numbers (1.245, 43.89, 678.7) alternately using 4-digit multiplexed 7-segment display with AT89S52.

__Hardware Connection:__
 - Microcontroller used: AT89S52
 - Segment data lines connected to: Port P0
	 - Digit select lines connected to:
	 - P2.0 → sel1 (1st digit)
	 - P2.1 → sel2 (2nd digit)
	 - P2.2 → sel3 (3rd digit)
	 - P2.3 → sel4 (4th digit)
 - Display type: Common Anode 7-Segment Displays
 - Decimal point control using dp1, dp2, dp3 variables
 - Resistors (220Ω–330Ω) between P0 and segment pins
 - Power supply: +5V DC regulated

__Software Simulation:__

![image](https://github.com/user-attachments/assets/d63c507e-900b-4f54-8651-e0fef2d8ee90)

__Code:__
```
#include<reg52.h>
#include "segment.h"
main()
{
	unsigned int k;
	while(1)
	{

		for(k=0;k<500;k++)
			dispf_4_mux_segs(1.245);
	    
		for(k=0;k<500;k++)
			dispf_4_mux_segs(43.89);
	    
		for(k=0;k<500;k++)
			dispf_4_mux_segs(678.7);
	}
}
```
_____________________________________________________________________________________________________________
__12.Title: Scrolling Message Display on 4-Digit 7-Segment Using AT89S52__

_Objective:_ To scroll the word "HELP" across a 4-digit 7-segment multiplexed display using AT89S52.

__Hardware Connection:__
 - Microcontroller used: AT89S52
 - Segment data lines connected to: Port P0
 - Digit select lines connected to:
	 - P2.0 → sel1 (1st digit)
	 - P2.1 → sel2 (2nd digit)
	 - P2.2 → sel3 (3rd digit)
	 - P2.3 → sel4 (4th digit)
 - Display type: Common Anode 7-Segment Displays

__Software Simulation:__

![image](https://github.com/user-attachments/assets/5b0440a0-4014-4cf8-b04b-f0209c6df8b8)

__Code:__
```
#include<reg52.h>
#include "segment.h"
main()
{
	while(1)
	{
		display_help_string_scroll();
	}
}
```
_______________________________________________________________________________________________________________
__13.Title: LCD 16*2 Data Display with CGRAM and Multiple Formats Using AT89S52__

_Objective:_ To demonstrate the use of 16x2 alphanumeric LCD by displaying various data formats—characters, strings, unsigned/signed integers, float, hexadecimal, octal, binary—and custom characters using CGRAM.

__Hardware Connection:__
 - RS → P2.0
 - RW → P2.1
 - EN → P2.2
 - D0–D7 (LCD Data Lines) → P1.0 to P1.7
 - VSS → GND
 - VDD → +5V
 - VEE → 10k potentiometer center pin (contrast control)
 - 10k potentiometer ends → VDD and GND
 - LCD backlight LED+ → +5V through 220Ω resistor
 - LCD backlight LED− → GND

__Software Simulation:__

![image](https://github.com/user-attachments/assets/f956f16c-d757-4529-bf78-3a5706eced93)

__Hardware Simulation:__

![Screenshot 2025-06-12 233850](https://github.com/user-attachments/assets/00ae165e-4aff-4e41-b554-d0e409244863)

![Screenshot 2025-06-12 233914](https://github.com/user-attachments/assets/2154254c-75a7-4079-9e0e-38384f747c0a)

![Screenshot 2025-06-12 233921](https://github.com/user-attachments/assets/af3eff8a-5c50-4d68-837a-3ed255bcdd23)

__Code:__
```
#include "lcd.h"
#include "lcd_defines.h"
#include "delay.h"

u8 cgramLUT[8] = {
    0x07,   
    0x04,   
    0x04,   
    0x1F,  
    0x10,   
    0x10,   
    0x10,  
    0x00    
};

void main() {
    InitLCD();                        
    delay_ms(20);
    
	BuildCGRAM(cgramLUT, 0);          
    CmdLCD(CLEAR_LCD);
    CharLCD('A');                  	
   	StrLCD(" V24HE6G2 ");                
	  delay_ms(2000);  
    
	  CmdLCD(GOTO_LINE2_POS0);        
    U32LCD(1234567890);             
    delay_ms(2000);                   

    CmdLCD(CLEAR_LCD);
    S32LCD(-1234567890);              
    CmdLCD(GOTO_LINE2_POS0);
    F32LCD(123.456789, 6);           
    delay_ms(2000);

    CmdLCD(CLEAR_LCD);
    HexLCD(256);                    
    CmdLCD(GOTO_LINE2_POS0);
    OctLCD(65);                       
    delay_ms(1000);

    CmdLCD(CLEAR_LCD);
    BinLCD(127, 16);                 
    CmdLCD(GOTO_LINE2_POS0);
    CharLCD(0);                      
    while (1);                     
}
```
____________________________________________________________________________________________________________
__14. Title: Alphabet Display with ASCII Values on LCD Using AT89S52__

_Objective:_ To display uppercase alphabets (A–Z) on a 16x2 LCD along with their corresponding ASCII values in both decimal and hexadecimal formats, using the AT89S52 microcontroller.

__Hardware Connection:__
 - RS → P2.0
 - RW → P2.1
 - EN → P2.2
 - D0–D7 (LCD Data Lines) → P1.0 to P1.7
 - VSS → GND
 - VDD → +5V
 - VEE → 10k potentiometer center pin (contrast control)
 - 10k potentiometer ends → VDD and GND
 - LCD backlight LED+ → +5V through 220Ω resistor
 - LCD backlight LED− → GND

__Software Simulation:__

![image](https://github.com/user-attachments/assets/25357598-6c18-41ac-a184-7f6a679810eb)

__Hardware Simulation:__

![Screenshot 2025-06-12 234054](https://github.com/user-attachments/assets/e1254459-705f-4af7-a03e-3646d0ce8309)

![image](https://github.com/user-attachments/assets/07d93a9c-1b5b-4095-afce-7feb4865b1c8)

__Code:__
```
#include "lcd.h"
#include "lcd_defines.h"
#include "delay.h"

void main() {
    u32 i;     
    InitLCD();           
    delay_ms(20);             
    for (i = 0; i < 26; i++) 
    {
        CharLCD('A' + i);      
	CharLCD(' ');    
        
        U32LCD('A' + i); 
        CharLCD(' ');           
        HexLCD('A' + i); 
        
        delay_ms(1000);   
        CmdLCD(CLEAR_LCD);
	delay_ms(10);
    }
    while(1);        
}
```
_________________________________________________________________________________________________________________
__15. Title: Electronic Dice Simulation on LCD Using AT89S52__

_Objective:_ To simulate a 6-faced electronic dice using the AT89S52 microcontroller. When a push-button is pressed, a pseudo-random number between 1 and 6 is generated and displayed on a 16x2 LCD.

__Hardware Connection:__
 - RS → P2.0
 - RW → P2.1
 - EN → P2.2
 - D0–D7 (LCD Data Lines) → P1.0 to P1.7
 - VSS → GND
 - VDD → +5V
 - VEE → 10k potentiometer center pin (contrast control)
 - 10k potentiometer ends → VDD and GND
 - LCD backlight LED+ → +5V through 220Ω resistor
 - LCD backlight LED− → GND

__Software Simulation:__

![image](https://github.com/user-attachments/assets/e2049737-056b-463d-a5f5-7f6575307c81)

__Hardware Simuation:__

![Screenshot 2025-06-12 234224](https://github.com/user-attachments/assets/db78959f-3a96-42c4-b6fd-03576acd2b6d)

![image](https://github.com/user-attachments/assets/310a70e5-84ab-4623-a36f-290404fa19fb)

__Code:__
```
#include <reg51.h>
#include "lcd.h"
#include "lcd_defines.h"
#include "delay.h"
#include "types.h"

sbit ROLL_SW = P3^2;

u8 lfsr = 0xAA;  // Initial seed

u8 get_random_6() {
    u8 fb = ((lfsr >> 0) ^ (lfsr >> 2) ^ (lfsr >> 3) ^ (lfsr >> 5)) & 1;
    lfsr = (lfsr >> 1) | (fb << 7);
    return (lfsr % 6) + 1;
}

void main() {
    u8 faceVal = 1;
    u8 prev_sw = 1;

    InitLCD();
    delay_ms(20);
    StrLCD("Electronic Dice");

    while(1) {
        CmdLCD(GOTO_LINE2_POS0);
        U32LCD(faceVal);

        if (ROLL_SW == 0 && prev_sw == 1) {
            delay_ms(20); // debounce
            if (ROLL_SW == 0) {
                faceVal = get_random_6();
            }
        }
        prev_sw = ROLL_SW;
    }
}
```
_______________________________________________________________________________________________________________
__16. Title: Oscillating Message Display on 16x2 LCD Using AT89S52__

_Objective:_ To continuously scroll a static message ("GOPAL") from left to right and then right to left on a 16x2 character LCD using an 8051 microcontroller (AT89S52), demonstrating cursor positioning, command/data handling, and LCD timing control.

__Hardware Connection:__
 - RS → P2.0
 - RW → P2.1
 - EN → P2.2
 - D0–D7 (LCD Data Lines) → P1.0 to P1.7
 - VSS → GND
 - VDD → +5V
 - VEE → 10k potentiometer center pin (contrast control)
 - 10k potentiometer ends → VDD and GND
 - LCD backlight LED+ → +5V through 220Ω resistor
 - LCD backlight LED− → GND

__Software Simulation:__

![image](https://github.com/user-attachments/assets/969ea4a4-d746-4424-aeb1-ede04791f22f)

__Hardware Simulation:__

![Screenshot 2025-06-12 234344](https://github.com/user-attachments/assets/421fc979-668e-4f1e-90f4-2aa5722fe6d1)

![Screenshot 2025-06-12 234403](https://github.com/user-attachments/assets/79a5dbf6-4854-4b71-9516-b1266533bdfe)

__Code:__
```
#include <reg51.h>
#include "lcd.h"
#include "lcd_defines.h"
#include "delay.h"
#include "types.h"

s8 msg[] = "GOPAL";

void main() {
    s32 i;
    InitLCD();
    delay_ms(20); 
    while (1) {
        for (i = 0; i <= (16 - 5); i++)
	{ 
            CmdLCD(0x80 + i);              
            StrLCD(msg);      
            delay_ms(100);
            CmdLCD(CLEAR_LCD);         
        }

        // Right to Left Scroll
        for (i = (16 - 5 - 1); i >= 0; i--) {
            CmdLCD(0x80 + i);             
            StrLCD(msg);
            delay_ms(100);
            CmdLCD(CLEAR_LCD);
        }
    }
}
```
________________________________________________________________________________________________________________
__17. Title: Fastest Finger First Timer Display on LCD Using AT89S52__

_Objective:_ To implement a reflex timer system using a 16x2 LCD and two switches on an AT89S52 microcontroller. The system begins timing when a trigger switch is pressed and stops when a stop switch is activated, displaying the elapsed time (seconds.milliseconds) on the LCD.

__Hardware Connection:__
LCD Connections:
 - RS → P2.0
 - RW → P2.1
 - EN → P2.2
 - D0–D7 → P1.0 to P1.7
 - VSS → GND
 - VDD → +5V
 - VEE → Center of 10k Potentiometer (for contrast)
 - Potentiometer ends → VDD and GND
 - LCD Backlight + → +5V through 220Ω resistor
 - LCD Backlight − → GND

Switch Inputs (Active LOW):
 - Trigger Switch → P3.2
 - Stop Switch → P3.3
 - Common Ground: All GND pins (LCD, switches, MCU) must be connected together

__Software Simuatuion:__

![image](https://github.com/user-attachments/assets/275c035a-cf26-41b5-8c1c-2be478a57214)

__Hardware Simulation:__

![Screenshot 2025-06-12 234508](https://github.com/user-attachments/assets/146b394e-4d6a-432e-bb18-e353767cbc65)

![image](https://github.com/user-attachments/assets/2fcd2034-0b08-484c-a2a9-1fddf99aa41c)


__Code:__
```
// fastest_finger_first_lcd.c
#include <reg51.h>
#include "lcd.h"
#include "lcd_defines.h"
#include "delay.h"
#include "types.h"

sbit TRIG_SW_AL = P3^2;   
sbit STOP_SW_AL = P3^3;   

void disp_time(u32 sec, u32 millisec){
    CmdLCD(GOTO_LINE2_POS0); 
    U32LCD(sec);           
    CharLCD('.');            
    U32LCD(millisec);        
}

void main(){
    u32 millisec = 0, sec = 0;
    u8 flag = 0;

    InitLCD();
    delay_ms(20);
    StrLCD("Fast Finger 15+");

    while(1){
        disp_time(sec, millisec);

        if(TRIG_SW_AL == 0) {
            flag = 1;

            while(TRIG_SW_AL == 0)
                disp_time(sec, millisec);

            while(flag == 1) {
                for (sec = 0; sec < 10; sec++) {
                    if (STOP_SW_AL == 0) {
                        flag = 2;
                        while (STOP_SW_AL == 0)
                            disp_time(sec, millisec);
                        break;
                    }

                    for(millisec = 0; millisec < 10; millisec++) {
                        delay_ms(100); // Simulate time
                        disp_time(sec, millisec);

                        if(STOP_SW_AL == 0) {
                            flag = 2;
                            while (STOP_SW_AL == 0)
                                disp_time(sec, millisec);
                            break;
                        }
                    }

                    if(flag == 2) break;
                }

                if(flag == 2) flag = 0;  // Reset for next round
            }

            sec = 0;
            millisec = 0;
        }
    }
}
```
_________________________________________________________________________________________________________________________________________________________
__18. Title: 4x3 Matrix Keypad Interface with 16x2 LCD on AT89S52__

_Objective:_ To interface a 4x3 matrix keypad with an AT89S52 microcontroller and display the pressed key on a 16x2 character LCD. When the program starts, a welcome message is displayed, and then the system continuously scans the keypad to display numeric keypresses.

__Hardware Connection:__
LCD (16x2) Interface with AT89S52:
 - LCD RS → P3.7
 - LCD RW → P3.5
 - LCD EN → P3.6
 - LCD D0–D7 (Data Bus) → Port 2 (0xA0 or P2.0 to P2.7)
 - LCD VSS → GND
 - LCD VDD → +5V
 - LCD VEE → Wiper of 10k potentiometer (contrast)
 - LCD Backlight + → +5V via 220Ω resistor
 - LCD Backlight − → GND

Keypad (4x3 Matrix) Interface with AT89S52:
 - Row 0 (R0) → P1.0
 - Row 1 (R1) → P1.1
 - Row 2 (R2) → P1.2
 - Row 3 (R3) → P1.3
 - Column 0 (C0) → P1.4
 - Column 1 (C1) → P1.5
 - Column 2 (C2) → P1.6
 - Column 3 (C3) → Not Used in 4x3 keypad

__Software Simulation:__

![image](https://github.com/user-attachments/assets/679e56fd-62ab-449b-9860-b5a947b5e856)

__Hardware Simuation:__

![image](https://github.com/user-attachments/assets/96578290-c1bc-460f-a296-62c2d78d1823)

![image](https://github.com/user-attachments/assets/51f3d4b2-b263-465a-94f4-3d4fd3e691f7)


__Code:__
```
#include<reg51.h>
void keypad();
void cmd(char c);
void delay(int num);
void lcdinit();
void lcddata(char c);
sfr dataport=0xA0;    
    
sbit r0=P1^0;sbit r1=P1^1;
sbit r2=P1^2;sbit r3=P1^3;
sbit c0=P1^4;sbit c1=P1^5;
sbit c2=P1^6;sbit c3=P1^7;
sbit rs=P3^7;sbit rw=P3^5;
sbit en=P3^6;

                                   
int main(){
int count=0;
//Display string on 16x2 lcd Row-1
char st[]={"PLEASE ENTER     NUMBER "};
lcdinit();                         

while(st[count]!='\0')
{
lcddata(st[count]);
if(count==16)
cmd(0xC0);
count++;
}

delay(100000);  

cmd(0x01);  
cmd(0x80);  

while(1)     
{
keypad();
}
}
                                    
void lcddata(char c)
{
dataport=c;
rw=0;                
rs=1;               
en=1;
delay(50);       
en=0;
delay(50);
}
                                 
void cmd(char c){
dataport=c;
rw=0;        
rs=0;       
en=1;
delay(50);     
en=0;
delay(50);
}
void delay(int num){
unsigned int i,j;
for(i=0;i< num;i++)
for(j=0;j<5;j++);
}
                                   
void lcdinit(){
delay(15000);cmd(0x30);
delay(4500); cmd(0x30);
delay(300);  cmd(0x30);
delay(600);  cmd(0x38);
cmd(0x0F);   cmd(0x01);
cmd(0x06);   cmd(0x80);
dataport=0x00;
P1=0xFF;
P3=0x00;
}
                                          
void keypad(){
unsigned char c='t';
while(c!='E'){
// Row 0: 1 2 3
r0=0; r1=1; r2=1; r3=1;
if(c0==0 && r0==0){ lcddata('1'); delay(10000); while(c0==0); }
if(c1==0 && r0==0){ lcddata('2'); delay(10000); while(c1==0); }
if(c2==0 && r0==0){ lcddata('3'); delay(10000); while(c2==0); }
P1=0xFF;

// Row 1: 4 5 6
r0=1; r1=0; r2=1; r3=1;
if(c0==0 && r1==0){ lcddata('4'); delay(10000); while(c0==0); }
if(c1==0 && r1==0){ lcddata('5'); delay(10000); while(c1==0); }
if(c2==0 && r1==0){ lcddata('6'); delay(10000); while(c2==0); }
P1=0xFF;

// Row 2: 7 8 9
r0=1; r1=1; r2=0; r3=1;
if(c0==0 && r2==0){ lcddata('7'); delay(10000); while(c0==0); }
if(c1==0 && r2==0){ lcddata('8'); delay(10000); while(c1==0); }
if(c2==0 && r2==0){ lcddata('9'); delay(10000); while(c2==0); }
P1=0xFF;

// Row 3: * 0 #
r0=1; r1=1; r2=1; r3=0;
if(c1==0 && r3==0){ lcddata('0'); delay(10000); while(c1==0); }
P1=0xFF;

c='E';
}
}
```
_______________________________________________________________________________________________________________________________________
__19. Title: Name Entry System Using 4x4 Keypad and 16x2 LCD on AT89C51__

_Objective:_ To develop an embedded system that allows a user to enter alphanumeric characters using a 4x4 matrix keypad, and displays the input in real-time on a 16x2 LCD. This mimics the functionality of a traditional mobile keypad (multi-key tap) for character selection.

Key Functionalities:
 - LCD displays an initial message prompting for name input.
 - Each key press on the keypad displays corresponding letters/numbers/symbols.
 - Multi-press logic allows cycling through characters mapped to each key.
 - Real-time character display with cursor control on LCD.

__Hardware Connections:__
Microcontroller:
 - AT89C51 / AT89S52 (8051-based MCU)

16x2 LCD (Connected to Port 2):\
LCD Pin	       Description	            Connection
- D0–D7 	Data lines	Port 2 (P2.0–P2.7)
- RS	      Register Select	P3.7
- RW	         Read/Write	P3.5
- EN              Enable	P3.6
- VSS	           GND		GND
- VDD	           +5V		+5V
- VEE	    Contrast Control	10k Pot to GND

4x4 Matrix Keypad (Connected to Port 1):
Row\ 
  Pin	Connection	Description
 - R0	P1.0	Row 0
 - R1	P1.1	Row 1
 - R2	P1.2	Row 2
 - R3	P1.3	Row 3

Column\ 
   Pin	Connection Description
 - C0	P1.4	Column 0
 - C1	P1.5	Column 1
 - C2	P1.6	Column 2
 - C3	P1.7	Column 3

Power Supply:
 - +5V regulated power supply for microcontroller, LCD, and keypad.

__Software Simulation:__

![image](https://github.com/user-attachments/assets/db0fe7a4-8238-4a3d-a784-2bb1d7d837bf)

__Hardware Simulation:__

![Screenshot 2025-06-12 234716](https://github.com/user-attachments/assets/2549b056-fd71-4a3e-8f5a-f2f9afc331bd)

![Screenshot 2025-06-12 235429](https://github.com/user-attachments/assets/656b338a-852a-479b-82ad-243ce68e1f09)


__Code:__
```
#include<reg51.h>
void keypad();
void cmd(char c);
void delay(int num);
void lcdinit();
void lcddata(char c);
sfr dataport=0xA0;        //16x2 lcd connected to port-2

sbit r0=P1^0;sbit r1=P1^1;
sbit r2=P1^2;sbit r3=P1^3;//Keypad rows and coulombs
sbit c0=P1^4;sbit c1=P1^5;
sbit c2=P1^6;sbit c3=P1^7;
sbit rs=P3^7;sbit rw=P3^5;
sbit en=P3^6;

                                   //MAIN FUNCTION
int main(){
int count=0;
//Display string on 16x2 lcd Row-1
char st[]={"PLEASE ENTER YOUR NAME "};
lcdinit();                         //Initialize 16x2 lcd

while(st[count]!='\0') //Display st[] string on 16x2 lcd
{
lcddata(st[count]);
if(count==16)
cmd(0xC0);
count++;
}

delay(100000);  //Delay st[] string will remain on lcd for some time

cmd(0x01);   //Clear Lcd - st[] string will vanish
cmd(0x80);   //Put string on first row of Lcd

while(1)     //Check for keystrokes 
{
keypad();
}
}
                                    //DATA FUNCTION
void lcddata(char c)
{
dataport=c;
rw=0;                
rs=1;               
en=1;
delay(50);       
en=0;
delay(50);
}
                                   //COMMAND FUNCTION
void cmd(char c){
dataport=c;
rw=0;        
rs=0;       
en=1;
delay(50);     
en=0;
delay(50);
}
void delay(int num){
unsigned int i,j;
for(i=0;i< num;i++)
for(j=0;j<5;j++);
}
                                   //LCD INITIALIZATION
void lcdinit(){
delay(15000);cmd(0x30);
delay(4500); cmd(0x30);
delay(300);  cmd(0x30);
delay(600);  cmd(0x38);
cmd(0x0F);   cmd(0x01);
cmd(0x06);   cmd(0x80);
dataport=0x00;
P1=0xFF;
P3=0x00;
}
                                          //IDENTIFYING KEYSTROKE
void keypad(){
unsigned char c='t';
while(c!='E'){
             
//Scan first row and coulomb, coulomb will be static and all row buttons will be scanned 
//command 0x10 moves the cursor one step back

                        
r0=0;r1=1;r2=1;r3=1;                   //a,b,c,1
if(c0==0 && r0==0){
lcddata('a');P1=0xFE;delay(10000);
     if(c0==0 && r0==0){	 
     cmd(0x10); lcddata('b');P1=0xFE;delay(10000);
     if(c0==0 && r0==0){
     cmd(0x10); lcddata('c');P1=0xFE;delay(10000);
     if(c0==0 && r0==0){
     cmd(0x10); lcddata('1');P1=0XFE;delay(10000);
                                                  }
                                  }
                       }
  P1=0xFF; 
                  }
r0=0;r1=1;r2=1;r3=1;	              //d,e,f,2
if(c1==0 && r0==0){
lcddata('d');P1=0xFE;delay(10000);
     if(c1==0 && r0==0){
     cmd(0x10); lcddata('e');P1=0xFE;delay(10000);
     if(c1==0 && r0==0){
     cmd(0x10); lcddata('f');P1=0xFE;delay(10000);
     if(c1==0 && r0==0){
     cmd(0x10); lcddata('2');P1=0xFE;delay(10000);
                                                  }
                                    }
                       } 
   P1=0xFF;
                  }
                                      //g,h,i,3
r0=0;r1=1;r2=1;r3=1;
if(c2==0 && r0==0){
lcddata('g');P1=0xFE;delay(10000);
     if(c2==0 && r0==0){
     cmd(0x10); lcddata('h');P1=0xFE;delay(10000);
     if(c2==0 && r0==0){
     cmd(0x10); lcddata('i');P1=0xFE;delay(10000);
     if(c2==0 && r0==0){
     cmd(0x10); lcddata('3');P1=0xFE;delay(10000);
                                                  }
                                    }
                       }	
   P1=0xFF;
                  }
                                       //j,k,l,4
r0=0;r1=1;r2=1;r3=1;
if(c3==0 && r0==0){
lcddata('j');P1=0xFE;delay(10000);
     if(c3==0 && r0==0){
     cmd(0x10); lcddata('k');P1=0xFE;delay(10000);
     if(c3==0 && r0==0){
     cmd(0x10); lcddata('l');P1=0xFE;delay(10000);
     if(c3==0 && r0==0){
     cmd(0x10); lcddata('4');P1=0xFE;delay(10000);
                                                  }
                                    }
                       }	
    P1=0xFF;
                  }
                                       //m,n,o,5
r0=1;r1=0;r2=1;r3=1;
if(c0==0 && r1==0){
lcddata('m');P1=0xFD;delay(10000);
     if(c0==0 && r1==0){
     cmd(0x10); lcddata('n');P1=0xFD;delay(10000);
     if(c0==0 && r1==0){
     cmd(0x10); lcddata('o');P1=0xFD;delay(10000);
     if(c0==0 && r1==0){
     cmd(0x10); lcddata('5');P1=0xFD;delay(10000);
                                                  }
                                    }
                       }	
    P1=0xFF;
                  }
                                       //p,q,r,6
 r0=1;r1=0;r2=1;r3=1;
if(c1==0 && r1==0){
lcddata('m');P1=0xFD;delay(10000);
     if(c1==0 && r1==0){
     cmd(0x10); lcddata('n');P1=0xFD;delay(10000);
     if(c1==0 && r1==0){
     cmd(0x10); lcddata('o');P1=0xFD;delay(10000);
     if(c1==0 && r1==0){
     cmd(0x10); lcddata('5');P1=0xFD;delay(10000);
                                                  }
                                    }
                       }	
    P1=0xFF;
                  }
                                        //s,t,u,7
r0=1;r1=0;r2=1;r3=1;
if(c2==0 && r1==0){
lcddata('s');P1=0xFD;delay(10000);
     if(c2==0 && r1==0){
     cmd(0x10); lcddata('t');P1=0xFD;delay(10000);
     if(c2==0 && r1==0){
     cmd(0x10); lcddata('u');P1=0xFD;delay(10000);
     if(c2==0 && r1==0){
     cmd(0x10); lcddata('7');P1=0xFD;delay(10000);
                                                  }
                                    }
                       }	
     P1=0xFF;
                  }
                                        //v,w,x,8
r0=1;r1=0;r2=1;r3=1;
if(c3==0 && r1==0){
lcddata('v');P1=0xFD;delay(10000);
     if(c3==0 && r1==0){
     cmd(0x10); lcddata('w');P1=0xFD;delay(10000);
     if(c3==0 && r1==0){
     cmd(0x10); lcddata('x');P1=0xFD;delay(10000);
     if(c3==0 && r1==0){
     cmd(0x10); lcddata('8');P1=0xFD;delay(10000);
                                                  }
                                    }
                       }	 
      P1=0xFF;
                  }
                                         //y,z,9
r0=1;r1=1;r2=0;r3=1;
if(c0==0 && r2==0){
lcddata('y');P1=0xFB;delay(10000);
     if(c0==0 && r2==0){
     cmd(0x10); lcddata('z');P1=0xFB;delay(10000);
     if(c0==0 && r2==0){
     cmd(0x10); lcddata('9');P1=0xFB;delay(10000);
                                    }
                       }	 
      P1=0xFF;
                  }
                                        //0,-,>
r0=1;r1=1;r2=0;r3=1;
if(c1==0 && r2==0){
lcddata('0');P1=0xFB;delay(10000);
     if(c1==0 && r2==0){
     cmd(0x10); lcddata('-');P1=0xFB;delay(10000);
     if(c1==0 && r2==0){
     cmd(0x10); lcddata('>');P1=0xFB;delay(10000);
                                    }
                       }	
       P1=0xFF;
                  }
                                       //!,@,#
r0=1;r1=1;r2=0;r3=1;
if(c2==0 && r2==0){
lcddata('!');P1=0xFB;delay(10000);
     if(c2==0 && r2==0){
     cmd(0x10); lcddata('@');P1=0xFB;delay(10000);
     if(c2==0 && r2==0){
     cmd(0x10); lcddata('#');P1=0xFB;delay(10000); 
                                    }
                       }	
        P1=0xFF;
                  }
                                       //$,%,^
r0=1;r1=1;r2=0;r3=1;
if(c3==0 && r2==0){
lcddata('$');P1=0xFB;delay(10000);
     if(c3==0 && r2==0){
     cmd(0x10); lcddata('%');P1=0xFB;delay(10000);
     if(c3==0 && r2==0){
     cmd(0x10); lcddata('^');P1=0xFB;delay(10000);
   
                                    }
                       }	 
        P1=0xFF;
                  }
                                        //&,*
r0=1;r1=1;r2=1;r3=0;
if(c0==0 && r3==0){
lcddata('&');P1=0xF7;delay(10000);
     if(c0==0 && r3==0){
     cmd(0x10); lcddata('*');P1=0xF7;delay(10000);
                       }	
         P1=0xFF;
                  }
                                        //(,)
r0=1;r1=1;r2=1;r3=0;
if(c1==0 && r3==0){
lcddata('(');P1=0xF7;delay(10000);
     if(c1==0 && r3==0){
     cmd(0x10); lcddata(')');P1=0xF7;delay(10000);
                       }	
         P1=0xFF;
                  }
                                        //-,+
r0=1;r1=1;r2=1;r3=0;
if(c2==0 && r3==0){
lcddata('-');P1=0xF7;delay(10000);
     if(c2==0 && r3==0){
     cmd(0x10); lcddata('+');P1=0xF7;delay(10000);
                       }
      P1=0xFF;
                  }
                                        ///,*
r0=1;r1=1;r2=1;r3=0;
if(c3==0 && r3==0){
lcddata('/');P1=0xF7;delay(10000);
     if(c3==0 && r3==0){
     cmd(0x10); lcddata('*');P1=0xF7;delay(10000);
                       }	
       P1=0xFF;
                  }
 c='E';
 }
}
```
____________________________________________________________________________________________________________________________________________
__20.Title: LCD 20*4 Data Display with CGRAM and Multiple Formats Using AT89S52__

_Objective:_ To demonstrate the use of 16x2 alphanumeric LCD by displaying various data formats—characters, strings, unsigned/signed integers, float, hexadecimal, octal, binary—and custom characters using CGRAM.

__Hardware Connection:__
 - RS → P2.0
 - RW → P2.1
 - EN → P2.2
 - D0–D7 (LCD Data Lines) → P1.0 to P1.7
 - VSS → GND
 - VDD → +5V
 - VEE → 10k potentiometer center pin (contrast control)
 - 10k potentiometer ends → VDD and GND
 - LCD backlight LED+ → +5V through 220Ω resistor
 - LCD backlight LED− → GND

__Software Simulation:__

![image](https://github.com/user-attachments/assets/866ed9e4-a2b5-4b39-aa82-802a0d366aba)

__Hardware Simulation:__

![Screenshot 2025-06-12 233518](https://github.com/user-attachments/assets/3e1362d2-d95c-487f-9b47-57ea343776e3)

![Screenshot 2025-06-12 233534](https://github.com/user-attachments/assets/6062b240-0706-4139-a9d5-6e46f03e776a)

__Code:__
```
#include "lcd.h"
#include "lcd_defines.h"
#include "delay.h"

u8 cgramLUT[8] = {
    0x07,   
    0x04,   
    0x04,   
    0x1F,  
    0x10,   
    0x10,   
    0x10,  
    0x00    
};

void main() {
    InitLCD();                        
    delay_ms(20);
    
	BuildCGRAM(cgramLUT, 0);          
    CmdLCD(CLEAR_LCD);
    CharLCD('A');                  	
   	StrLCD(" V24HE6G2 ");                
	  delay_ms(2000);  
    
	  CmdLCD(GOTO_LINE2_POS0);        
    U32LCD(1234567890);             
    delay_ms(2000);                   

    CmdLCD(GOTO_LINE3_POS0);
    S32LCD(-1234567890);              
    CmdLCD(GOTO_LINE4_POS0);
    F32LCD(123.456789, 6);           
    delay_ms(2000);

    CmdLCD(CLEAR_LCD);
    HexLCD(256);                    
    CmdLCD(GOTO_LINE2_POS0);
    OctLCD(65);                       
    delay_ms(1000);

    CmdLCD(GOTO_LINE3_POS0);
    BinLCD(127, 16);                 
    CmdLCD(GOTO_LINE4_POS0);
    CharLCD(0);                      
    while (1);                     
}
```
__________________________________________________________________________________________________________________________
