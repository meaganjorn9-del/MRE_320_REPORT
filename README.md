# Sound Sensor Characterization

## Overview
This project evaluates the performance characteristics of a sound sensor by comparing measured sound levels with known reference sound levels.

The objectives were to determine:

- Sensor sensitivity
- Measurement accuracy
- RMS response to sound level
- Operating range of the sensor

---

# Experimental Setup

### Reference Conditions

Silent room baseline:

40 dB

Calibration signal:

1 kHz tone at **70 dB**

During calibration:

70 dB → RMS = 1

This value was used to normalize all RMS measurements.

---

# RMS Response vs Sound Level

| Sound Level (dB) | RMS Output |
|------------------|-----------|
| 60 | 0.5 |
| 65 | 0.6 |
| 70 | 1.0 |
| 75 | 1.8 |
| 80 | 2.3 |
| 85 | 4.5 |

### Graph

![RMS vs dB](images/rms_vs_db.png)

### Observation

Below **60 dB**, the RMS values became inconsistent, indicating the lower detection limit of the sensor.

---

# Accuracy Testing

Average sensor output was calculated using **10 samples** for each sound level.

| Input dB | Sensor Output (dB) | Error (dB) |
|---------|-------------------|-----------|
| 60 | 60.23 | +0.23 |
| 65 | 65.17 | +0.17 |
| 70 | 67.74 | -2.26 |
| 75 | 74.15 | -0.85 |
| 80 | 79.45 | -0.55 |
| 85 | 85.54 | +0.54 |
| 90 | 92.64 | +2.64 |
| 95 | 98.94 | +3.94 |
| 100 | 106.56 | +6.56 |

### Graph

![Sensor Output vs Input](images/output_vs_input.png)

---

# Measurement Error

Error was calculated as:

Error = Sensor Reading − Actual Sound Level

### Graph

![Error vs dB](images/error_vs_db.png)

### Observations

- Small error between **65 dB and 85 dB**
- Sensor begins to **overestimate** above **90 dB**
- Accuracy decreases significantly near **100 dB**

---

# Sensor Sensitivity

| Input dB | Sensitivity |
|---------|------------|
| 65 | 1.01 |
| 70 | 1.95 |
| 75 | 0.78 |
| 80 | 0.94 |
| 85 | 0.82 |
| 90 | 0.70 |
| 95 | 0.79 |
| 100 | 0.66 |

Sensitivity decreases slightly at higher sound levels, indicating increasing nonlinearity.

---

# Operating Range

Estimated reliable operating range:

60 dB – 90 dB

- **Below 60 dB:** sensor readings fluctuate
- **Above 90 dB:** error increases significantly

---

# Key Findings

### Linear region
Best performance occurs between:

65 dB – 85 dB

### Low-level instability
Measurements become unreliable below **60 dB**.

### High-level overestimation
Above **90 dB**, the sensor consistently reports values higher than the true sound level.

### Calibration effectiveness
Using **70 dB → RMS = 1** provides a useful reference for mid-range measurements.

---

# Conclusion

The sound sensor provides reliable measurements between:

60 dB – 90 dB

Outside this range:

- Noise dominates low-level readings
- Nonlinearity increases at high sound levels

Future improvements could include:

- multi-point calibration
- signal filtering
- linearization of sensor response
