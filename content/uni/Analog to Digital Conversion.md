For a computer to use an analog signal, it needs to be digitised with an analog-to-digital converter (A/D converter)![[Screenshot 2026-07-02 at 16.26.46.png]]

## Sampling
The first step is sampling - turning a continuous signal into discrete signal, every stem in the discrete signal represent sample values, and there is a fixed interval between the stems, meaning some information is lost.

The analog signal is given by:

$$
	x(t) = (0.85)^t
$$
For sampling, we have to decide a sampling interval, $T$. We define sampling interval by setting the sampling frequency $f_s$. For simplicity suppose

$$
f_s = 1Hz.
$$
$$
T = 1/f_s
$$
$$
T = 1s
$$
For sampling replace  $t = nT$.
Thus,
$$
x(nT) = (0.85)^nT
$$
Since $T = 1s$, therefore,
$$
x(n) = (0.85)^n
$$
$x(n)$ is the discrete time signal with sampling interval of $1s$.![[Screenshot 2026-07-02 at 16.39.05.png]]

## Quantisation
Quantisation is the process of converting the amplitude of discrete signal into a digital signal by expressing each sample value as a finite number of digits - basically rounding the stems to a set amplitude, the accuracy of the signal representation is directly proportional to how many discrete levels are allowed to represent the magnitude of the signal.