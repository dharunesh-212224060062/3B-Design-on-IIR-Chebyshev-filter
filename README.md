# IIR-FILTER-DESIGN

# EXP 3 B: DESIGN OF LOW PASS CHEBYSHEV IIR FILTER USING BILINEAR TRANSFORMATION

# AIM: 

# To a design of low pass Chebyshev IIR filter using Bilinear Transformation.

# APPARATUS REQUIRED: 
PC installed with SCILAB. 

# PROGRAM: 
```clc;
clear;

wp = input('Enter the passband frequency (radians) = ');
ws = input('Enter the stopband frequency (radians) = ');
alphap = input('Enter the passband attenuation (dB) = ');
alphas = input('Enter the stopband attenuation (dB) = ');
T = input('Enter the sampling time = ');

// Prewarping
omegap = (2/T)*tan(wp/2);
disp(omegap,'omegap = ');

omegas = (2/T)*tan(ws/2);
disp(omegas,'omegas = ');

// Filter Order
N = acosh(sqrt((10^(0.1*alphas)-1)/(10^(0.1*alphap)-1)))...
    /acosh(omegas/omegap);

disp(N,'N = ');

N = ceil(N);
disp(N,'Rounded value of N = ');

// Cutoff Frequency
omegac = omegap/((10^(0.1*alphap)-1)^(1/(2*N)));
disp(omegac,'omegac = ');

// Ripple Factor
epsilon = sqrt((10^(0.1*alphap))-1);
disp(epsilon,'epsilon = ');

// Analog Chebyshev Type-I LPF
[poles,gn] = zpch1(N,epsilon,omegap);

disp(gn,'Gain = ');

Hs = poly(gn,'s','coeff')/real(poly(poles,'s'));

disp(Hs,'Analog Low Pass Chebyshev Transfer Function = ');

// Bilinear Transformation
z = poly(0,'z');

Hz = horner(Hs,(2/T)*((z-1)/(z+1)));

disp(Hz,'Digital LPF Transfer Function H(z) = ');

// Frequency Response
Hw = frmag(Hz,512);

w = 0:%pi/511:%pi;

plot(w/%pi,abs(Hw));
xlabel('Normalized Digital Frequency');
ylabel('Magnitude');
title('Frequency Response of Chebyshev IIR LPF');
```

# OUTPUT: 
<img width="923" height="923" alt="WhatsApp Image 2026-06-10 at 7 08 42 PM" src="https://github.com/user-attachments/assets/8f733a06-18ba-4cfb-bec8-af68354c88ce" />
<img width="873" height="1167" alt="WhatsApp Image 2026-06-10 at 7 08 41 PM" src="https://github.com/user-attachments/assets/78e5fc3b-8266-43d5-b66c-c00d4aae0f4f" />


# RESULT: 
Thus design of Chebyshev Low pass IIR filter waveforms were plotted and output was
verified.
