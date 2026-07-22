---
sidebar_position: 10
---

# Device Map

::::tip Note
This feature is only available in WalnutPi Gen 1 images V2.5.0 and above.
::::

The WalnutPi Device Map is a unique feature of the WalnutPi system. It obtains the board's location via IP address and displays it on a map, with location accuracy to the city level. [Device Map Link](https://map.walnutpi.com)

![map_device](./img/map_device/map_device1.png)

This feature is enabled by default. Users can disable it manually:

**Disable command:**

```bash
systemctl disable map_device.service
```

Restart the board for the change to take effect.

**Enable command:**

```bash
systemctl enable map_device.service
```

Restart the board for the change to take effect.
