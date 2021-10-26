# Lab 5: Jakub Socha

Link to your `Digital-electronics-2` GitHub repository:

   [https://github.com/...](https://github.com/xsocha00/Digital-electronics-2/tree/main/Labs/05-segments)


### 7-segment library

1. In your words, describe the difference between Common Cathode and Common Anode 7-segment display.
   * CC SSD - all cathodes are connected together, segments are active high
   * CA SSD - all anodes are connected together, segments are active low

2. Code listing with syntax highlighting of two interrupt service routines (`TIMER0_OVF_vect`, `TIMER0_OVF_vect`) from counter application with at least two digits, ie. values from 00 to 59:

```c
/**********************************************************************
 * Function: Timer/Counter1 overflow interrupt
 * Purpose:  Increment counter value from 00 to 59.
 **********************************************************************/
ISR(TIMER1_OVF_vect)
{
    static uint8_t counter = 0;
    static uint8_t counter_tens = 0;
    if (counter == 9 && counter_tens == 5)
    {
       	counter = 0;
        counter_tens = 0;
    }
    if (counter > 9 && counter_tens !=5)
    {
        counter = 0;
        counter_tens++;
    }
    counter ++;
}
```

```c
/**********************************************************************
 * Function: Timer/Counter0 overflow interrupt
 * Purpose:  Display tens and units of a counter at SSD.
 **********************************************************************/
ISR(TIMER0_OVF_vect)
{
    static uint8_t pos = 0;
    
    pos++;
    if(pos == 0)
    {
       	pos = 1;
       	SEG_update_shift_regs(counter, 0);
    	}
    else
    {
        pos = 0;
        SEG_update_shift_regs(counter_tens, 1);
    }

}
```

3. Flowchart figure for function `SEG_clk_2us()` which generates one clock period on `SEG_CLK` pin with a duration of 2&nbsp;us. The image can be drawn on a computer or by hand. Use clear descriptions of the individual steps of the algorithms.

   ![your figure](https://github.com/xsocha00/Digital-electronics-2/blob/main/Labs/05-segments/diagram.png)


### Kitchen alarm

Consider a kitchen alarm with a 7-segment display, one LED and three push buttons: start, +1 minute, -1 minute. Use the +1/-1 minute buttons to increment/decrement the timer value. After pressing the Start button, the countdown starts. The countdown value is shown on the display in the form of mm.ss (minutes.seconds). At the end of the countdown, the LED will start blinking.

1. Scheme of kitchen alarm; do not forget the supply voltage. The image can be drawn on a computer or by hand. Always name all components and their values.

   ![your figure](https://github.com/xsocha00/Digital-electronics-2/blob/main/Labs/05-segments/alarm.png)