# sos-blinky-stm32f103c8

This project is a simple "blinky" application for the popular STM32F103C8T6 ("Blue Pill") development board, which flashes an SOS Morse code signal (... --- ...) using the onboard LED (PC13).

## Demo

A video of the project in operation:

[**Video Preview (preview.mp4)**](preview.mp4)

---

## Hardware Requirements

* **STM32F103C8T6 "Blue Pill"** Development Board
* **ST-Link V2** (or a similar programmer) for programming
* USB cables for power and programming

## Software and Environment

* **IDE:** STM32CubeIDE
* **Library:** STM32 HAL (Hardware Abstraction Layer)
* **Language:** C

## How It Works

The code continuously flashes the SOS signal within the main `while(1)` loop.

### Morse Code Timing

A base interval (`morse_interval`) of 200ms is used for the Morse code timing:

* **Dot (.):** 1 interval (200ms) LED ON
* **Dash (-):** 3 intervals (600ms) LED ON
* **Intra-signal Gap:** (Between dots and dashes) 1 interval (200ms) LED OFF
* **Letter Gap:** (Between S, O, S) 3 intervals (600ms) LED OFF
* **Word Gap:** (After SOS) 7 intervals (1400ms) LED OFF

### Important Note: Inverted LED Logic (Active-Low)

On most "Blue Pill" boards, the onboard blue LED connected to pin **PC13** is wired as **active-low**. This means:

* `HAL_GPIO_WritePin(GPIOC, GPIO_PIN_13, GPIO_PIN_RESET);` // Logic 0 -> **LED Turns ON**
* `HAL_GPIO_WritePin(GPIOC, GPIO_PIN_13, GPIO_PIN_SET);`   // Logic 1 -> **LED Turns OFF**

The `write_dot_and_delay` and `write_dash_and_delay` functions in the code are written according to this inverted logic.

## How to Use

1.  Clone this repository.
2.  Open the project with STM32CubeIDE.
3.  Build the project (`Build`).
4.  Flash the code to your STM32 board using your ST-Link programmer (`Run`).
5.  You will see the onboard LED start to flash the SOS signal.
