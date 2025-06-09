# FSK Audio Modem

A Python-based audio modem using Frequency-Shift Keying (FSK) to transmit and receive text messages in real time over standard speakers and microphones.

### This project uses https://github.com/sunw4r/audio_modem repo 

## Features

* **Real-time Tx/Rx** of text via two audio tones
* **Goertzel filter**–based tone detection with automatic noise-floor calibration
* **Configurable** sample rate, bit duration, FSK frequencies, sync header, detection threshold
* **Sync header framing** for reliable packet alignment
* **Cross-platform** (Windows, macOS, Linux)

## Requirements

* Python 3.7 or higher
* `numpy`
* `scipy`
* `sounddevice`

Install dependencies:

```bash
pip install numpy scipy sounddevice
```

## File Overview

**fsk\_transmissor.py**

* Converts text to bitstream
* Generates FSK sine-waves for ‘0’ and ‘1’ bits
* Plays audio via default output device

**fsk\_receptor.py**

* Captures audio from default input device
* Calibrates noise floor over multiple windows
* Applies Goertzel filters to detect 1200 Hz/2500 Hz tones
* Searches for 8-bit sync header then reconstructs characters

## Configuration

Edit parameters at the top of each script:

```python
# Common to Tx & Rx
sample_rate    = 48000       # Sampling rate in Hz
duration       = 0.1         # Bit duration in seconds
freq_0         = 1200        # Tone for bit ‘0’ in Hz
freq_1         = 2500        # Tone for bit ‘1’ in Hz
header         = '10101010'  # 8-bit sync pattern
```

Additional Rx-only settings in **fsk\_receptor.py**:

```python
calib_windows       = 5      # Windows for noise-floor calibration
detection_threshold = 0.5    # Goertzel magnitude threshold
```

## Usage

### Transmit

```bash
python fsk_transmissor.py "Hello, world!"
```

Outputs an FSK-modulated audio stream carrying your message.

### Receive

```bash
python fsk_receptor.py
```

Listens continuously; prints any decoded messages when the sync header is detected.

## Troubleshooting

* **No tones or static noise:**

  * Verify your speaker/mic works at the chosen frequencies.
  * Try lower/higher `freq_0` & `freq_1` values.

* **Bit errors or garbled text:**

  * Increase `duration` to give each bit more time.
  * Lower `detection_threshold` for more sensitive detection.

* **High ambient noise:**

  * Increase `calib_windows` to improve noise-floor estimate.
  * Run in a quieter environment or use a directional microphone.


