# X-Pad

![Version](https://img.shields.io/badge/Version-V%200.1%20BETA-blue)
[![Status](https://img.shields.io/badge/Status-PCB%20Design%20Complete-green.svg)](https://github.com/YourRepo/X-Pad)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

The **X-Pad** is a highly customizable, feature-rich game controller built around the $\text{ESP32-S3-WROOM-1U}$, offering `Wi-Fi`, `BLE HID`, `USB HID`, `ESP-NOW`, and `LoRa` connectivity. It includes `14 buttons`, a `D-Pad`, `dual analog sticks`, `triggers`, `RGB lighting`, `dual vibration motors`, and an `MPU6050` gyro sensor, all powered by a long-lasting `1S2P 18650 Li-ion battery pack` that delivers at least 24 hours of use. A secondary `ATtiny84-MU` co-processor handles stick input, localized RGB effects, and vibration control, while a latch-based auto-sleep system ensures power efficiency. The controller has the default `PowerA` key layout and provides a UI-driven key-mapper program for flexible input remapping.

## Features

#### Main MCU & Connectivity

- Uses **ESP32-S3-WROOM-1U** as the primary MCU.
- Supports **four default communication interfaces:**

  - **Wi-Fi**
  - **Bluetooth Low Energy (BLE HID)**
  - **USB HID**
  - **ESP-NOW**

- Includes an additional **LoRa module** for extended long-range communication.
- ESP32-S3 supports **multiple simultaneous BLE HID device connections**.

#### Input & Control Hardware

- **Total of 14 buttons**, including:

  - 4 face buttons (**A, B, X, Y**)
  - 2 bumpers
  - 4 menu buttons (**Master, Menu, Share, View**)
  - 2 stick-click buttons
  - 2 back buttons

- **Directional Pad (D-Pad)**
- **Two analog sticks**
- **Two analog triggers**
- **RGB LEDs** placed across the controller for visuals

#### Sensors & Haptics

- Built-in **MPU6050 gyro sensor** for motion control.
- **Dual vibration motors** for haptic feedback.

#### Power System

- Powered by a **1S2P 18650 Li-ion battery pack**.
- Battery protection circuit has **DW01A** and **FS8205**.
- The charging circuit has **TP4056**.
- A 3v3 power supply is provided and stabilised by **SGM2212**.
- Battery life of **24+ hours** per charge.
- Includes a **latch-based auto-sleep circuit** to reduce power consumption when idle.

#### Supporting MCU (Co-Processor)

- **ATtiny84-MU** used due to `ESP32-S3` pin limitations.
- Responsibilities include:

  - Reading **analog stick inputs**
  - Controlling nearby **RGB LEDs** for responsive lighting effects
  - Monitoring & controlling **vibration motors**

#### Software & Customization

- **UI-based key-mapper program** included for user customization.
- Allows mapping of **different key combinations**.
- Default key mapping follows **original PowerA controller layout**.

## Developpers notes

The X-Pad is engineered on a robust dual-MCU architecture, utilizing the $\text{ATtiny84-MU}$ as a dedicated input co-processor to offload low-latency tasks-specifically analog stick reading, RGB control, and haptic feedback-from $\text{ESP32-S3-WROOM-1U}$. This separation ensures the $\text{ESP32-S3}$ can dedicate its resources to maintaining stable multi-protocol wireless communication ($\text{BLE/Wi-Fi/LoRa/ESP-NOW}$), maximizing range and reliability. This section provides the detailed pin-to-pin mapping for the `V 0.1 BETA` hardware design.

### Schematic Diagram

<div align="center">
  <img
    src="assets\imgs\circuitry\X-Pad%20Schematic.png"
    alt="Schematic Diagram"
    width="80%"
  >
</div>

### PCB Design

#### Front Panel

<div align="center">
  <img
    src="assets\imgs\circuitry\X-Pad%20PCB%20Front.webp"
    alt="Front Panel"
    width="60%"
  >
</div>

#### Back Panel

<div align="center">
  <img
    src="assets\imgs\circuitry\X-Pad%20PCB%20Back.webp"
    alt="Back Panel"
    width="60%"
  >
</div>

### Some more details

<details>
  <summary><strong>All Functions and their details with keymap and hex id</strong></summary>

#### Keys, Buttons and D-Pad

<div align="center">

| prefix | name         | footprint           | hex id | net | pin    | function     |
| :----- | :----------- | :------------------ | :----- | :-- | :----- | :----------- |
| KEY1   | MASTER       | PAD                 | ---    | ST  | GPIO38 | Menu Buttons |
| KEY2   | MENU         | PAD                 | ---    | MB  | GPIO37 | Menu Buttons |
| KEY3   | VIEW         | PAD                 | ---    | HB  | GPIO36 | Menu Buttons |
| KEY4   | SHARE        | PAD                 | ---    | SB  | GPIO35 | Menu Buttons |
| KEY5   | X            | PAD                 | ---    | X   | GPIO42 | Face Buttons |
| KEY6   | Y            | PAD                 | ---    | Y   | GPIO41 | Face Buttons |
| KEY7   | A            | PAD                 | ---    | A   | GPIO40 | Face Buttons |
| KEY8   | B            | PAD                 | ---    | B   | GPIO39 | Face Buttons |
| KEY9   | D-PAD UP     | PAD                 | ---    | DU  | GPIO45 | D-Pad        |
| KEY10  | D-PAD DOWN   | PAD                 | ---    | DD  | GPIO48 | D-Pad        |
| KEY11  | D-PAD RIGHT  | PAD                 | ---    | DR  | GPIO47 | D-Pad        |
| KEY12  | D-PAD LEFT   | PAD                 | ---    | DL  | GPIO21 | D-Pad        |
| KEY13  | LEFT BUMPER  | KEY-TH_TL1105VF160Q | ---    | LB  | GPIO18 | Bumpers      |
| KEY14  | RIGHT BUMPER | KEY-TH_TL1105VF160Q | ---    | RB  | GPIO17 | Bumpers      |
| KEY15  | LEFT BACK    | PAD                 | ---    | LT  | GPIO5  | Back Buttons |
| KEY16  | RIGHT BACK   | PAD                 | ---    | RT  | GPIO6  | Back Buttons |

</div>

#### Left Joystick, Vobration Motor

<div align="center">

| prefix | name                | footprint                        | hex id | net   | pin | function             |
| :----- | :------------------ | :------------------------------- | :----- | :---- | :-- | :------------------- |
| JS1    | Left Joystick (X)   | JOYSTICK-TH_252BXXXXXXXB         | ---    | ST1-X | PA2 | Left Stick X Axis    |
| JS1    | Left Joystick (Y)   | JOYSTICK-TH_252BXXXXXXXB         | ---    | ST1-Y | PA0 | Left Stick Y Axis    |
| JS1    | Left Joystick (KEY) | JOYSTICK-TH_252BXXXXXXXB         | ---    | ST1   | PA1 | Left Stick Button    |
| M1     | LCM0827A3038F       | VIBRATION-MOTOR-TH_LCM0827A3038F | ---    | LM    | PA3 | Left Vibration Motor |

</div>

#### Right Joystick, Vobration Motor

<div align="center">

| prefix | name                 | footprint                        | hex id | net   | pin | function              |
| :----- | :------------------- | :------------------------------- | :----- | :---- | :-- | :-------------------- |
| JS2    | Right Joystick (X)   | JOYSTICK-TH_252BXXXXXXXB         | ---    | ST2-X | PA7 | Right Stick X Axis    |
| JS2    | Right Joystick (Y)   | JOYSTICK-TH_252BXXXXXXXB         | ---    | ST2-Y | PB3 | Right Stick Y Axis    |
| JS2    | Right Joystick (KEY) | JOYSTICK-TH_252BXXXXXXXB         | ---    | ST2   | PB2 | Right Stick Button    |
| M2     | LCM0827A3038F        | VIBRATION-MOTOR-TH_LCM0827A3038F | ---    | RM    | PB1 | Right Vibration Motor |

</div>

#### Gyro

<div align="center">

| prefix | name           | footprint                       | hex id | net  | pin   | function             |
| :----- | :------------- | :------------------------------ | :----- | :--- | :---- | :------------------- |
| U2     | MPU6050 (ADDR) | QFN-24_L4.0-W4.0-P0.50-BL-EP2.7 | ---    | ADDR | GPIO2 | MPU6050 Address Line |
| U2     | MPU6050 (SCL)  | QFN-24_L4.0-W4.0-P0.50-BL-EP2.7 | ---    | SCL  | GPIO9 | General I2C rail     |
| U2     | MPU6050 (SDA)  | QFN-24_L4.0-W4.0-P0.50-BL-EP2.7 | ---    | SDA  | GPIO8 | General I2C rail     |
| U2     | MPU6050 (INT)  | QFN-24_L4.0-W4.0-P0.50-BL-EP2.7 | ---    | INTG | GPIO1 | MPU6050 Int Line     |

</div>

#### LoRa

<div align="center">

| prefix | name                 | footprint           | hex id | net  | pin    | function                         |
| :----- | :------------------- | :------------------ | :----- | :--- | :----- | :------------------------------- |
| U5     | Ra-02 SX1278 (MISO)  | WIRELM-SMD_RA-02-BL | ---    | MISO | GPIO13 | SPI rail MOSI pin                |
| U5     | Ra-02 SX1278 (MOSI)  | WIRELM-SMD_RA-02-BL | ---    | MOSI | GPIO11 | SPI rail MISO pin                |
| U5     | Ra-02 SX1278 (SCK)   | WIRELM-SMD_RA-02-BL | ---    | SCK  | GPIO12 | SPI rail SCK pin                 |
| U5     | Ra-02 SX1278 (SS/CS) | WIRELM-SMD_RA-02-BL | ---    | CS   | GPIO10 | Slave Select pin for LoRa module |

</div>

#### RGBs

<div align="center">

| prefix | name          | footprint                             | hex id | net  | pin    | function               |
| :----- | :------------ | :------------------------------------ | :----- | :--- | :----- | :--------------------- |
| RGB1   | SK6812MINI-HS | LED-SMD_4P-L3.5-W3.5-BR_SK6812MINI-HS | ---    | PWR  | GPIO4  | Power ON LED           |
| RGB2   | SK6812MINI-HS | LED-SMD_4P-L3.5-W3.5-BR_SK6812MINI-HS | ---    | RGB1 | PA5    | Left Stick Asthetics   |
| RGB3   | SK6812MINI-HS | LED-SMD_4P-L3.5-W3.5-BR_SK6812MINI-HS | ---    | RGB2 | PB0    | Right Stick Asthetics  |
| RGB4   | SK6812MINI-HS | LED-SMD_4P-L3.5-W3.5-BR_SK6812MINI-HS | ---    | FC   | GPIO14 | Face Buttons Asthetics |
| RGB5   | SK6812MINI-HS | LED-SMD_4P-L3.5-W3.5-BR_SK6812MINI-HS | ---    | DP   | GPIO46 | D-Pad Asthetics        |

</div>
</details>

## Acknowledgments

- Espressif Systems ([ESP32-S3-WROOM-1U](https://documentation.espressif.com/esp32-s3-wroom-1_wroom-1u_datasheet_en.pdf))
- LoRa Alliance ([Ra-02 SX1278](https://jlcpcb.com/api/file/downloadByFileSystemAccessId/8609185408316432384))
- Design Tool ([EasyEDA](https://easyeda.com/))
- PCB Printing ([JLCPCB](https://jlcpcb.com/))
- All open-source contributors.
