---
sidebar_position: 1
---

# NPU Introduction

NPU (Neural Processing Unit) is a hardware acceleration chip specifically designed for neural network computing in the field of artificial intelligence, serving as the core computing engine of the AI era. Compared to traditional CPUs (Central Processing Units) and GPUs (Graphics Processing Units), NPUs deeply optimize their architecture by integrating a large number of dedicated units for neural network operations, such as multiply-accumulator arrays and systolic arrays, enabling efficient execution of complex operations like matrix operations and activation function calculations. This gives them astonishing speed and energy efficiency advantages when processing deep learning tasks, significantly reducing computational latency and power consumption, and enabling real-time inference and training in scenarios such as image recognition, speech processing, and natural language processing. From smart terminals to data centers, from edge computing to cloud services, NPUs, with their powerful parallel processing capabilities and excellent energy efficiency ratios, drive the rapid deployment of AI technologies and become a key force in driving intelligent transformation across industries.

For the differences between CPU, GPU, and NPU, you can watch this Bilibili video: https://www.bilibili.com/video/BV1wbcdeWENh/

![intro](./img/intro/intro1.png)

WalnutPi 2B (Allwinner T527) features a built-in 2 TOPS NPU, supporting INT 8/16/32b and Float 16/32b. WalnutPi OS (Debian) has already ported the relevant drivers.

