# Measuring Vitals with AVR NTUA BOARD

## Overview

This project is a hands-on implementation developed for the Microcomputers Laboratory course at the School of Electrical and Computer Engineering (ECE), National Technical University of Athens (NTUA). It demonstrates the simulation of patient vital signs measurement using the educational NTUA BOARD, featuring an AVR microcontroller. The system measures simulated temperature and blood pressure, displays results locally on an LCD screen, and communicates the data to a web server for remote monitoring.

## Features

- **Temperature Simulation**: Utilizes a DS18B20 digital temperature sensor via the One-Wire protocol to simulate patient temperature readings.
- **Blood Pressure Simulation**: Employs a potentiometer connected to the ADC to simulate blood pressure values.
- **Local Display**: Results are shown on a 16x2 LCD display controlled through I2C using a PCA9555 I/O expander.
- **Keypad Interaction**: Includes a matrix keypad for user input, such as triggering a nurse call or resetting status.
- **Web Server Communication**: Sends vital signs data to a remote web server via USART communication with an ESP module (e.g., ESP8266).
- **Status Monitoring**: Automatically checks for abnormal readings and flags issues like "CHECKTEMP", "CHECKPRESSURE", or "RIP".
- **Real-time Updates**: Continuously monitors and transmits data in JSON format.

## Technologies and Protocols Used

- **AVR Microcontroller**: Core processing unit running at 16 MHz.
- **TWI (I2C)**: For interfacing with the PCA9555 I/O expander.
- **PCA9555**: I2C-based I/O expander for LCD and keypad control.
- **LCD Display**: 16x2 character LCD via I2C protocol.
- **USART**: Serial communication for data transmission to the ESP module.
- **One-Wire Protocol**: Dedicated to the DS18B20 temperature sensor.
- **Keypad Scanning**: Matrix keypad for user inputs.
- **GPIO**: General-purpose I/O for sensor and control signals.
- **ADC**: Analog-to-digital conversion for potentiometer readings.

## How It Works

1. **Initialization**: The system initializes TWI, LCD, USART, and the temperature sensor.
2. **Connection Setup**: Establishes connection to the ESP module and sets the target web server URL (e.g., `http://192.168.1.250:5000/data`).
3. **Data Acquisition**:
   - Reads temperature from DS18B20 sensor.
   - Samples potentiometer via ADC to simulate blood pressure.
4. **Status Evaluation**: Checks readings against thresholds to determine patient status (e.g., OK, NURSECALL, CHECKTEMP).
5. **Display and Transmission**:
   - Displays temperature, pressure, and status on the LCD.
   - Sends a JSON payload containing the data to the web server via ESP.
6. **User Interaction**: Monitors keypad for inputs like nurse calls or status resets.
7. **Loop**: Repeats the measurement and transmission cycle continuously.

## Requirements

- **Hardware**:
  - NTUA BOARD with AVR microcontroller.
  - DS18B20 temperature sensor.
  - Potentiometer for pressure simulation.
  - 16x2 LCD display.
  - PCA9555 I/O expander.
  - Matrix keypad.
  - ESP module (e.g., ESP8266) for Wi-Fi communication.
- **Software**:
  - AVR-GCC compiler.
  - AVRDUDE for programming the microcontroller.
  - Web server capable of receiving HTTP POST requests (e.g., Flask server at the specified URL).

## Setup and Usage

1. **Compile and Upload**:
   - Compile `main_code.c` using AVR-GCC.
   - Upload the binary to the AVR microcontroller using AVRDUDE.

2. **Hardware Connections**:
   - Connect DS18B20 to PD4 (One-Wire).
   - Connect potentiometer to PC0 (ADC).
   - Wire LCD and keypad via PCA9555 on I2C bus.
   - Connect ESP module via USART (RX/TX pins).

3. **Web Server**:
   - Set up a web server at `http://192.168.1.250:5000/data` to receive JSON payloads.
   - The payload format is: `[{"name":"temperature","value":"XX.X"},{"name":"pressure","value":"YY.0"},{"name":"team","value":"26"},{"name":"status","value":"STATUS"}]`

4. **Run**:
   - Power on the board.
   - The system will attempt to connect to the ESP and web server.
   - Monitor LCD for status and use keypad for interactions.

## Acknowledgments

Special thanks to Kostas Frantzeskos and Kostas Psarras for their cooperation throughout the semester. Parts of their code for communicating with the temperature sensor were incorporated into this project.

Developed by Ioannis Danias and Stavros Mitro for the Microcomputers Laboratory course at ECE NTUA.
