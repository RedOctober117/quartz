# n-Radix to Base 10

When converting between radix, it is always easiest to convert to `Base 10` first. Converting to `Base 10` is as easy as making tens:

`Base 10` represented in expanded form: 
`153 Base 10 = (10^2 * 1) + (10^1 * 5) + (10^0 * 3)`

In elementary school, this is taught as "100 ones, plus 10 fives, plus 3 ones," or: 

`(100 * 1) + (10 * 5) + (3 * 1)`

The same concept is applied to other radix. When converting any radix to `Base 10`, we take each place, multiplied by its base to the power of the index. For example:

Consider: `212 Base 3 = (3^2 * 2) + (3^1 * 1) + (3^0 * 2) = 18 + 3 + 2 = 23 Base 10`

Hexadecimal remains the same process. Each position's base to the power of its index. 

Consider: `6D5 Base 16 (Hex) = (16^2 * 6) + (16^1 * 13) + (16^0 * 5) = 1536 + 208 + 5 = 1749`

# Base 10 to n-Radix
Converting `Base 10` to any other radix is a matter of division. The process is simple, divide the `Base 10` number by the new base. Take the integer of the quotient as the next divisor, and multiply the remainder by the new base. This will be the resulting bit/digit. If zero, write zero.

Consider: 
```
1256 Base 10 -> Base 16 (Hex):
	1256 / 16 = 78.5   (.5 * 16 = 8)      R 8
	  78 / 16 = 4.875  (.875 * 16 = 14)  R 14
	   4 / 16 = 0.25   (.25 * 16 = 4)     R 4
	Stop at 0.
	Convert any numbers >9 to their corresponding hexadecimal value.
```
The new base is comprised of the remainders. When converting integer components, the remainders are read bottom to top, thus `1256 Base 10 = 4E8 Base 16 (Hex)`. 

`Base 10 -> Base 2 (Binary)` is even more straightforward, albeit much more work for big numbers. Divide the original number by two until you reach zero:
```
567 Base 10 -> Base 2 (Binary):
	567 / 2 = 283.5  (.5 * 2 = 1) R 1
	283 / 2 = 141.5  (.5 * 2 = 1) R 1
	141 / 2 = 70.5   (.5 * 2 = 1) R 1
	 70 / 2 = 35                  R 0
	 35 / 2 = 17.5 (...)          R 1
	 17 / 2 = 8                   R 1
	  8 / 2 = 4                   R 0
	  4 / 2 = 2                   R 0
	  2 / 2 = 1                   R 0
	  1 / 2 = 0.5                 R 1

567 Base 10 -> Base 2 (Binary) = 1000110111
```

# Fractional Values from Base 10 to n-Radix
Fractional values are converted inversely from integers. Rather than division, the fractional value is multiplied by the new radix, and the number left of the decimal is taken as the new index value. 

```txt
0.03125 (Base 10) -> (Base 2):
0.03125 * 2 = 0.0625  R0
 0.0625 * 2 = 0.125   R0
  0.125 * 2 = 0.25    R0
   0.25 * 2 = 0.5     R0
    0.5 * 2 = 1.0     R1

Result is read top to bottom: .00001
```
Just like with integer conversion, when you encounter a 1 to the left of the decimal, drop it when moving to the next multiplication step.