_Booth's Algorithm_ simplifies binary multiplication. Problems are of two parts:
- `Multiplicand (M)`
- `Multiplier (Q)`

Booth discovered that for any given `Q`, it can be represented as such:

For all sequences of ones, the number can be represented as `(2^(j+1)) - (2^i)`, where `(j)` is the index of the most significant 1 of the sequence, and `(i) `is the index of the least significant 1 of the sequence. 

For example:

`00011100 (Base 2)`

This integer has only one string of `1's`, and thus we will only represent it with a single set of `2^(j+1) - (2^i)`. Our most significant `1` is at the index `2^4`, and our least significant 1 is at index `2^2`. Our equation is as follows:

`(2^(4+1)) - (2^(2))`
`(2^(5)) - (2^(2))`
 
For a quick sanity check, `00011100 (Base 2) = 28; (2^5) - (2^2) = (32) - (4) = 28`. 

Because this equation is equivalent to the multiplier, we can still use it with the multiplicand:

```txt
M((2^(j+1)) - (2^i)))
Distribute (M)
(2^(j+1))(M) - (2^i)(M)
```

We want to change all subtraction operations to addition in binary for the sake of ease, and just like standard `Base 10` math, we can move that `(-)` into the `(M)`, like so:

`(2^(j+1))(M) + (2^i)(-M)`

`(-M)` is simply the inverse of `(M)`, which can be calculated using [[Signed Integer Representation#Two's Compliment|2's compliment]]. Remember, toggle all bits and add one. Once all necessary values are computed, the next step can begin. It is very simple to take `(M)` multiplied by any `(2^x)`. Simply shift `(M)` to the left `(x)` times, and fill with zeros. Consider the following:

```txt
       M = 00111001
(2^4)(M) = 001110010000
```

Because `(2^(j+1))` is always at least 1 greater than `(2^i)`, `(2^i)(-M)` will have fewer bits than the other side. To resolve this issue, we fill the left hand side with the [[Most Significant Bit (MSB)|most significant bit]], as follows:

```txt
       M = 00111001
(2^4)(M) = 001110010000

       M = 00111001
(2^2)(M) = 0011100100
0011100100 padded = 000011100100

We can now add:
001110010000
000011100100
```

Note that the above is just an example of padding, it does not consider (-M).


Now that we are familiar with the process, let's demonstrate.

```txt
Multiplicand(M): 00000110
Multiplier(Q):   01100000
```

First, compute the inverse of (M):
```txt
00000110 (Base 2, unsigned) -> 1's compliment = 11111001
11111001 (Base 2, 1's) -> 2's compliment = 11111001 + 00000001 = 11111010
(-M) = 11111010
```

Now, for `Q`, `2^(j+1)`,
Our leading one is at index `6`, thus `2^(6+1) = 2^7`
The tailing bit is at index `5`, thus `2^5`

We now have:

`(2^7)(M) + (2^5)(-M)`

Let's evaluate.

```txt
(2^7)(M) = 00000110 * 2^7
Left shift 7 times, padding with zeros,
000001100000000
(2^7)(M) = 000001100000000
(2^5)(-M) = 1111101000000
```

We need to pad the left with two 1's to align the values:

`111111101000000`

Now we can add our two values:
 ```txt
   000001100000000
+ 111111101000000
-----------------
   000001001000000
```

Sanity check time:

Let's convert our 2's compliment answer back to `Base 10`.
Because the value begins with `0`, that means it is a positive answer, so we can just convert straight to decimal:
```txt
000001001000000 (Base 2) -> (Base 10) = 576
Our (M): 6
Our (Q): 96

  96
x  6
----
 576

All good!
```


If you have a value that has two disparate strings of ones, the equation still applies, but with extra steps:
```txt
(M)  = 001110011
(Q)  = 000111001
(-M) = 110001101

Q decomposes to:

((2^(5+1)) - (2^(3))) + ((2^(0+1)) - (2^(0)))
= ((2^6) - (2^3)) + ((2^1) - (2^0))
= ((2^6)(M) + (2^3)(-M)) + ((2^1)(M) + (2^0)(-M))
=   001110011000000 
       110001101000 
         0011100110 
  +       110001101
  -----------------

Pad all values with their MSB:
001110011000000
111110001101000
000000011100110
111111110001101

Add in three steps for ease:

  001110011000000
+ 111110001101000
-----------------
  001100100101000

Bottom half:

  000000011100110
+ 111111110001101
-----------------
  000000001110011

Add our two sums together:

  001100100101000
+ 000000001110011
-----------------
  001100110011011
```

Sanity check:
Result is positive, thus no conversion to unsigned.
```txt
001100110011011 (Base 2) -> (Base 10) = 6555
(M) (Base 2) -> (Base 10) = 115
(Q) (Base 2) -> (Base 10) = 57

  115
x  57
-----
 6555

All good!
```

