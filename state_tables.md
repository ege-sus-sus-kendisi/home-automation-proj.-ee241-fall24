# State Tables for Verilog Modules

## 1. Lighting Module State Table

| **Inputs**                         | **Outputs**                             | **Conditions**                     |
|-------------------------------------|------------------------------------------|-------------------------------------|
| `reset = 1`                         | `light_on = 0`, `light_brightness = 0`, `light_color = 24'h000000` | Reset condition.                   |
| `presence_detected = 1`, `hour < OFF_HOUR` | `light_on = 1`, `light_brightness = brightness`, `light_color = color` | Presence detected and time valid.  |
| `presence_detected = 0` or `hour >= OFF_HOUR` | `light_on = 0`, `light_brightness = 0`, `light_color = 24'h000000` | No presence or invalid time.       |

---

## 2. Heating Module State Table

| **Inputs**                           | **Outputs**                | **Conditions**                   |
|---------------------------------------|-----------------------------|-----------------------------------|
| `reset = 1`                           | `heater_on = 0`, `ventilator_on = 0` | Reset condition.                 |
| `internal_temp < external_temp`       | `heater_on = 1`             | Heating required.                |
| `internal_temp >= external_temp`      | `heater_on = 0`             | No heating required.             |
| `air_quality < 50`                    | `ventilator_on = 1`         | Ventilation required.            |
| `air_quality >= 50`                   | `ventilator_on = 0`         | No ventilation required.         |

---

## 3. Security Module State Table

| **Inputs**                                                 | **Outputs**                  | **Conditions**                   |
|-------------------------------------------------------------|-------------------------------|-----------------------------------|
| `reset = 1`                                                 | `door_locked = 1`, `alarm_on = 0` | Reset condition.                 |
| `remote_lock = 1` or `biometric_fingerprint = 0` or `biometric_face = 0` | `door_locked = 1`            | Lock due to remote or failed biometrics. |
| `presence_detected = 0`                                     | `door_locked = 1`, `alarm_on = 1` | No presence, alarm triggered.   |
| `presence_detected = 1` and valid biometrics                | `door_locked = 0`, `alarm_on = 0` | Presence and valid biometrics.  |

---

## 4. Appliance Control Module State Table

| **Inputs**                         | **Outputs**                     | **Conditions**                     |
|-------------------------------------|----------------------------------|-------------------------------------|
| `reset = 1`                         | `appliance_on = 0`, `blinds_open = 0`, `valve_closed = 1` | Reset condition.                   |
| `remote_control = 1` or `presence_detected = 1` | `appliance_on = 1`           | Appliance controlled remotely or presence detected. |
| `hour >= OFF_HOUR`                  | `blinds_open = 0`               | Close blinds at or after off-hour. |
| `hour < OFF_HOUR`                   | `blinds_open = 1`               | Open blinds before off-hour.       |
| `presence_detected = 0`             | `valve_closed = 1`              | Close valve if no presence.        |
| `presence_detected = 1`             | `valve_closed = 0`              | Open valve if presence detected.   |

---

## 5. Garden and Pets Module State Table

| **Inputs**                                  | **Outputs**                     | **Conditions**                    |
|---------------------------------------------|----------------------------------|------------------------------------|
| `reset = 1`                                  | `irrigation_on = 0`, `feeder_on = 0`, `pet_door_open = 0` | Reset condition.                  |
| `soil_moisture < 50` and `weather_condition < 20` | `irrigation_on = 1`           | Start irrigation due to dry soil and bad weather. |
| `soil_moisture >= 50` or `weather_condition >= 20` | `irrigation_on = 0`          | Stop irrigation.                  |
| `pet_detected = 1`                          | `feeder_on = 0`, `pet_door_open = 1` | Pet detected.                     |
| `pet_detected = 0`                          | `feeder_on = 1`, `pet_door_open = 0` | No pet detected.                  |
