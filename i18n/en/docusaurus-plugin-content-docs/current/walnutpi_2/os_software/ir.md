---
sidebar_position: 44
---

# IR Receiver

The Walnut Pi has 1 onboard infrared receiver.

![ir1](./img/ir/ir1.png)

The Walnut Pi system comes pre-installed with **ir-keytable** software, which can be used to view IR device information and test IR reception decoding.

## Viewing Device Information

Run the following command in the terminal to view IR device information:

```bash
ir-keytable
```
![ir2](./img/ir/ir2.png)

## IR Reception Test

First, you will need a commonly available remote control, such as the one shown below, which is easy to purchase.

![ir3](./img/ir/ir3.png)


Enter the following command in the terminal and wait for IR remote signals:

```bash
sudo ir-keytable -c -p NEC -t
```

![ir4](./img/ir/ir4.png)

Point the remote control at the IR receiver and press any button:

![ir5](./img/ir/ir5.png)

You will see the received IR code in the terminal:

![ir6](./img/ir/ir6.png)
