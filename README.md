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

__Hardware Simulation:__

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

__8.Title: Digital Clock Simulation on 7-Segment Display Using AT89S52__

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


__Hardware Simulatuion:__


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
__9.Title: Static 4-Digit Number Display Using AT89S52 and 7-Segment Display__

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


__Hardware Simulation:__

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
__10.Title: Floating Point Number Display on 4-Digit 7-Segment Using AT89S52__

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

__Hardware Simulation:__

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
__11.Title: Scrolling Message Display on 4-Digit 7-Segment Using AT89S52__

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

__Hardware Simulation:__

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
__12.Title: LCD Data Display with CGRAM and Multiple Formats Using AT89S52__

_Objective:_ To demonstrate the use of 16x2 alphanumeric LCD by displaying various data formats—characters, strings, unsigned/signed integers, float, hexadecimal, octal, binary—and custom characters using CGRAM.

__Hardware Connection:__
 - Microcontroller used: AT89S52
 - LCD type: 16x2 alphanumeric, HD44780 compatible
 - LCD data lines D0–D7 connected to Port P0 (for 8-bit mode)
 - Control lines:
	 - RS → P2.0
	 - RW → P2.1
	 - EN → P2.2
	 - VSS → GND
	 - VDD → +5V
	 - VEE → 10K potentiometer (for contrast control)
 - Power supply: Regulated 5V DC

__Software Simulation:__

__Hardware Simulation:__

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
__13. Title: Alphabet Display with ASCII Values on LCD Using AT89S52__

_Objective:_ To display uppercase alphabets (A–Z) on a 16x2 LCD along with their corresponding ASCII values in both decimal and hexadecimal formats, using the AT89S52 microcontroller.

__Hardware Connection:__
 - Microcontroller: AT89S52
 - LCD Type: 16x2 Alphanumeric LCD (HD44780 compatible)
 - LCD Mode: 8-bit
 - LCD Data Lines (D0–D7): Connected to Port P0
 - LCD Control Lines:
	 - RS: P2.0
	 - RW: P2.1
	 - EN: P2.2
 - VSS: GND
 - VDD: +5V
 - VEE: Contrast via 10K potentiometer
 - Backlight: +5V through current-limiting resistor
 - Power Supply: Regulated 5V DC

__Software Simulation:__


__Hardware Simulation:__

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
__14. Title: Electronic Dice Simulation on LCD Using AT89S52__

_Objective:_ To simulate a 6-faced electronic dice using the AT89S52 microcontroller. When a push-button is pressed, a pseudo-random number between 1 and 6 is generated and displayed on a 16x2 LCD.

__Hardware Connection:__
 - Microcontroller: AT89S52
 - LCD Type: 16x2 Alphanumeric LCD (HD44780 compatible)
 - LCD Mode: 8-bit
 - LCD Data Lines (D0–D7): Connected to Port P0
 - LCD Control Lines:
	 - RS: Connected to P2.0
	 - RW: Connected to P2.1
	 - EN: Connected to P2.2
 - Switch (ROLL_SW): Connected to P3.2 (active low, pulled-up with 10KΩ resistor)
 - VSS: GND
 - VDD: +5V
 - VEE: Contrast via 10K potentiometer
 - Backlight: +5V through current-limiting resistor
 - Power Supply: Regulated 5V DC

__Software Simulation:__

__Hardware Simuation:__

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


