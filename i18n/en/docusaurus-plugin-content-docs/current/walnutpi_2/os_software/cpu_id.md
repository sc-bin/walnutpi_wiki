---
sidebar_position: 42
---

# Chip ID

The Walnut Pi 2B is powered by the Allwinner T527 chipset, and each chip has a unique chip ID. Users can retrieve the chip ID using the following command to distinguish between different development boards:

```bash
cat /sys/class/sunxi_info/sys_info |grep sunxi_serial
```

![cpu_id](./img/cpu_id/cpu_id1.png)
