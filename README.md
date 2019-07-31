# AudioProcessing
An toolbox for audio processing in Matlab,the verison of Matlab is R2016a. </br>
The audio sample in this toobox is 8000Hz, 16 bits.

## 1. getAudioFingerpriner
[getAudioFingerprinter](https://github.com/DandelionLau/AudioProcessing-toolbox/blob/master/getAudioFingerprinter.m) calcuates the difference of the energy of each frequency sub-band as shown below.  
![Extraction process](https://github.com/DandelionLau/AudioProcessing/blob/master/pic/audiofingerprinter.jpg)

Specifically, the extraction process including the following steps:
1. divide audio into frames, the overlap length is alterable
2. do fft for each frame 
3. divide frequency spectrum into 32 frequency sub bands
4. calcuate the energy of each sub band
5. calcuate audio fingerprinter as follow  
![Bit Derviation](https://github.com/DandelionLau/AudioProcessing/blob/master/pic/bitDerivation.JPG)

The result is shown below
![printer](https://github.com/DandelionLau/AudioProcessing/blob/master/pic/fingerprinter.png)

## 2. getZCR
[getZCR](https://github.com/DandelionLau/AudioProcessing-toolbox/blob/master/getZCR.m) calcuates the zero-crossing rate which can be used to predict the frequency roughly.
Specifically, the extraction process including the following steps:
1. divide audio into frames 
2. calcuate zcr of each frame using the following equation

![ZCR](https://github.com/DandelionLau/AudioProcessing/blob/master/pic/ZCR.JPG)                      
where sgn(x) is given by  
![sgn(x)](https://github.com/DandelionLau/AudioProcessing/blob/master/pic/sgn.JPG)  
The result is shown below  
![zcrpic](https://github.com/DandelionLau/AudioProcessing/blob/master/pic/ZeroCrossingRate.png)  

## 3. getLandmarks
calcuate the enegry max points(also called landmark) in frequency spectrum 
1. divide audio into frames, the overlap length is alterable
2. do fft for each frame 
3. calcuate the energy of frequency 
4. calcuate the local maximum as landmark
The result is shown below
![landmark-2d](https://github.com/DandelionLau/AudioProcessing-toolbox/blob/master/pic/landmark-2d.png)
![landmark-3d](https://github.com/DandelionLau/AudioProcessing-toolbox/blob/master/pic/landmark-3d.png)

## 4. getEnergy
calcuate the short-time energy</br>
1.divide audio into frames, the overlap length is alterable</br>
2.calcuate the energy using the following equation:</br>
![stenergy](https://github.com/DandelionLau/AudioProcessing-toolbox/blob/master/pic/short-time-energy.png)

The result is shown below</br>
![getEnrgy](https://github.com/DandelionLau/AudioProcessing-toolbox/blob/master/pic/getEnergy.png)

## 5. getSpecgram
Implementation of matlab function Specgram() 
1. divide signal into frames in time domain</br>
2. do fft of each frame</br>
![specgram](https://github.com/DandelionLau/AudioProcessing-toolbox/blob/master/pic/specgram.png)

## 6. getLMSPredictor
![LMS](https://github.com/DandelionLau/AudioProcessing-toolbox/blob/master/pic/LMSPredictor.JPG)
```
where a = b = 0.953125 
r0 = r1 = 0
COR0 = COR1 =0
VAR0 = VAR1 = 1
The update procedure is shown below:
  K1(n) = b*COR0(n-1)/VAR0(n-1);
	K2(n) = b*COR1(n-1)/VAR1(n-1);
	Xest(n) =  K1(n)*r0(n-1) + K2(n)*r1(n-1);
	e0(n) = Xrec(n);
	e1(n) = e0(n) - K1(n)*r0(n-1);
	VAR0(n) = u*VAR0(n-1) + 0.5*[r0(n-1)^2+e0(n)^2];
	COR0(n) = u*COR0(n-1) + r0(n-1)*e0(n);
	VAR1(n) = u*VAR1(n-1) + 0.5*[r1(n-1)^2+e1(n)^2];
	COR1(n) = u*COR1(n-1) + r1(n-1)*e1(n);
	r1(n) = a*(r0(n-1)-K1(n)*e0(n));
	r0(n) = a*e0(n);
	Xerr(n) = Xrec(n) - Xest(n);
```
The function returns the estimate value Xest and the setimate error Xerr
