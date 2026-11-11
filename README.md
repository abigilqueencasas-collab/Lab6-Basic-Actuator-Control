# Laboratory Activity 6: Basic Actuator Control

This project shows how an ESP32 can drive a small DC motor through a motor driver breakout board (a DRV8833 or TB6612FNG type). A push button switches the motor between spinning and coasting to a stop.

## Hardware Setup

- **Microcontroller:** ESP32, powered over USB.
- **Motor power:** a separate AA battery pack feeds the driver's `VM` and `GND` pins, so the motor does not draw current through the ESP32.
- **Load:** a small DC fan motor wired to the driver's motor outputs.
- **Input:** a push button wired to a GPIO pin and ground, using the ESP32's internal pull-up resistor (no external resistor needed).
- **Common ground:** the ESP32, driver, and battery pack all share a ground.

| Signal | ESP32 pin |
|--------|-----------|
| Button (`BTN`) | GPIO 27 *(edit to match your wiring)* |
| Driver input (`ENA`) | GPIO 25 *(edit to match your wiring)* |

## Wiring Evidence

### Video demonstration: 

https://drive.google.com/file/d/1J5k86c9m79h-3HARDJQS3u5_ysCP8fxQ/view?usp=sharing


## How It Works

1. On startup, `ENA` is set LOW, so the motor begins stopped.
2. The button input uses `INPUT_PULLUP`, so it reads LOW when pressed.
3. Each debounced press flips the motor state.
4. `ENA` HIGH runs the motor; `ENA` LOW cuts the drive signal and the fan spins down on its own (coast), rather than being actively braked.

## Results

- **Press:** the control signal goes HIGH and the motor turns ON.
- **Release / toggle off:** the signal goes LOW and the fan slows to a natural stop.

Serial Monitor output:

```
Motor OFF (coast)
Motor ON
Motor OFF (coast)
Motor ON
```

<img width="1536" height="2048" alt="image" src="https://github.com/user-attachments/assets/de86b927-f614-4392-ab99-2fe3e52e5a2f" />


## Code

See [`Basic-Actuator-Control-Laboratory6.ino`](./Basic-Actuator-Control-Laboratory6.ino).
