# STM32-UART-to-LCD-Binary-Display
This project demonstrates how to receive numbers through UART and display their binary equivalent on a 16x2 LCD using STM32.  The user sends a number (via serial terminal like PuTTY), and once a space is entered, the STM32 converts that number into 8-bit binary format and displays it on the LCD.
About This Project

This project is a simple and practical example of combining UART communication and LCD interfacing with STM32.

Instead of hardcoding values, the microcontroller waits for input from a serial terminal (like PuTTY). Once you enter a number and press space, it converts that number into binary and shows it on the LCD.

It’s a good mini-project to understand:

UART receive/transmit
LCD interfacing (8-bit mode)
Number processing in embedded C
How It Works (Simple Explanation)
You open PuTTY (or any serial terminal).
Type a number (for example: 25)
Press space
STM32:
Reads the number
Converts it to binary (00011001)
Displays it on LCD

Also, whatever you type is echoed back to PuTTY (so you can see it).

Pin Configuration
LCD Connections (8-bit mode)
LCD Pin	STM32 Pin
D0	PA10
D1	PB3
D2	PB5
D3	PB4
D4	PB10
D5	PA8
D6	PA9
D7	PC7
RS	PB6
RW	PA7
EN	PA6
Button (optional)
Function	Pin
Input Button	PC13
UART (for PuTTY)
Function	Pin
TX	PA2
RX	PA3

Baud Rate: 115200

Code Logic Explained
1. UART Receive
HAL_UART_Receive(&huart2,&rx,1,HAL_MAX_DELAY);
Waits until user sends a character
2. Echo Back
HAL_UART_Transmit(&huart2,&rx,1,1000);
Sends the same character back to terminal
3. Build Number Digit by Digit
if(rx >= '0' && rx <= '9')
{
    num = num*10 + (rx - '0');
}

Example:

Input: 2 → num = 2
Then 5 → num = 25
4. Detect End of Number
if(rx == ' ')
Space means "number complete"
5. Convert to Binary
for(int i=7;i>=0;i--)
{
    bin[7-i] = ((num>>i)&1) + '0';
}
Converts decimal to 8-bit binary string
6. Display on LCD
lcd_command(0x80);
lcd_string(bin,8);
How to Run
Flash code into STM32
Connect LCD and UART properly
Open PuTTY
Set:
COM port
Baud rate = 115200
Type a number (like 13)
Press space

LCD will show:

00001101
Example
Input (PuTTY)	Output (LCD)
5 ␣	00000101
10 ␣	00001010
255 ␣	11111111
Notes
Only supports numbers up to 255 (8-bit)
Make sure LCD contrast is adjusted
Always press space after number
Without space → no output
Future Improvements
Show decimal + binary together
Add overflow handling (>255)
Use interrupt-based UART
Switch to 4-bit LCD mode
Final Thoughts

This project is a great step if you're learning embedded systems.
It combines input (UART) + processing (logic) + output (LCD) — which is basically the core of embedded programming.
