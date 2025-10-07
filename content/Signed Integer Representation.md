There are four major ways to represent signed integers in [[Assembly|assembly]]:
- [[#Signed Magnitude]]
- [[#One's Compliment]]
- [[#Two's Compliment]]
- [[#Excess-M]]

# Signed Magnitude
_Signed Magnitude_ represents negatives by making use of the [[Most Significant Bit (MSB)|most significant bit]]. When the bit is `0`, the number is positive. When `1`, negative. 
# One's Compliment
_One's Compliment_ represents negatives by toggling all bits in negative values.


# Two's Compliment
_Two's Compliment_ represents negatives by toggling all bits and adding one.


# Excess-M
_Excess-M_ represents negatives by using an offset. A common offset is `Excess-127`. To convert our `Base 10` value to `Excess-127`, we first add our offset, 127, and then convert to `Base 2`:
```txt
40 (Base 10) -> (Base 2, Excess-127)
40 (Base 10) -> (Excess-127) = 40 + 127 = 167 (Base 10)
167 (Base 10, Excess-127) -> (Base 2, Excess-127) = 101001110
------------------------------------------------------------
-30 (Base 10) -> (Base 2, Excess-127)
-30 (Base 10) -> (Excess-127) = -30 + 127 = 97 (Base 10)
97 (Base 10, Excess-127) -> (Base 2, Excess-127) = 01100001
```

