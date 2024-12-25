---
sidebar_position: 3
---

# MQTT通讯

## 前言
上一节，我们学习了Socket通信，当服务器和客户端建立起连接时，就可以相互通信了。在互联网应用大多使用WebSocket接口来传输数据。而在物联网应用中，常常出现这样的情况：海量的传感器，需要时刻保持在线，传输数据量非常低，有着大量用户使用。如果仍然使用socket作为通信，那么服务器的压力和通讯框架的设计随着数量的上升将变得异常复杂！

那么有无一个框架协议来解决这个问题呢，答案是有的。那就是MQTT(消息队列遥测传输)。


## 实验目的
通过编程让核桃派实现MQTT协议信息的发布和订阅（接收）。

## 实验讲解
MQTT是IBM于1999年提出的，和HTTP一样属于应用层，它工作在 TCP/IP协议族上，通常还会调用socket接口。是一个基于客户端-服务器的消息发布/订阅传输协议。其特点是协议是轻量、简单、开放和易于实现的，这些特点使它适用范围非常广泛。在很多情况下，包括受限的环境中，如：机器与机器（M2M）通信和物联网（IoT）。其在，通过卫星链路通信传感器、偶尔拨号的医疗设备、智能家居、及一些小型化设备中已广泛使用。
总结下来MQTT有如下特性/优势：
- 异步消息协议
- 面向长连接
- 双向数据传输
- 协议轻量级
- 被动数据获取


![mqtt1](./img/mqtt/mqtt1.jpg)

从上图可以看到，MQTT通信的角色有两个，分别是服务器和客户端。服务器只负责中转数据，不做存储；客户端可以是信息发送者或订阅者，也可以同时是两者。具体如下图：

![mqtt2](./img/mqtt/mqtt2.png)

确定了角色后是如何传输数据呢？下表示MQTT最基本的数据帧格式，例如温度传感器发布主题“Temperature”编号,消息是“25”（表示温度）。那么所有订阅了这个主题编号的客户端（手机应用）就会收到相关信息，从而实现通信。如下表所示：

![mqtt3](./img/mqtt/mqtt3.png)

由于特殊的发布/订阅机制，服务器不需要存储数据（当然也可以在服务器的设备上建立一个客户端来订阅保存信息），因此非常适合海量设备的传输。

人生苦短，而python已经封装好了MQTT客户端的库文件。让我们的应用变得简单美妙。使用的是paho.mqtt python库，该库由eclipse公司维护，拥有众多开发者用户。可以使用pip来安装，在终端运行下面指令即可安装：

```bash
sudo pip3 install paho-mqtt
```

![mqtt4](./img/mqtt/mqtt4.png)

## paho-mqtt对象

### 构造函数
```python
import paho.mqtt.client as mqtt
client = mqtt.Client()
```
导入MQTT库和构建client客户端对象。

### 使用方法
```python
client.connect(host,port,keepalive)
```
连接到MQTT服务器。
- `host` : 服务器地址；
- `port` : 端口，通常是1883；
- `keepalive` : 保活，默认60秒。

<br></br>

```python
client.publish(topic,message)
```
发布信息。
- `topic` : 主题名称；
- `message` : 信息内容，例：'Hello WalnutPi!'

<br></br>

```python
client.subscribe(topic)
```
订阅;
- `topic` : 主题名称。

<br></br>

```python
client.on_connect = on_connect
```
使用回调函数方式连接。用法看订阅者示例代码。

<br></br>

```python
client.on_message = on_message
```
接收信息的回调函数。用法看订阅者示例代码。

<br></br>

更多使用方法，请看官方文档: https://github.com/eclipse/paho.mqtt.python#eclipse-paho-mqtt-python-client

由于客户端分为发布者和订阅者角色，因此为了方便大家更好理解，本实验分开两个案例来编程，分别为发布者(publish)和订阅者(subscribe)。再结合MQTT网络调试助手来测试。代表编写流程图如下：

**发布者(publish)代码流程：**

```mermaid
graph TD
    导入相关模块-->初始化相关模块-->建立mqtt连接-->判断是否连接成功--是-->循环发布数据;
    判断是否连接成功--否-->结束;
```
<br></br>

**订阅者(subscribe)代码流程：**

```mermaid
graph TD
    导入相关模块-->初始化相关模块-->建立mqtt连接-->判断是否连接成功--是-->循环处理接收到的数据;
    判断是否连接成功--否-->结束;
```

## 参考代码

### 发布者 publish

```python
'''
实验名称：MQTT通信
实验平台：核桃派1B
说明：编程实现MQTT通信:发布者（publish）。
'''

#导入相关库
import paho.mqtt.client as mqtt
import time

#服务器和主题信息
host = 'mq.tongxinmao.com'
port = 18830
topic = '/public/walnutpi/1'

#构建mqtt客户端对象
client = mqtt.Client()

#发起连接
client.connect(host,port)

while True:
    
    #发布信息
    client.publish(topic,'Hello WalnutPi!')
    
    time.sleep(1) #延时1秒，发送间隔
```

### 订阅者 subscribe

```python
'''
实验名称：MQTT通信
实验平台：核桃派1B
说明：编程实现MQTT通信: 订阅者（subscribe）。
'''

#导入相关库
import paho.mqtt.client as mqtt
import time

#服务器和主题信息
host = 'mq.tongxinmao.com'
port = 18830
topic = '/public/walnutpi/1'

#客户端从服务器接收到1个CONNACK响应时执行的回调函数.
def on_connect(client, userdata, flags, rc):
    print("Connected with result code "+str(rc))
    # 在on_connect()中使使用订阅主题意味着如果我们失去连接并重新连接，订阅将被更新。
    client.subscribe(topic)

# 当从服务器中收到其他设备的发布信息时，执行这个回调函数.
def on_message(client, userdata, msg):
    print(msg.topic+" "+str(msg.payload))

#构建MQTT客户端
client = mqtt.Client()

#配置连接和接收信息的回调函数
client.on_connect = on_connect
client.on_message = on_message

#连接服务器
client.connect(host, port)

# 处理网络流量、分派回调和处理重新连接的阻塞调用。
client.loop_forever()
```

## 实验结果

### 发布者测试

电脑打开通讯猫MQTT助手，保证电脑是连接到互联网的：

![mqtt5](./img/mqtt/mqtt5.png)

接下来是配置MQTT助手，按下图配置。

1、点击网络；

2、点击MQTT;

3、点击启动；

4、输入订阅主题，这里填发送者的主题 “/public/walnutpi/1”;

5、点击订阅主题按钮，等待接收信息；

6、订阅成功后左边提示订阅成功。

![mqtt6](./img/mqtt/mqtt6.png)

使用Thonny远程核桃派运行以上发布者代码，关于核桃派运行python代码方法请参考： [运行Python代码](../python_run)

![mqtt7](./img/mqtt/mqtt7.png)


运行后可以看到MQTT网络助手接收到核桃派发来的信息：

![mqtt8](./img/mqtt/mqtt8.png)


### 订阅者测试


订阅者”代码测试方法跟“发布者”相反。在MQTT助手中发布主题修改为：'/public/01Studio/2'。

![mqtt9](./img/mqtt/mqtt9.png)

运行订阅者代码：

![mqtt10](./img/mqtt/mqtt10.png)

可以看到thonny下方终端打印接收到的数据（实际是核桃派开发板接收到的数据）。

![mqtt11](./img/mqtt/mqtt11.png)

当然你也可以在同一个MQTT在线助手下测试发布和订阅功能来做一些测试，只需要将主题设置一致即可，如下图所示：

![mqtt12](./img/mqtt/mqtt12.png)

通过本节我们了解了MQTT通信原理以及成功实现通信。这个实验的MQTT是连接到通讯猫服务器的，所以是支持远程数据传输的。也就是你可以在家使用核桃派A订阅公司或者学校实验室里面的核桃派B，实现一些传感器等数据传输。目前市面上大部分物联网云平台支持MQTT，原理大同小异。大家可以基于不同平台协议来开发，实现自己的物联网设备远程连接。