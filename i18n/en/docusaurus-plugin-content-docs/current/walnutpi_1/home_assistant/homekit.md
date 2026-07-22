---
sidebar_position: 10
---

# Connecting to Apple HomeKit

Apple HomeKit is the built-in smart home app on iPhones. Simply add the HomeKit Bridge integration in WalnutPi Home Assistant to bind specific devices and control them on your iPhone.

This section takes an LED light as an example, adding the registered LED entity to HomeKit. Ensure you have already added the LED entity. Refer to the tutorial: [LED](../home_assistant/mqtt/device_entity/led.md) section.

First, add the HomeKit Bridge integration to bridge HomeKit and Home Assistant devices.

![homekit](./img/homekit/homekit1.png)

![homekit](./img/homekit/homekit2.png)

Search for the keyword "homekit" and click the Apple entry that appears:

![homekit](./img/homekit/homekit3.png)


Click `HomeKit Bridge`:

![homekit](./img/homekit/homekit4.png)

Here, select the domains to include. These are actually Home Assistant component categories. Since the LED used here belongs to the light category, just make sure light is checked.

![homekit](./img/homekit/homekit5.png)

Click Finish:

![homekit](./img/homekit/homekit6.png)

At this point, a new notification will appear in the left notification bar:

![homekit](./img/homekit/homekit7.png)

A QR code will appear.

![homekit](./img/homekit/homekit8.png)

Open the built-in "Home" app on your iPhone:

![homekit](./img/homekit/homekit9.png)

Select Scan Accessory:

![homekit](./img/homekit/homekit10.png)

Scan the QR code that appeared in Home Assistant:

![homekit](./img/homekit/homekit11.png)

![homekit](./img/homekit/homekit11_2.png)

Then follow the prompts to add. After successful addition, you will see the LED device entity appear in the Apple app.

![homekit](./img/homekit/homekit12.png)

You can now control the WalnutPi's LED through the Apple Home app.

![homekit](./img/homekit/homekit13.png)

![homekit](./img/homekit/homekit14.png)



