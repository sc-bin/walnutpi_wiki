---
sidebar_position: 8
---

# SSH Remote Terminal

Users familiar with command-line operations can perform LAN-based SSH remote terminal control on a networked Walnut Pi, allowing convenient remote command operations on the Walnut Pi from your PC.

- `Normal User (Default)` Username: pi ; Password: pi
- `Root Account` Username: root ; Password: root

Before this, you need to connect the Walnut Pi to the router via an **Ethernet cable** or by following the [WiFi Connection](../os_software/wifi) section. Ensure the Walnut Pi and your computer are on the same subnet (i.e., connected to the same router).

First, obtain the Walnut Pi's current IP address via an HDMI display or serial connection using the following command:
```bash
sudo ifconfig
```
eth0 indicates the Ethernet interface, and wlan0 indicates the WiFi connection. When connected, the IP address will be displayed below.

![ssh1](./img/ssh/ssh1.png)

We'll use PuTTY for demonstration (you can use any other SSH-capable software):

![ssh2](./img/ssh/ssh2.png)

Select SSH, then enter the Walnut Pi's IP address. The default port is 22.

![ssh3](./img/ssh/ssh3.png)

When the trust prompt appears, simply select Yes.

![ssh4](./img/ssh/ssh4.png)

You will then see a login prompt. Enter "pi" for both username and password. Upon successful login, the Walnut Pi terminal information will appear.

![ssh5](./img/ssh/ssh5.png)
