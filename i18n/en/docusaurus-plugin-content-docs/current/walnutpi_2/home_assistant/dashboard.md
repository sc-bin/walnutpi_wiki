---
sidebar_position: 5
---

# Dashboard

The Dashboard is the home page you see after logging into Home Assistant. It is used to display various information and can be customized by the user. By default, there are **Overview** and **Energy** pages. The most commonly used is the **Overview** page, which appears almost empty when you first log in.

![dashboard](./img/dashboard/dashboard1.png)

Now let's explain how to add new cards to the dashboard. Click the **pencil** button in the top right corner, then in the popup dialog, click the top-right button and select **Edit Dashboard**:

![dashboard](./img/dashboard/dashboard2.png)

A new window will pop up. If you want to start from a blank dashboard, check the option at the bottom left (don't worry about losing devices — you can add them back later), then click **Start with an empty dashboard**:

![dashboard](./img/dashboard/dashboard3.png)

The interface below will then appear. From now on, clicking the **pencil** button in the top right corner will always bring up this view. Click the **Add Card** button at the bottom right:

![dashboard](./img/dashboard/dashboard4.png)

Let's take adding a **Weather Forecast** card as an example to see how to add cards to the dashboard. You can see many card types. Scroll down to Weather Forecast, and you'll notice that the card only shows a description, meaning this card hasn't been linked to a service yet:

![dashboard](./img/dashboard/dashboard5.png)

Go back to the Overview page and first set your location using the map:

![dashboard](./img/dashboard/dashboard6.png)

Add an integration under Settings → Devices & Services:

![dashboard](./img/dashboard/dashboard7.png)

![dashboard](./img/dashboard/dashboard8.png)

In the popup window, search for the keyword "**meteoro**" and select the Meteorologisk institutt service (a weather service):

![dashboard](./img/dashboard/dashboard9.png)

Then set the name and latitude/longitude coordinates. If you already set the location using the map earlier, you don't need to enter it again. Click the **Submit** button to complete the configuration:

![dashboard](./img/dashboard/dashboard10.png)

![dashboard](./img/dashboard/dashboard11.png)

You can see that the service has been successfully added under Integrations:

![dashboard](./img/dashboard/dashboard12.png)

Now go back to the Overview home page, click the **pencil** button at the top right, then click **Add Card**, and find Weather Forecast. You will see that weather data is now available:

![dashboard](./img/dashboard/dashboard13.png)

Click to select it, then configure the relevant information in the popup window. For this demo, use the default settings and click Save.

![dashboard](./img/dashboard/dashboard14.png)

The weather forecast card now appears on the dashboard:

![dashboard](./img/dashboard/dashboard15.png)

When there are multiple cards on the dashboard, you can change their positions by editing the order number below:

![dashboard](./img/dashboard/dashboard16.png)
