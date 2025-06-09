# Audio Modem with FSK in Real-Time

This project implements a simple audio modem using Frequency-Shift Keying (FSK) to transmit and receive text messages in real time over standard speakers and microphones.

## Features

- **Real-time transmission and reception** of text via FSK  
- **Goertzel-based tone detection** with automatic noise-floor calibration  
- **Configurable parameters**: sample rate, bit duration, FSK frequencies, sync header, detection threshold  
- **Sync header detection** for reliable framing and message alignment  
- **Cross-platform compatibility** (Windows, macOS, Linux)  

## Requirements

- **Python 3.7+**  
- **Libraries** (install via pip):  
  ```bash
  pip install numpy sounddevice scipy
