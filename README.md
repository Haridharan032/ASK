# ASK
# Aim
Write a simple Python program for the modulation and demodulation of ASK and FSK.
# Tools required
Google colab
# Thoery
## Theory
Theory
Amplitude Shift Keying (ASK) is a digital modulation technique in which the amplitude of the carrier signal changes according to the binary input data while frequency and phase remain constant.

For binary 1, the carrier signal is transmitted.

For binary 0, the carrier signal is absent or reduced.

In ASK, the binary message signal is multiplied with a high-frequency carrier signal to produce the modulated waveform.

The ASK signal is given by  $s(t)=m(t)A_c\sin(2\pi f_c t)$

Where:
$m(t)$ = Message signal

$A_c$​ = Carrier amplitude

$f_c$​ = Carrier frequency


At the receiver side, the ASK signal is demodulated by multiplying it with the carrier signal and passing it through a low-pass filter to recover the original binary data.
In this experiment, Python is used to generate the message signal, carrier signal, ASK modulated signal, and decoded output waveform.
# Program
```
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import butter, lfilter

# Low-pass filter
def lpf(x, fc, fs):
    b, a = butter(4, fc/(0.5*fs), 'low')
    return lfilter(b, a, x)

# Parameters
fs, fc, br, T = 1000, 50, 10, 1
t = np.arange(0, T, 1/fs)

# Message signal
bits = np.random.randint(0, 2, br)
msg = np.repeat(bits, fs//br)

# Carrier signal
carrier = np.sin(2*np.pi*fc*t)

# ASK modulation & demodulation
ask = msg * carrier
demod = lpf(ask * carrier, fc, fs)
decoded = (demod[::fs//br] > 0.25).astype(int)

# Plot
plt.figure(figsize=(10,9))
plt.suptitle("NAME :HARIDHARAN G\nREG NO : 212224060090",fontsize=12, fontweight='bold')

plt.subplot(4,1,1)
plt.plot(t, msg)
plt.title("Message Signal")

plt.subplot(4,1,2)
plt.plot(t, carrier)
plt.title("Carrier Signal")

plt.subplot(4,1,3)
plt.plot(t, ask)
plt.title("ASK Modulated Signal")

plt.subplot(4,1,4)
plt.step(range(len(decoded)), decoded, where='mid')
plt.title("Decoded Bits")

plt.tight_layout(rect=[0,0,1,0.93])
plt.show()

```
# Output Waveform
<img width="899" height="816" alt="image" src="https://github.com/user-attachments/assets/178243e3-1d4a-4bdd-91c8-c3d942be74bd" />

# Results
Thus the ASK experiment has been completed and it is verified successfully
