---
sidebar_position: 7
---

# Obtaining IP Address

## WiFi IP Address

WiFi module hardware location. Connect wirelessly to a router via WiFi (supports 2.4G and 5G signals):

![ip_get1](./img/ip_get/ip_get1.png)

Use the following command to get all network IP addresses of the WalnutPi. **wlan0** is the WiFi card name. Once connected, you can see its IP address.

```bash
sudo ifconfig
```

![ip_get2](./img/ip_get/ip_get2.png)

## Ethernet IP Address

Ethernet module hardware location. Connect to a router via an Ethernet cable:

![ip_get3](./img/ip_get/ip_get3.png)

Use the following command to get all network IP addresses of the WalnutPi. **eth0** is the Ethernet card name. Once connected, you can see its IP address.

```bash
sudo ifconfig
```

![ip_get4](./img/ip_get/ip_get4.png)
