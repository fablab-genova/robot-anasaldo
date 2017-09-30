# Joint control task

[back to README.md](../README.md)

## Lessons learnt

## log

### 30.09.17

We bought a few Arduino Nano equivalent boards for 4€ each.
The price is very reasonable but after digging a bit deeper it seems that these boards only have two interrupt pins.
This makes it difficult to handle the signals on the three encoder channels (A, B, and index).
Furthermore as pointed out in [this Reddit thread](https://www.reddit.com/r/arduino/comments/xyjt6/using_rotary_encoders_without_available_interrupt/) it seems one of the two available pins needs to be employed for generating the PWM signal.
