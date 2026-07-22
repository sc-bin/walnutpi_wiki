---
sidebar_position: 7
---

# IP Address

## WiFi IP Address

WiFi module hardware location—connects wirelessly to the router (supports 2.4G and 5G signals):

![ip_get1](./img/ip_get/ip_get1.png)

Use the following command to retrieve all network IP addresses of the Walnut Pi. **wlan0** is the WiFi wireless adapter name; once connected, its IP address will be displayed.
```bash
sudo ifconfig
```

![ip_get2](./img/ip_get/ip_get2.png)

## Ethernet IP Address

Ethernet module hardware location—connects to the router via Ethernet cable:

![ip_get3](./img/ip_get/ip_get3.png)

Use the following command to retrieve all network IP addresses of the Walnut Pi. **eth0** is the Ethernet adapter name; once connected, its IP address will be displayed.
```bash
sudo ifconfig
```

![ip_get4](./img/ip_get/ip_get4.png)
