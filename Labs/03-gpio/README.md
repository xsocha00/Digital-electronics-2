# Lab 3: Jakub Socha

Link to your `Digital-electronics-2` GitHub repository:

   [https://github.com/...](https://github.com/xsocha00/Digital-electronics-2/tree/main/Labs/03-gpio)


### Data types in C

1. Complete table.

| **Data type** | **Number of bits** | **Range** | **Description** |
| :-: | :-: | :-: | :-- | 
| `uint8_t`  | 8 | 0, 1, ..., 255 | Unsigned 8-bit integer |
| `int8_t`   | 8 | -128, ..., 127 | Signed 8-bit integer |
| `uint16_t` | 16 | 0, 1, ..., 65535 | 	Unsigned 16-bit integer |
| `int16_t`  | 16 | -32768, ... , 32767 | Signed 16-bit integer |
| `float`    | 32 | -3.4e+38, ..., 3.4e+38 | Single-precision floating-point |
| `void`     | none | - | result of function that does not return value |


### GPIO library

1. In your words, describe the difference between the declaration and the definition of the function in C.
   * Function declaration - tells the name of function
   * Function definition - body of function, what the function does 

2. Part of the C code listing with syntax highlighting, which toggles LEDs only if push button is pressed. Otherwise, the value of the LEDs does not change. Use function from your GPIO library. Let the push button is connected to port D:

```c
    // Configure Push button at port D and enable internal pull-up resistor
    GPIO_config_input_pullup(&PORTD, BUTTON);

    // Infinite loop
    while (1)
    {
        if (bit_is_clear(PIND, BUTTON))
        {
            // Pause several milliseconds
            _delay_ms(BLINK_DELAY);
            
            GPIO_toggle(&PORTB, LED_GREEN);
            
            GPIO_toggle(&PORTC, LED_BLUE);
	}
    }
```


### Traffic light

1. Scheme of traffic light application with one red/yellow/green light for cars and one red/green light for pedestrians. Connect AVR device, LEDs, resistors, one push button (for pedestrians), and supply voltage. The image can be drawn on a computer or by hand. Always name all components and their values!

   ![your figure](https://github.com/xsocha00/Digital-electronics-2/tree/main/Labs/03-gpio/traffic_light.png)