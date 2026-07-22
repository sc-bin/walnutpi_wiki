---
sidebar_position: 20
---

# Shutdown and Reboot

The Walnut Pi runs an operating system, so unlike a typical microcontroller development board that simply shuts off when power is cut, it is recommended to use the **Log Out** function in the menu bar for shutdown or reboot in the pop-up dialog. This helps protect the circuit board and avoids sudden power loss, which could damage the operating system or cause data loss.

![log_out1](./img/log_out/log_out1.png)

**Shut Down** for shutdown, **Restart** for reboot.

![log_out2](./img/log_out/log_out2.png)

You can also shut down or reboot via commands:
- Shutdown
```bash
sudo poweroff
```

- Reboot
```bash
sudo reboot
```
