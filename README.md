![Banner](Banner.png)

# KEYPAD Library
Driver for using keypad in AVR - ARM Cortex M

### Version : 0.0.0

- #### Type : Embedded Software.

- #### Support : AVR/ARM STM32 series.

- #### Program Language : C

- #### Properties :

### Initialization and de-initialization functions:

### Operation functions:
```c++  
uint8_t Keypad_GetKey(void); /* Function for get pushed key */
void Keypad_Read(CommandFunction_T your_function); /* Function for read keypad and run user command */
``` 
### Macros:
```c++  
#define _KEYPAD_PORT 
#define _KEYPAD_PIN  
#define _KEYPAD_FIRST_ROW  
#define _KEYPAD_SCAN_SPEED  
``` 

## How to use this library

### The Keypad library can be used as follows:
#### 1.  Add .h and source file in project.      
#### 2.  Config 4 GPIO as output for rows and 4 GPIO as input for column in your project.  
  * In AVR:  
  
    ```c++
    DDRB = 0xF0; // 1111 0000
    ```
#### 3.  Config Keypad in 'KEYPAD_CONFIG.h' header, for example:  
   * Options in AVR:  
   
      ```c++
      /* Set your connected port */
      
      #define _KEYPAD_PORT          &PORTB
      #define _KEYPAD_PIN           &PINB
      #define _KEYPAD_FIRST_ROW     0
      #define _KEYPAD_SCAN_SPEED    1
      
      ```
      
   * Options in STM32:  
   
      ```c++
      /* Set your connected port */
      
      #define _KEYPAD_PORT          GPIOB
      #define _KEYPAD_PIN           GPIOB
      #define _KEYPAD_FIRST_ROW     14
      #define _KEYPAD_SCAN_SPEED    1
      
      ```
          
#### 4.  Create your function and use operation methods, for example:  
#### Example 1:  
```c++  
void MyFunction(int8_t x)
{
    /* ---- x is the pushed key ---- */
    if(x == 6)
    {
      LED_ON();
    }
    else
    { 
      LED_OFF();
    }
  
}
 
int main(void)
{
	
    while (1) 
    {
  
      Keypad_Read(MyFunction);
    
    }
}
   
``` 
#### Example 2:  
```c++  
void MyFunction(int8_t x)
{
    /* ---- x is the pushed key ---- */
    sprintf(str, "%u", x); /* cast pushed key number to string */
    Lcd_PutString(str); /* show pushed key in the LCD */
}
 
int main(void)
{
	
    while (1) 
    {
  
      Keypad_Read(MyFunction);
    
    }
}
   
``` 
#### Example 3:  
```c++  
uint8_t key_character[16] = {'1' , '2' , '3' , 'A' , '4' , '5' , '6', 'B' , '7' , '8' , '9' , 'C' , '*' , '0' , '#' , 'D'};

void ShowKey(int8_t x)
{
    /* ---- x is the pushed key ---- */
    Lcd_PutChar(key_character[ch]); /* Show character */
}
 
int main(void)
{
	
    while (1) 
    {
  
      Keypad_Read(ShowKey);
    
    }
}
   
``` 

## Tests performed:
- [X] Run on AVR
- [x] Run on STM32 Fx cores 

#### Developer: Majid Derhambakhsh
