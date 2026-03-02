# MRE_320_REPORT
# Sensor Measurement Report: Ultrasonic Ranging Module Sensor

## 1. Executive Summary
This report evaluates the performance of the HC-SR04 ultrasonic sensor against manufacturer specifications. Key findings indicate the sensor meets accuracy claims (±3mm) when detecting solid, flat objects within the specified range (2cm – 400cm). However, significant limitations were identified: the sensor fails entirely on soft or irregular surfaces (e.g., seashells, narrow cylinders), returning false timeout values (~2308cm). Precision is high across all successful tests, with variance typically under ±1mm. It is recommended for applications involving solid, flat targets but requires software filtering and error handling.

## 2. Objectives
-Characterize HC-SR04 accuracy against actual distance measurements

-Assess precision across multiple target types and distances

-Evaluate sensor limitations with different object materials and geometries

-Verify manufacturer specifications against real-world performance

## 3. Experimental Setup
### 3.1 Hardware
- **Sensor:** HC-SR04 Ultrasonic Sensor
- **Microcontroller:** Arduino Uno R3
- **Reference:** Book (flat), Purple Vase (curved), Vase of Seashells (complex), Hairspray Can (narrow cylinder)
- **Environmental chamber:** Measuring Tape (cm)

### 3.2 Configuration
- Sampling rate: 1 Hz
- Duration: 72 hours continuous
- I²C communication at 100 kHz

![Setup photo](images/test_setup.jpg)
Arduino Uno           HC-SR04
-----------           -------
5V        ─────────► VCC
GND       ─────────► GND
Pin 9     ─────────► Trig
Pin 10    ─────────► Echo
## 4. Results
### 4.1 Accuracy Comparison
![Temperature comparison plot](images/accuracy_plot.png)

*Figure 2: DHT22 vs. reference thermometer over 0-50°C range*

| Temperature | DHT22 Reading | Reference | Error |
|-------------|---------------|-----------|-------|
| 0°C | 0.8°C | 0.0°C | +0.8°C |
| 25°C | 25.3°C | 25.0°C | +0.3°C |
| 50°C | 51.2°C | 50.0°C | +1.2°C |

### 4.2 Response Time
- 63% response time: 12 seconds
- 90% response time: 35 seconds

## 5. Discussion
The DHT22 shows good accuracy (±0.5°C) in the 10-40°C range but deviates significantly at extremes. Response time is adequate for environmental monitoring but too slow for rapid process control.

## 6. Conclusions and Recommendations
- Suitable for indoor climate monitoring
- Not recommended for freezer or oven applications
- Consider adding weatherproof housing for outdoor use

## 7. References and Appendices
- Appendix A: Raw data files
- Appendix B: Calibration certificates
- Appendix C: Python analysis scripts        
