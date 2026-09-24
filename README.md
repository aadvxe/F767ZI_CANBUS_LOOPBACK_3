# F767ZI CAN Bus Loopback Test (bxCAN)

An embedded STM32CubeIDE project for the **NUCLEO-F767ZI** evaluation board demonstrating CAN bus internal loopback self-testing using the STM32 **bxCAN** peripheral and HAL driver.

---

## 🎯 Project Overview

This project validates the CAN controller configuration and hardware peripheral readiness by transmitting CAN frames in **`CAN_MODE_LOOPBACK`**. In this mode, transmitted messages are internally routed directly to the receive FIFO without requiring an external physical CAN transceiver or bus termination.

- **MCU:** STM32F767ZIT6 (ARM Cortex-M7 @ 216 MHz)
- **Evaluation Board:** NUCLEO-F767ZI
- **IDE / Toolchain:** STM32CubeIDE / GCC ARM Embedded
- **HAL Driver:** STM32F7xx HAL Library

---

## ⚙️ CAN Configuration Details

| Parameter | Configuration | Notes |
| :--- | :--- | :--- |
| **CAN Instance** | `CAN1` | bxCAN controller |
| **Operating Mode** | `CAN_MODE_LOOPBACK` | Internal hardware loopback |
| **Bit Timing** | Prescaler: `4`, BS1: `15TQ`, BS2: `2TQ`, SJW: `1TQ` | Total 18 TQ per bit |
| **Filter Bank** | Bank 0, 32-bit ID Mask Mode | Mask `0x0000`, ID `0x0000` (Accepts all) |
| **FIFO Assignment** | `CAN_RX_FIFO0` | Receives incoming loopback frames |
| **Test Message ID** | `0x11` (Standard ID, 11-bit) | DLC: 2 bytes (`[0x03, 0x01]`) |

---

## 💡 LED Status Indications

On the NUCLEO-F767ZI board:
- **Green LED (`LD1` / `PB0`):** Toggles when `CAN_Polling()` passes successfully (`HAL_OK`), confirming transmit-and-receive verification.
- **Blue/Red LED (`LD2` / `PB7`):** Toggles if `CAN_Polling()` fails or encounters a transmission/reception timeout.

---

## 📁 Folder Structure

```
F767ZI_CANBUS_LOOPBACK_3/
└── F767ZI_CANBUS_LOOPBACK_3/
    ├── Core/
    │   ├── Inc/                 # Header files (main.h, stm32f7xx_hal_conf.h, etc.)
    │   ├── Src/
    │   │   ├── main.c           # CAN loopback configuration, transmission & verification
    │   │   ├── stm32f7xx_it.c   # Interrupt service routines
    │   │   └── system_stm32f7xx.c # System clock & CMSIS setup
    │   └── Startup/             # Startup assembly file
    ├── Drivers/                 # STM32F7xx HAL and CMSIS driver source
    ├── Debug/                   # Compiler build artifacts (.elf, .bin, .map)
    ├── F767ZI_CANBUS_LOOPBACK_3.ioc # STM32CubeMX project definition
    └── STM32F767ZITX_FLASH.ld   # Linker script for Flash execution
```

---

## 🛠️ Building & Running

1. Open **STM32CubeIDE**.
2. Go to **File > Open Projects from File System...** and select the `F767ZI_CANBUS_LOOPBACK_3/F767ZI_CANBUS_LOOPBACK_3` folder.
3. Connect your **NUCLEO-F767ZI** to your PC via Micro-USB (ST-LINK port).
4. Build the project: **Project > Build Project** (`Ctrl+B`).
5. Flash and run: **Run > Run** (`Ctrl+F11`) or Debug (`F11`).
6. Observe the green LED `LD1` (`PB0`) toggling on the board, indicating successful loopback communication.
