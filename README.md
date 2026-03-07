# MRE_320_REPORT  
# Sensor Measurement Report: Sound Sensor Module

## 1. Executive Summary
This report evaluates the performance of a sound sensor by testing three main characteristics: **range, sensitivity, and precision**. Results show that the sensor operates most reliably in the mid-range sound levels. The lower usable limit was observed near **60 dB**, where readings below this point became inconsistent. Sensitivity testing showed that the sensor’s RMS output increased with sound level, but the response was not perfectly linear. Precision testing showed that the sensor produced repeatable results in the main operating range, although performance worsened at higher sound levels.

Overall, the sensor is suitable for detecting and comparing sound intensity over a moderate range, but it is less reliable at very low or very high sound levels.

---

## 2. Objectives
- Determine the **usable range** of the sound sensor
- Measure the **sensitivity** of the sensor to changing sound levels
- Evaluate the **precision** of repeated measurements
- Identify limitations in sensor response

---

## 3. Experimental Setup

### 3.1 Hardware
- **Sensor:** Analog Sound Sensor Module
- **Microcontroller:** Arduino Uno R3
- **Signal Source:** JBL Flip 6 Speaker 25 cm away from sensor
- **Reference Measurement:** dB level app with iPhone 
- **Environment:** Quiet indoor room

### 3.2 Configuration
- Quiet room baseline: **~40 dB**
- Calibration signal: **1 kHz tone at 70 dB**
- Multiple samples were collected at each sound level
- Sound levels tested: **60 dB - 100 dB**

---

### 3.3 Calibration
The sound sensor was calibrated using a **1 kHz tone at 70 dB** measured using the reference sound level app. The RMS output measured at this sound level was defined as the calibration reference point.

Calibration reference:

**70 dB → RMS = 1**

Multiple RMS measurements were taken at different sound levels to determine the relationship between the sensor output (RMS) and the corresponding sound level in decibels.

| Sound Level (dB) | RMS Output |
|---|---:|
| 60 | 0.5 |
| 65 | 0.6 |
| 70 | 1.0 |
| 75 | 1.8 |
| 80 | 2.3 |
| 85 | 4.5 |


Using these measurements, a logarithmic relationship between RMS output and sound level was determined. Because decibel measurements are inherently logarithmic, the data was fit to a logarithmic regression model.

The resulting calibration equation is:

**dB = 25.3 log(RMS) + 69.3**

Where:

- **dB** = estimated sound level in decibels  
- **RMS** = measured RMS voltage from the sound sensor

This equation was derived by applying a logarithmic curve fit to the measured RMS vs sound level data points. The coefficients **25.3** and **69.3** were determined from the regression analysis and represent the slope and offset needed to convert RMS output values into approximate decibel levels.

This calibration equation was then used to convert sensor RMS readings into estimated sound level values during testing.

---

## 4. Results

### 4.1 Range Testing
*Figure 1: Sensor operating range based on observed measurements*

The sensor was tested across a range of sound levels to determine where it responded consistently.

| Sound Level (dB) | Observation |
|---|---|
| Below 60 | RMS readings unstable |
| 60–95 | Reliable operating range |
| Above 95 | Response becomes significantly less accurate |

**Result:**  
The approximate usable range of the sound sensor is:

**60 dB – 95 dB**

The lower limit of **60 dB** was determined experimentally from the sensor readings in a quiet room environment. In this condition the measured sound level was approximately **60 dB**, representing the baseline reading of the sensor. When the input sound level dropped below this value, the RMS output became unstable and fluctuated significantly, making the measurements unreliable.

At the upper end of the tested range, measurements remained reasonable up to approximately **95 dB**. At **100 dB**, however, the measurement error increased substantially, indicating that the sensor response becomes increasingly nonlinear near the upper limit of the tested range.
---

### 4.2 Sensitivity Testing

Sensitivity describes how strongly the sensor output changes in response to changes in sound level. To evaluate this behavior, the sensor output was recorded for several sound levels and averaged over **10 samples** at each level.

### Sensitivity Measurements

| Input dB | Output dB (avg of 10 samples) | Sensitivity |
|---|---|---|
| 60 | 60.23 | — |
| 65 | 65.17 | 1.012145749 |
| 70 | 67.74 | 1.945525292 |
| 75 | 74.15 | 0.780031201 |
| 80 | 79.45 | 0.943396226 |
| 85 | 85.54 | 0.821018062 |
| 90 | 92.64 | 0.704225352 |
| 95 | 98.94 | 0.793650794 |
| 100 | 106.56 | 0.656167979 |

### Sensitivity Graph

<img width="561" height="418" alt="image" src="https://github.com/user-attachments/assets/168c99b0-9221-498f-a5f2-56e8f741896c" />


The graph shows the relationship between **input sound level (dB)** and the **measured sensor output (dB)**.

### Linear Region Analysis

From the plotted data, the sensor response appears approximately linear between **75 dB and 95 dB**. This region was selected to determine the effective sensitivity of the sensor because it represents the most stable portion of the response curve.

Sensitivity was calculated from the slope of the linear portion of the graph:

Sensitivity = ΔInput / ΔOutput

Using the values from the linear region:

Input change:  
95 dB − 75 dB = **20 dB**

Output change:  
98.94 dB − 74.15 dB ≈ **16.1 dB**

Resulting sensitivity:

**Sensitivity ≈ 1.24 dB input / dB output**

This value represents the approximate rate at which the sensor output changes relative to changes in input sound level within the most linear operating region.

---

### Manufacturer Specifications

The following specifications are provided by an available datasheet for the **KY-037 sound sensor module**.

| Parameter | Specification |
|---|---|
| Operating Voltage | 3.3V – 5.5V |
| Microphone Sensitivity | -42 ±3 dB |
| Current Consumption | ~0.5 mA |
| Board Dimensions | 15 mm × 36 mm (0.6 in × 1.4 in) |

Source: **arduinomodels.info**

**Note:**  
This specification sheet from *arduinomodels.info* was the only publicly available datasheet found for the **KY-037 sound sensor module** during this project. Many KY-037 modules sold online do not include detailed manufacturer documentation, so the listed specifications were used as the closest available reference.

## Comparison to Experimental Results

The datasheet lists a **microphone sensitivity of -42 ±3 dB**, which refers to the electrical response of the microphone element itself. The experimental sensitivity calculated in this project represents the response of the **entire sensor module**, including the microphone, amplifier, and output circuitry.

Experimental results show that the sensor responds consistently to changes in sound level within the 75–95 dB range, where the response is approximately linear. Outside of this region the sensor response becomes increasingly nonlinear, which is consistent with the behavior of small amplified microphone modules.
---
### 4.3 Precision Testing

Precision describes how consistently the sensor produces the same output when measuring the same sound level multiple times. To evaluate precision, **10 samples were collected at each sound level**, and the average output value was calculated.

### Average Sensor Output

| Input dB | Output dB (avg of 10 samples) |
|---|---:|
| 60 | 60.23 |
| 65 | 65.17 |
| 70 | 67.74 |
| 75 | 74.15 |
| 80 | 79.45 |
| 85 | 85.54 |
| 90 | 92.64 |
| 95 | 98.94 |
| 100 | 106.56 |

<img src="images/output_vs_input.png" width="900">

---

### Measurement Error

Error was calculated as the difference between the measured sensor output and the input sound level:

**Error = Output dB − Input dB**

| Input dB | Error (dB) |
|---|---:|
| 60 | 0.23 |
| 65 | 0.17 |
| 70 | -2.26 |
| 75 | -0.85 |
| 80 | -0.55 |
| 85 | 0.54 |
| 90 | 2.64 |
| 95 | 3.94 |
| 100 | 6.56 |

<img src="images/error_vs_db.png" width="900">

---

### Precision Analysis

Precision was further evaluated using the **standard deviation of the sensor output measurements**, which quantifies the variability of the data around the mean.

The calculated standard deviation of the measurements was:

**Standard Deviation = 2.7379 dB**

This value represents the typical spread of the sensor readings relative to the average measured value. Based on this result, the precision of the sensor can be approximated as:

**Precision ≈ ±3 dB**

This means that repeated measurements at the same sound level typically vary by about **3 dB from the mean value**.

The results show that the sensor maintains relatively good precision within the **mid-range sound levels (65–85 dB)**, where measurement error remains small. However, as the sound level increases above **90 dB**, the error increases and the sensor response becomes less consistent.

Experimental results also show that the sensor responds consistently to changes in sound level within the **75–95 dB range**, where the response is approximately linear. Outside of this region, the sensor response becomes increasingly nonlinear, which is consistent with the behavior of small amplified microphone modules.

Overall, the sensor demonstrates acceptable precision for moderate sound level measurements but becomes less reliable near the upper limits of the tested range.
---

## 6. Conclusions and Recommendations

### Conclusions
- The sensor’s usable range is approximately **60 dB to 90 dB**
- Sensitivity increases with sound level, but the response is **nonlinear**
- Precision is best in the **65 dB to 85 dB** range
- Performance decreases outside the mid-range region

### Recommendations
- Use the sensor mainly in the **mid-range operating region**
- Apply filtering to reduce unstable readings
- Use multi-point calibration if better sensitivity modeling is needed
- Avoid using the sensor for very quiet or very loud sound measurements

---

## 7. Sensor Code

https://app.arduino.cc/sketches/2e772baf-376d-4302-96f5-2350e1bbb418?nav=Files&view-mode=preview

---

## 8. Sensor Wiring Diagram

Wiring:

- **VCC → 5V**
- **GND → GND**
- **OUT → A0**

---

## 9. References and Appendices

### References
- KY-037 Sound Sensor specifications, *ArduinoModels.info*  
  https://arduinomodels.info/ky-037-sound-sensor-module/

### Appendices
- **Appendix A:** Raw measurement data (`Sound Sensor Testing.xlsx`)
- **Appendix B:** Calibration data and RMS measurements used to derive the equation  
  **dB = 25.3 log(RMS) + 69.3**
- **Appendix C:** Sensitivity calculations and input/output graph
- **Appendix D:** Precision calculations including error values and standard deviation  
  (**σ = 2.7379 dB**, precision ≈ **±3 dB**)
- **Appendix E:** Arduino code used for data collection  
  https://app.arduino.cc/sketches/2e772baf-376d-4302-96f5-2350e1bbb418
