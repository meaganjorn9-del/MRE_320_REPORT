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


## 4. Results
### 4.1 Accuracy Comparison
*Figure 2: HC-SR04 vs. reference distance over 15-314 cm range*

|Actual Distance	Sensor Reading (Avg)|	Reference| Distance|	Error|
|--------|--------|---------|-------|
|15.88 cm	|15.95 cm	|15.88 cm	|+0.07 cm|
|36.83 cm	|35.84 cm	|36.83 cm	|-0.99 cm|
|85.73 cm	|84.65 cm	|85.73 cm	|-1.08 cm|
|314.00 cm*|	314.02 |cm	314.00 cm|+0.02 cm|

**Excluding timeout errors; 50% of readings at this distance were false timeouts (~2308 cm)*


4.2 Material Sensitivity Results
*Figure 3: HC-SR04 performance on different surface types at ~44 cm distance*

|Object|	Surface Type|	Sensor Reading (Range)|	Result|
|--------|--------|---------|-------|
|Book	Flat| solid, paper	|44.32 – 44.78 cm|	✅ Pass|
|Purple Vase	Curved|smooth, ceramic|	43.61 – 44.08 cm|	✅ Pass|
|Seashell Vase	Complex|irregular, porous	|2306.06 – 2306.83 cm	|❌ Fail|
|Hairspray Can	Narrow cylinder| metal|	2305.47 – 2308.32 cm|	❌ Fail|

4.3 Precision Analysis
Figure 4: Measurement variability at each test distance

|Test Distance	|Sample Count|	Mean Reading|	Standard Deviation|	Variance|
|--------|--------|---------|-------|--------|
|15.88 cm	|9|	15.95 cm|	±0.18 cm|	0.03 cm²|
|36.83 cm	|10|	35.84 cm|	±0.05 cm|	0.0025 cm²|
|85.73 cm	|9|	84.65 cm|	±0.35 cm|	0.12 cm²|
|314.00 cm*|	4	|314.02 cm|	±1.52 cm|	2.31 cm²|

*Excluding timeout errors

4.4 Failure Mode Analysis
Figure 5: Timeout values observed during testing

|Condition|	Observed Reading|	Theoretical| Maximum	Error Type|
|--------|--------|---------|-------|
|No echo (soft surface)	|2306.06 – 2306.83 cm	|2308 cm|	Sensor timeout|
|No echo (narrow object)|	2305.47 – 2308.32 cm|	2308 cm	|Sensor timeout|
|Out of range (>400 cm)	|2308.22 – 2308.92 cm	|2308 cm	|Sensor timeout|

4.5 Spec Sheet Verification
Figure 6: Manufacturer specifications vs. test results

|	Parameter	Manufacturer Claim|	Test Result	Verdict|	
|---------|-------|
|	Operating Range	2 – 400 cm	15 – 314 cm verified	|	✅ Pass|	
|	Accuracy	±3 mm	0.7 – 10.8 mm observed|		⚠️ Partial*|	
|	Operating Frequency	40 kHz	Assumed correct|		✅ Pass|	
|	Material Sensitivity	Not specified	Fails on irregular surfaces|⚠️ Limitation identified|	

*Accuracy within spec for flat surfaces at close range; deviates at mid-range and extreme distances

4.6 Summary Statistics
Figure 7: Combined performance metrics

|Metric|Value|Notes|
|---------|---------|---------|
|Best Accuracy|	±0.07 cm|	At 15.88 cm distance|
|Worst Accuracy	|±1.08 cm	|At 85.73 cm distance|
|Best Precision|	±0.05 cm|	At 36.83 cm distance|
|Worst Precision|	±1.52 cm|	At 314.00 cm distance*|
|Success Rate (Flat)|	100%	|Book, vase, wall targets|
|Success Rate (Complex)|0%|Seashells, hairspray can|



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
