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
- Sampling rate: ~4 Hz (limited by echo timeout)
- Operating Voltage: 5Vdc (via Arduino)
- Communication: Digital pulse timing (trigger/echo pins)
- Test Distances: 15.88 cm, 36.83 cm, 85.73 cm, 314.00 cm

![Setup photo](images/test_setup.jpg)
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
The HC-SR04 demonstrates excellent precision and meets its ±3mm accuracy specification when detecting solid, flat objects. However, the sensor's performance is highly dependent on target characteristics. Soft, porous, or geometrically complex surfaces scatter or absorb the ultrasonic waves, preventing the echo from returning to the receiver. In these failure cases, the microcontroller timer runs until it times out, resulting in false readings near 2308 cm (the maximum distance calculable based on the 38ms timeout period). This behavior is not detailed in the basic spec sheet and represents a critical limitation for general-purpose use. The sensor shows a consistent underestimation of approximately 1 cm in the 35-85 cm range, suggesting a systematic offset that could be calibrated in software.

## 6. Conclusions and Recommendations
Suitable for: Distance measurement against solid, flat surfaces (walls, floors, large panels); robotics obstacle avoidance (with appropriate targets); liquid level sensing (if surface is calm and reflective)

Not recommended for: Objects with soft fabrics, irregular textures, or complex geometry; environments with acoustic noise interference; applications requiring detection of narrow objects

Implementation Notes: Software filtering (median or moving average) is recommended to smooth minor fluctuations. Error handling must be implemented to discard timeout values (~2308 cm)

Calibration: Consider applying distance-dependent correction factors to improve absolute accuracy


## 7. References and Appendices
- Appendix A: 
- Appendix B: 
- Appendix C:      
