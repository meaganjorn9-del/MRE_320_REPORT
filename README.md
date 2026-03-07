# DHT-11 Sensor Characteristics

## Overview
This project evaluates the performance characteristics of a DHT-11 temperature and humidity sensor by comparing the results to the readings of a thermometer and a hygrometer.

The objectives were to determine:

-Hysteresis of the sensor

-Drift

-Resolution of the sensor


---

# Experimental Setup

### Reference Conditions

Normal room temperature and humidity:

20.9 degrees Celsius

39.2% humidity


---

### Hysteresis Testing

# Temperature/Humidity 1 vs Temperature/Humidity 2

| Temperature/Humidity 1 (*C/%) | Temperature/Humidity 2 |
|-------------------------------|-----------------------|
| 21.1/40% | 21.6/39% |
| 21.1/40% | 21.5/39% |
| 21.1/40% | 21.6/39% |
| 21.1/40% | 21.6/39% |
| 21.1/40% | 21.6/39% |
| 21.1/40% | 21.5/39% |
| 21.1/40% | 21.5/39% |
| 21.1/40% | 21.5/39% |
| 21.1/40% | 21.6/39% |
| 21.1/40% | 21.5/39% |

# Observations

When measuring the object, specifically a calculator, it measured 21.1 degrees in one direction and about 21.5 degrees in the other direction.
The actual temperature of it on a thermometer was 20.94 degrees Celsius. 

The humidity was 40% in one direction and 39% in the other direction. 

---

### Drift Testing

The sensor was left to measure temperature and humidity for 10 minutes.

| Time (min) | Temperature (C) | Humidity (%) |
|------------|-----------------|-------------|
| 0 | 21.5 | 40 |
| 1 | 21.4 | 40 |
| 2 | 21.5 | 40 |
| 3 | 21.4 | 40 |
| 4 | 21.4 | 40 |
| 5 | 21.4 | 40 |
| 6 | 21.4 | 40 |
| 7 | 21.4 | 40 |
| 8 | 21.4 | 40 |
| 9 | 21.4 | 40 |
| 10 | 21.4 | 40 |

# Observations

The temperature wavered slightly between 21.4 and 21.5, at least early.
The humidity remained 40% throughout the period of time.

---

### Resolution Testing

Resolution was found using fingers as an input and measured the smallest incremental change.

| Temperature (C) | Humidity (%) |
|-----------------|-------------|
| 21.2 | 41 |
| 21.2 | 41 |
| 21.2 | 41 |
| 21.2 | 41 |
| 21.2 | 48 |
| 21.3 | 52 |
| 21.3 | 51 |
| 21.4 | 49 |
| 21.4 | 48 |
| 21.4 | 47 |
| 21.5 | 46 |
| 21.5 | 45 |
| 21.4 | 44 |
| 21.5 | 43 |
| 21.5 | 43 |
| 21.5 | 43 |
| 21.5 | 42 |
| 21.6 | 42 |
| 21.6 | 42 |
| 21.6 | 42 |

# Observations

The temperatures changes in 0.1-degree increments while the humidity changes in 1% increments. It takes a few moments for the sensor to read any changes.

---

### Key findings

# Hysteresis Test

The difference between the first group of temperatures and the actual temperature was 0.2 degrees. The difference between the 2nd group of temperatures and the actual temperature was about 0.7 degrees.

The difference in humidity for the first test was 0.8%. In the 2nd test, the difference was 0.2%. This test came out positive without major differences.

# Drift

The biggest difference in wavering temperature was 0.1 degrees. There was no difference in humidity which is very ideal.

# Resolution

The incremental change in temperature and humidity is not very good as the readings often repeat themselves too often. A more precise reading would be in 0.01-degree increments or 0.1% increments.

---

### Conclusion

The sensor is good for general use, but it is not ideal for very precise readings

Advantages:

- Measures parameters without large gaps in data
- Does not waver in its measurements
- Low cost

Disadvantages:
- Not ideal for super precise measurements
- There is a delay in its response time


