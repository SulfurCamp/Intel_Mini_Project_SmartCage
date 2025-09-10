# Smart_Cage

## Project Goal
The goal is to build a smart cage system for temporary pet storage.

- Implement a server using Raspberry Pi 4
- Real-time control of the cage's temperature, humidity, illuminance, and DC motor using STM32
- Implement an administrator system using Arduino (user controllable)
- Implement real-time status monitoring function using environmental sensors (temperature, humidity, illuminance)
- Develop a server-based user control system (lighting, ventilation window, fan, etc.)
- Design an efficient board architecture with separated input sensors and output control
- Inter-device linkage and integrated management via TCP/IP-based Wi-Fi communication

## Block Diagram
<img width="1280" height="720" alt="image" src="https://github.com/user-attachments/assets/c71615dc-08b6-4864-b9bf-99865a3c03e5" />

## Flowchart
<img width="1280" height="720" alt="image" src="https://github.com/user-attachments/assets/fa78d1c5-d76d-4b0e-ba7c-5e9596036376" />

## Names and Roles
| Name | Role | Board |
|---|---|---|
| **User** | User command input and status check interface | LDplayer4 (Mobile) |
| **Server** | - Central control server for the entire system<br>- Receives and stores cage status from all CCUs<br>- Processes user control requests<br>- Bluetooth communication with the administrator MCU<br>- Records cage allocation, device operation status, rental time, etc. | Raspberry Pi |
| **CCU (Cage Control Unit)** | - One installed in each cage<br>- Measures temperature, humidity, and illuminance<br>- Controls internal lighting LED and status LED<br>- Controls window opening/closing motor<br>- Controls fan motor<br>- LCD status display<br>- Communicates directly with the server via Wi-Fi | STM32 |
| **MCU (Manager Control Unit)** | - Administrator-only control board<br>- Communicates with the server (Raspberry Pi) via Bluetooth<br>- Monitors the entire cage status<br>- Transmits administrator control commands (window, LED, fan, buzzer, etc.) | Arduino + Bluetooth module |

## Modules Used
**CCU (Cage Control Unit) Modules**
| Module Name | Role |
|---|---|
| DHT11 | Measures temperature and humidity |
| CDS Sensor (LDR) | Measures illuminance |
| LED × 2 | Status display (internal LED, external status LED) |
| Servo Motor (SG-90) | Opens/closes window |
| ESP-01 (Wi-Fi Module) | Communicates with Raspberry Pi via TCP/IP |

**MCU (Manager Control Unit) Modules**
| Module Name | Role |
|---|---|
| HC-06 | Bluetooth communication (with server) |
| LCD 16x2 | GUI configuration, administrator control |
| Joystick Module | Cursor movement, menu selection |

**Server (Raspberry Pi) Functions**
| Module/Function | Role |
|---|---|
| MariaDB | Stores cage status, user, and control records |
| Bluetooth Module (built-in) | Handles administrator communication with Arduino |
| TCP/IP Socket Server | Communication with user app and each cage (CCU) |
