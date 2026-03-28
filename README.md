# STM32-UART-to-LCD-Binary-Display
This project demonstrates how to receive numbers through UART and display their binary equivalent on a 16x2 LCD using STM32.  The user sends a number (via serial terminal like PuTTY), and once a space is entered, the STM32 converts that number into 8-bit binary format and displays it on the LCD.
# STM32 UART to LCD (Binary Display)

## About this project

This is a small STM32 project where I tried combining UART and LCD interfacing.

The idea is simple:
I send a number from my laptop using PuTTY, and the STM32 reads it, converts it into binary, and shows it on a 16x2 LCD.

It’s a basic project, but it helped me understand how data flows from UART → processing → LCD.

---

## What it does

- Takes input from serial terminal (PuTTY)
- Builds the number digit by digit
- When space is pressed → number is processed
- Converts the number into 8-bit binary
- Displays the binary value on LCD
- Also echoes back whatever you type

---

## How to use

1. Flash the code into STM32
2. Connect LCD and UART properly
3. Open PuTTY (or any serial terminal)
4. Set baud rate = 115200
5. Type a number (example: `23`)
6. Press **space**

Now you should see the binary value on LCD.

---

## Example

If you type:13(space)

LCD will show:00001101

---

## Pin connections (what I used)

### LCD (8-bit mode)

- Data pins:
  - D0 → PA10  
  - D1 → PB3  
  - D2 → PB5  
  - D3 → PB4  
  - D4 → PB10  
  - D5 → PA8  
  - D6 → PA9  
  - D7 → PC7  

- Control pins:
  - RS → PB6  
  - RW → PA7  
  - EN → PA6  

---

### UART

- TX → PA2  
- RX → PA3  
- Baud rate → 115200  

---

## Logic (in simple words)

- Each character from UART is read one by one
- If it’s a number → it builds the integer
- If space comes → conversion happens
- Binary string is created using bit shifting
- Then it’s sent to LCD

---

## Limitations

- Works only for numbers up to 255 (8-bit)
- Need to press space after typing number
- No error handling for wrong input

---

## Why I made this

Just to practice:
- UART communication
- LCD interfacing
- Bitwise operations

---

## Future ideas

- Show both decimal and binary
- Add error handling
- Use interrupts instead of polling
- Convert to 4-bit LCD mode

