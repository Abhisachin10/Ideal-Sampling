# Ideal, Natural, & Flat-top -Sampling
# Aim
Write a simple Python program for the construction and reconstruction of ideal, natural, and flattop sampling.
# Tools required
# Program

**IDEAL SAMPLING**
```
import matplotlib.pyplot as plt

fs = 100
f = 5
t = np.arange(0, 1, 1/fs)
x = np.sin(2*np.pi*f*t)

# Continuous signal
plt.figure(figsize=(10, 3))
plt.plot(t, x)
plt.title("Continuous Signal")
plt.grid()
plt.show()

# Ideal sampling
plt.figure(figsize=(10, 3))
plt.stem(t, x)
plt.title("Ideal Sampling")
plt.grid()
plt.show()

# Reconstruction (Interpolation)
t_rec = np.linspace(0, 1, 1000)
x_rec = np.interp(t_rec, t, x)

plt.figure(figsize=(10, 3))
plt.plot(t_rec, x_rec)
plt.title("Reconstructed Signal")
plt.grid()
plt.show()
```

**NATURAL SAMPLING**
```
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import butter, lfilter

t = np.linspace(0,1,1000)
x = np.cos(2*np.pi*5*t)

p = ((t*50)%1 < 0.5)        # pulse train
xn = x * p                 # natural sampling

b,a = butter(4, 10/(0.5*1000))
xr = lfilter(b, a, xn)

plt.figure(figsize=(10,2))
plt.plot(t,x)
plt.title("Message Signal")
plt.grid()
plt.show()

plt.figure(figsize=(10,2))
plt.plot(t,p)
plt.title("Pulse Train")
plt.grid()
plt.show()

plt.figure(figsize=(10,2))
plt.plot(t,xn)
plt.title("Natural Sampling")
plt.grid()
plt.show()

plt.figure(figsize=(10,2))
plt.plot(t,xr)
plt.title("Reconstructed Signal")
plt.grid()
plt.show()
```
**FLAT-TOP SAMPLING**
```
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import butter, filtfilt

fs = 1000
t = np.linspace(0, 1, fs)
x = np.sin(2*np.pi*5*t)

Ts = fs//50                          # sampling interval
n = np.arange(0, fs, Ts)             # ideal sampling instants

xh = np.repeat(x[n], Ts)[:fs]        # flat-top (sample & hold)

b, a = butter(4, 10/(0.5*fs))
xr = filtfilt(b, a, xh)

plt.figure(figsize=(10,3))
plt.plot(t, x)
plt.title("Message Signal")
plt.grid()
plt.show()

plt.figure(figsize=(10,3))
plt.stem(t[n], x[n], basefmt=" ")
plt.title("Ideal Sampling Instances")
plt.grid()
plt.show()

plt.figure(figsize=(10,3))
plt.plot(t, xh)
plt.title("Flat-Top Sampling")
plt.grid()
plt.show()

plt.figure(figsize=(10,3))
plt.plot(t, xr)
plt.title("Reconstructed Signal")
plt.grid()
plt.show()
```
# Output Waveform

**IDEAL SAMPLING**

<img width="707" height="742" alt="image" src="https://github.com/user-attachments/assets/c25597d2-b214-4605-bda4-ceb81b2461f7" />

**NATURAL SAMPLING**

<img width="708" height="726" alt="image" src="https://github.com/user-attachments/assets/c512843b-8233-4ccc-a019-42f8c3bbf40c" />

**FLAT-TOP SAMPLING**

<img width="528" height="740" alt="image" src="https://github.com/user-attachments/assets/01cae905-84d5-47b3-8d4d-b993007b1fe2" />



# Results

Thus, the python program for ideal sampling, natural sampling and flat-top sampling has been executed and verified successfully.

