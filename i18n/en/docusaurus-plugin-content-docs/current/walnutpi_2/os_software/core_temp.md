---
sidebar_position: 21
---

# Temperature Information

The Walnut Pi 2B's T527 chip has 6 temperature sensors:

- `sensor0`: CPUL (Little Core) temperature
- `sensor1`: CPUB (Big Core) temperature
- `sensor2`: GPU temperature
- `sensor3`: NPU temperature
- `sensor4`: DDR temperature
- `sensor5`: PMIC temperature

::::tip Note
Temperature values retrieved by the commands below need to be divided by 1000.
::::

## CPU Temperature

### CPUL

Check sensor type command:

```bash
cat /sys/class/thermal/thermal_zone0/type
```

Check temperature command:
```bash
cat /sys/class/thermal/thermal_zone0/temp
```

![core_temp1](./img/core_temp/cpul.png)

### CPUB

Check sensor type command:

```bash
cat /sys/class/thermal/thermal_zone1/type
```

Check temperature command:
```bash
cat /sys/class/thermal/thermal_zone1/temp
```

![core_temp1](./img/core_temp/cpub.png)

## GPU Temperature

Check sensor type command:

```bash
cat /sys/class/thermal/thermal_zone2/type
```

Check temperature command:
```bash
cat /sys/class/thermal/thermal_zone2/temp
```

![core_temp2](./img/core_temp/gpu.png)

## NPU Temperature

Check sensor type command:

```bash
cat /sys/class/thermal/thermal_zone3/type
```

Check temperature command:
```bash
cat /sys/class/thermal/thermal_zone3/temp
```

![core_temp3](./img/core_temp/npu.png)

## DDR Temperature

Check sensor type command:

```bash
cat /sys/class/thermal/thermal_zone4/type
```

Check temperature command:
```bash
cat /sys/class/thermal/thermal_zone4/temp
```

![core_temp4](./img/core_temp/ddr.png)

## PMIC Temperature

Check sensor type command:

```bash
cat /sys/class/thermal/thermal_zone5/type
```

Check temperature command:
```bash
cat /sys/class/thermal/thermal_zone5/temp
```

![core_temp4](./img/core_temp/pmc.png)
