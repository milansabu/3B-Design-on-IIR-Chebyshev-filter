# IIR-FILTER-DESIGN

# EXP 3 B: DESIGN OF LOW PASS CHEBYSHEV IIR FILTER USING BILINEAR TRANSFORMATION

# AIM: 

# To a design of low pass Chebyshev IIR filter using Bilinear Transformation.

# APPARATUS REQUIRED: 
PC installed with SCILAB. 

# PROGRAM: 
```
clc ; 
close ; 
wp=input('Enter the pass band frequency (Radians )= ' ); 
ws=input('Enter the stop band frequency (Radians )= ' ); 
alphap=input( ' Enter the pass band attenuation (dB)=' ); 
alphas=input( ' Enter the stop band attenuation(dB)=' ); 
T=input('Enter the Value of sampling Time='); 
 
//Pre warping- Bilinear Transformation 
omegap=(2/T)*tan(wp/2); 
disp(omegap,'omegap='); 
omegas=(2/T)*tan(ws/2); 
disp(omegas,'omegas=');

//Order of the filter  
N=acosh(sqrt(((10^(0.1*alphas))-1)/((10^(0.1*alphap))-1)))/(acosh(omegas/omegap)); 
disp(N,'N='); 
N=ceil(N); 
disp(N,'Round off value of N=');
 
//Cut off frequency 
omegac=omegap/(((10^(0.1*alphap)) -1)^(1/(2* N))); 
disp(omegac,'omegac=');
Epsilon = sqrt ((10^(0.1*alphap))-1);
disp(Epsilon,'Epsilon='); 
[pols ,gn] = zpch1(N, Epsilon,omegap ); 
disp(gn,'Gain'); 
disp(pols,'Poles'); 
hs=poly(gn,'s','coeff')/real(poly(pols,'s')); 
disp(hs,'Analog Low pass Chebyshev Filter Transfer function');
z=poly(0,'z');//Defining variable z 
Hz=horner(hs,(2/ T)*((z -1)/(z+1)))// Bilinear Transformation 
disp(Hz,'Digital LPF Transfer function H(Z)='); 
HW=frmag(Hz,512); // Frequency response 
w=0:%pi/511:%pi ; 
plot(w/%pi,abs(HW)); 
xlabel(' Normalized Digital Frequency w'); 
ylabel('Magnitude '); 
title(' Frequency Response of Chebyshev IIR LPF');
```
# CALCULATION:
<img width="1600" height="1200" alt="image" src="https://github.com/user-attachments/assets/bd2cd4ce-a159-46b6-bed9-2fb3d0312b73" />
<img width="1200" height="1600" alt="image" src="https://github.com/user-attachments/assets/d272d0a0-5a24-4fc0-bbba-6128ff63e8b0" />
<img width="1600" height="1200" alt="image" src="https://github.com/user-attachments/assets/8fb297f2-8a37-43a2-a2e0-5611acece17a" />

# OUTPUT: 
<img width="826" height="995" alt="image" src="https://github.com/user-attachments/assets/7e377df3-30c5-482d-8785-9e105f050ac3" />
<img width="757" height="706" alt="image" src="https://github.com/user-attachments/assets/856aa6d8-1250-42e2-9a66-2796bc5925e3" />


# RESULT: 
Thus design of Chebyshev Low pass IIR filter waveforms were plotted and output was
verified.
