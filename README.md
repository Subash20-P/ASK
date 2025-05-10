# Amplitude Shift Keying (ASK)

# Aim
Write a Python program for the modulation and demodulation of ASK.

# Tools Required
- **Python**: A versatile programming language for scientific computing and signal processing.
- **NumPy**: A numerical library for array-based operations and mathematical computations.
- **Matplotlib**: A plotting library for generating high-quality graphs and visualizations.
- **SciPy**: A library for scientific computing, used for signal processing (Butterworth filter).

# Program
```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import butter, lfilter

# Butterworth low-pass filter for demodulation
def butter_lowpass_filter(data, cutoff, fs, order=5):
    nyquist = 0.5 * fs
    normal_cutoff = cutoff / nyquist
    b, a = butter(order, normal_cutoff, btype='low', analog=False)
    return lfilter(b, a, data)

# Parameters
fs = 1000                # Sampling frequency (Hz)
f_carrier = 50           # Carrier frequency (Hz)
bit_rate = 10            # Data rate (bits per second)
T = 1                    # Total time duration (seconds)
t = np.linspace(0, T, int(fs * T), endpoint=False)

# Message signal (binary data)
bits = np.random.randint(0, 2, bit_rate)
bit_duration = fs // bit_rate
message_signal = np.repeat(bits, bit_duration)

# Carrier signal
carrier = np.sin(2 * np.pi * f_carrier * t)

# ASK Modulation
ask_signal = message_signal * carrier

# ASK Demodulation
demodulated = ask_signal * carrier  # Multiply by carrier for coherent detection
filtered_signal = butter_lowpass_filter(demodulated, f_carrier, fs)
decoded_bits = (filtered_signal[::bit_duration] > 0.25).astype(int)

# Plotting
plt.figure(figsize=(12, 8))

plt.subplot(4, 1, 1)
plt.plot(t, message_signal, label='Message Signal (Binary)', color='b')
plt.title('Message Signal')
plt.grid(True)

plt.subplot(4, 1, 2)
plt.plot(t, carrier, label='Carrier Signal', color='g')
plt.title('Carrier Signal')
plt.grid(True)

plt.subplot(4, 1, 3)
plt.plot(t, ask_signal, label='ASK Modulated Signal', color='r')
plt.title('ASK Modulated Signal')
plt.grid(True)

plt.subplot(4, 1, 4)
plt.step(np.arange(len(decoded_bits)), decoded_bits, label='Decoded Bits', color='r', marker='x')
plt.title('Decoded Bits')

plt.tight_layout()
plt.show()
```

# OUTPUT
![download (8)](https://github.com/user-attachments/assets/5434dd89-99c5-4131-a941-2ee2e63d9b24)
![WhatsApp Image 2025-05-10 at 23 05 43_f65c072d](https://github.com/user-attachments/assets/c93fbe9c-bf53-47c7-82b2-cf1c3bb4bfb4)

# RESULT
THUS THE ASK (Amplitude Shift Keying) IS PERFORMED USING PYTHON
