Device that converts 12v to 5v, measures power/other things, and controls 4-wire fans.

# DESIGN NOTES

The 3rd 5V out is reserved (backup).

**Power Sensing**

_Calibration_

V bus max   = 16V
V shunt max = 320㎷ (PGA = ÷8)
R shunt     = 0.04Ω

I max possible = V shunt max ÷ R shunt = 8A

I max expected = 3A (this needs to be revisited with better understanding of what it represents)

_Serial Bus Address_

Ground A0 and A1 to get adress of 1000000.

I²C bus pull-up resistors of 4.7KΩ was not calculated.  It was from arbitrary site.   The INA219 datasheet references 3.3KΩ.

_Optional Filter_

As filtering may not be needed initial implementation will be 0Ω resistors (R6/7) and capacitor (C3) unpopulated.

_Bypass Capacitors_

Values are taken from datasheet.  Ceramic type chosen from arbitrary page.

_Trace Widths_

8A 5mm main in/out
4A 2mm feed 2 converters
2A 1mm  feed 1 converter

**Questions**

- Vias to ground plane:  Run a short wire off the pad then insert a via?   Is this the best way of doing it?   It doesn't seem like via can be at the ground pad itself.
- OK to run trace between pads of a component like a resistor?