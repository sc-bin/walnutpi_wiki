---
sidebar_position: 10
---

# Integrating with Apple HomeKit

Apple HomeKit is the built-in smart home app on iPhones. By adding the HomeKit Bridge integration to your WalnutPi Home Assistant, you can bind specific devices and control them from your iPhone.

This section uses an LED as an example, adding a registered LED entity into HomeKit. Make sure the LED entity is already added — see the [LED](../home_assistant/mqtt/device_entity/led.md) tutorial.

First, add the HomeKit Bridge integration to bridge HomeKit and Home Assistant devices.

![homekit](./img/homekit/homekit1.png)

![homekit](./img/homekit/homekit2.png)

Search for the keyword "homekit" and click the Apple entry that appears:

![homekit](./img/homekit/homekit3.png)

Click **HomeKit Bridge**:

![homekit](./img/homekit/homekit4.png)

Here you can select the domains to include, which correspond to Home Assistant component categories. Since the LED used here belongs to the Light domain, make sure Light is checked.

![homekit](./img/homekit/homekit5.png)

Click Finish:

![homekit](./img/homekit/homekit6.png)

At this point, a new notification will appear in the left notification panel:

![homekit](./img/homekit/homekit7.png)

A QR code will appear.

![homekit](./img/homekit/homekit8.png)

Open the built-in "Home" app on your iPhone:

![homekit](./img/homekit/homekit9.png)

Select Scan Accessory:

![homekit](./img/homekit/homekit10.png)

Scan the QR code displayed by Home Assistant:

![homekit](./img/homekit/homekit11.png)

![homekit](./img/homekit/homekit11_2.png)

Then follow the prompts to add it. After successfully adding, you will see the LED device entity appear in the Apple Home app.

![homekit](./img/homekit/homekit12.png)

You can now control the WalnutPi LED via the Apple Home app.

![homekit](./img/homekit/homekit13.png)

![homekit](./img/homekit/homekit14.png)
