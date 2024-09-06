# IR-Controlled RGB Color Randomizer (IR Transmission)

This project uses an Arduino to control an RGB LED with colors randomized by an infrared (IR) remote control. When the IR receiver detects a signal, the RGB LED will change to a random color.

## Components Used

- Arduino Uno
- RGB LED
- IR Receiver
- Resistors
- Jumper Wires
- Breadboard

## Pin Configuration

- **PIN_IR_RECEIVER**: connected to the IR receiver (Pin 12)
- **PIN_RED**: connected to the red pin of the RGB LED (Pin 3)
- **PIN_GREEN**: connected to the green pin of the RGB LED (Pin 9)
- **PIN_BLUE**: connected to the blue pin of the RGB LED (Pin 10)

## Code

```cpp
const int PIN_IR_RECEIVER = 12;
const int PIN_RED = 3;
const int PIN_GREEN = 9;
const int PIN_BLUE = 10;

bool input_ready = true;

void setup() {
    pinMode(PIN_IR_RECEIVER, INPUT_PULLUP);
    pinMode(PIN_RED, OUTPUT);
    pinMode(PIN_GREEN, OUTPUT);
    pinMode(PIN_BLUE, OUTPUT);
    randomSeed(analogRead(0));
}

void loop() {
    if (input_ready && digitalRead(PIN_IR_RECEIVER) == LOW) {
        color_randomizer();
        input_ready = false;
    } else if (!input_ready && digitalRead(PIN_IR_RECEIVER) == HIGH) {
        input_ready = true;
    }
}

void color_randomizer() {
    int red = random(256);
    int green = random(256);
    int blue = random(256);
    analogWrite(PIN_RED, red);
    analogWrite(PIN_GREEN, green);
    analogWrite(PIN_BLUE, blue);
}
```

## How to Use

1. Connect the components to the Arduino according to the pin configuration.
2. Upload the code to your Arduino.
3. Point any IR remote control towards the IR receiver.
4. Press any button on the remote to change the RGB LED to a random color.

## Notes

- The randomSeed(analogRead(0)) line is used to seed the random number generator based on a noisy analog input, which helps produce different random values on each run.
- Ensure proper connections and resistor values to avoid damaging the RGB LED or IR receiver.
