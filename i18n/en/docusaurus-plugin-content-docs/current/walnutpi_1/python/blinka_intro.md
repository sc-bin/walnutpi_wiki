---
sidebar_position: 2
---

# Introduction to Blinka (Python Library)

In the MCU world, we can use MicroPython or CircuitPython for Python embedded programming. For Linux boards, there is an open-source project initiated by Adafruit called **Blinka**, which aims to provide a universal Python library for GPIO-based embedded programming on Linux boards. Blinka currently supports Raspberry Pi, Jetson Nano, and many other Linux development boards on the market.

Open-source project: https://circuitpython.org/blinka

![blinka](./img/blinka_intro/blinka.png)

In short, after installing the Blinka library on the WalnutPi, you can easily use Python libraries to work with various GPIO peripherals on the development board. The WalnutPi comes with Blinka pre-installed in the factory system, located at **/usr/lib/walnutpi/Adafruit_Blinka**:


::::tip Note

The pre-installed Blinka on the WalnutPi has been customized and adapted to the WalnutPi's CPU.

::::
