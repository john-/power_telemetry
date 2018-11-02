Device that converts 12v to 5v, measures power/other things, and controls 4-wire fans.

# DESIGN NOTES

The 3rd 5V converter powers ICs and is a backup

**Power Sensing**

_Calibration_

V bus max   = 16V
V shunt max = 320㎷ (PGA = ÷8)
R shunt     = 0.1Ω

I max possible = V shunt max ÷ R shunt = 3.2A

I max expected = 3A (this needs to be revisited with better understanding of what it represents)

_Serial Bus Address_

Ground A0 and A1 to get adress of 1000000.

I²C bus pull-up resistors of 4.7KΩ was not calculated.  It was from arbitrary site.   The INA219 datasheet references 3.3KΩ.

_Optional Filter_

As filtering may not be needed initial implementation will be 0Ω resistors (R6/7) and capacitor (C3) unpopulated.

_Bypass Capacitors_

Values are taken from datasheet.  Ceramic type chosen from arbitrary page.

Design mistakes:

- I did not include any temp sensors! Now when I read the data sheet for the ADT7470 it makes it clear it is can't do standalone temperature measuring. I previously assumed it had one built-in temperature sensor. Anyway, I will use manual control of the ADT7470 based on temperature of SBCs (there will be 2 Odroid C2s in the case). I may add an external temperature sensor for the temperature sensor. Previously I have used 1 wire sensor. I need to confirm I can use 1 wire and I2C at same time on C2.
- The circuit puts out 5V I2C and the C2 max input voltage 3.3V. I happen to have a level shifter to get things working. I should have had the circuit output 3.3V I2C.
- I am pretty sure I should have included GND with the SDA/SCL lines. Since I had to use the level shifter I wound up pulling in 5V/GND from elsewhere in the circuit.
