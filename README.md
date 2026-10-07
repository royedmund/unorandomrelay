# Arduino UNO random relay controller

An Arduino UNO sketch adapted by Roy E. Antaw / REA Electric from Ahmad Shamshiri's Robojax relay example. It randomly pulses one of the first three channels of a 16-channel relay board.

- [Original Robojax demonstration](https://youtu.be/Q9aBI4ELKC4)
- [Modified project demonstration](https://youtu.be/P9LIQ3Znmek)

## Files and Arduino IDE setup

| File | Purpose |
| --- | --- |
| [example.ino](example.ino) | Main sketch |
| [FlickerTest3ch.ini](FlickerTest3ch.ini) | Alternate Arduino sketch stored with a legacy `.ini` extension; not a configuration file |

Open `example.ino` in the Arduino IDE. If prompted, let the IDE place it in a sketch folder named `example`. Select the Arduino UNO board and the correct serial port, then compile/upload. To try the alternate sketch, copy `FlickerTest3ch.ini` into its own matching sketch folder as an `.ino` file. Do not combine both sketches in one folder, because each defines `setup()` and `loop()`.

## Pin mapping and behaviour

The `controlPin` array maps zero-based relay channels `0`–`15` to:

```text
2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, A0, A1, A2, A3, A4
```

`triggerType` defaults to `LOW` for an active-low relay board. The main loop uses `random(0,3)`, so only channels `0`, `1` and `2` are selected, with pulses from 100 to 249 ms. Serial diagnostics use 9600 baud. Although `loopDelay` is declared, the current loop does not apply a one-second pause.

Confirm the relay board's trigger logic, power requirements and wiring before uploading. Rapid repeated switching may not suit every relay or connected load.

## Attribution and structure

Keep the original copyright, attribution and GNU GPL v3-or-later notice in the sketches. The existing two-file layout is retained so old links remain usable; use separate matching sketch folders when working in the IDE. The `.ini` extension is historical and should not be interpreted as an input read by `example.ino`.
