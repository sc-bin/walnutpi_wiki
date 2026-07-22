---
sidebar_position: 1
---

# Running Python Code

This section explains how to do Python programming and run Python code on the WalnutPi. If you have never learned Python, you can first visit the following website to learn the basics:
- Python Basics Tutorial: [https://www.runoob.com/python/python-tutorial.html](https://www.runoob.com/python/python-tutorial.html)

## Running Python in Terminal

Let's first look at how to write and run Python code using the most basic method — the WalnutPi terminal. This method also works for headless (no desktop) systems.

Open the WalnutPi terminal and use the nano editor to create a new Python file:
```bash
nano hello_walnutpi.py
```
![terminal1](./img/python_run/terminal1.png)

Enter the editing interface and type the simplest Python code:
```python
print('hello walnutpi!')
```
![terminal2](./img/python_run/terminal2.png)

Press **Ctrl+X** to exit, and you will be prompted whether to save.

![terminal3](./img/python_run/terminal3.png)

Press **Y** to choose a filename to save. Keep the default and press Enter to confirm.

![terminal4](./img/python_run/terminal4.png)

Use the **ls** command to see that the **hello_walnutpi.py** file has been added to the current directory.

![terminal5](./img/python_run/terminal5.png)

You can directly run a Python file using the `python` command. You can see the code runs successfully and prints "hello walnutpi!"

```bash
python hello_walnutpi
```
![terminal6](./img/python_run/terminal6.png)

You can also type `python` directly in the terminal to see the current Python version and enter Python interactive mode.

![terminal7](./img/python_run/terminal7.png)

Press **Ctrl+Z** or **Ctrl+C** to exit.

![terminal8](./img/python_run/terminal8.png)

## Thonny IDE

If you are using the WalnutPi desktop version OS, you can directly use the built-in Thonny IDE for programming, which is very convenient. You need to connect the WalnutPi to a monitor via HDMI and connect a keyboard and mouse.

Open **Menu → Development → Thonny**

On first run, you will be prompted to select a language. Click "Let's go!" to enter:

![thonny1](./img/python_run/thonny1.png)

Once inside, bring up the file directory for easier viewing. Click **View → Files**:

![thonny10](./img/python_run/thonny10.png)

You can see a file directory of the current system added to the left side of the IDE:

![thonny11](./img/python_run/thonny11.png)

Next, create a new file:

![thonny2](./img/python_run/thonny2.png)

Type in the editing area:
```python
print('hello walnutpi!')
```
Then save.

![thonny3](./img/python_run/thonny3.png)

Click the green "Run" button, and the Python code will be executed directly:

![thonny12](./img/python_run/thonny12.png)

Of course, you can also interact with Python directly in the Python terminal at the bottom of Thonny:

![thonny13](./img/python_run/thonny13.png)

You can enable **Tab key autocompletion in the editor** via the Thonny menu bar **Tools → Options** for easier development.

![thonny14](./img/python_run/thonny14.png)

Below, after typing **led.**, press the Tab key to autocomplete:

![thonny15](./img/python_run/thonny15.png)

## Thonny Remote Connection (Windows-based)

Above, we used Thonny IDE on the WalnutPi system. Similarly, we can use Thonny IDE on Windows to remotely connect to the WalnutPi for Python programming. The WalnutPi system comes pre-installed with an SSH server, allowing remote control via SSH. This method is suitable for remote development using your own computer.

::::tip Note

This method is recommended for users who only do Python programming and are accustomed to using a PC. It is also the primary method used in this tutorial chapter.

::::

Thonny IDE Windows version download link: https://thonny.org/

After downloading and installing, open Thonny. First, click **View → Files** to bring up the file directory.

![win_thonny1](./img/python_run/win_thonny1.png)
![win_thonny2](./img/python_run/win_thonny2.png)

Next, connect to the WalnutPi via SSH. Click **Run → Configure Interpreter**:

![win_thonny3](./img/python_run/win_thonny3.png)

In the popup configuration interface, configure as shown below:
1. Select **Remote Python 3 (SSH)**
2. WalnutPi IP address
3. WalnutPi username, enter **pi**
4. Use the default password authentication
5. Enter **Python3** here (note the capitalization). This is because WalnutPi's `python3` (lowercase) has some file permission issues, while `Python3` (uppercase first letter) has been pre-configured with the correct permissions.

![win_thonny4](./img/python_run/win_thonny4.png)

After configuration, click **Run → Stop/Restart Backend** to initiate the connection:

![win_thonny5](./img/python_run/win_thonny5.png)

Enter the password **pi**:

![win_thonny6](./img/python_run/win_thonny6.png)

Wait until the WalnutPi file system directory appears at the bottom left of Thonny, indicating a successful connection:

![win_thonny7](./img/python_run/win_thonny7.png)

You can use Python commands directly in the Python terminal (equivalent to operating on the WalnutPi board):

![win_thonny7_1](./img/python_run/win_thonny7_1.png)

You can then open a local Windows `.py` file or a WalnutPi `.py` file, write the code, and click the **Run** button to execute the Python code.

![win_thonny8](./img/python_run/win_thonny8.png)

You can distinguish local vs. remote files by the title bar above the code area:

- [ hello.py ] with "**[ ]**" indicates a WalnutPi board file (remote file);

- hello2.py without "**[ ]**" indicates a Windows file (local file).

![win_thonny9](./img/python_run/win_thonny9.png)

You can upload/download files by **right-clicking** in the left file directory to transfer between WalnutPi and Windows.

![win_thonny10](./img/python_run/win_thonny10.png)
![win_thonny11](./img/python_run/win_thonny11.png)

You can enable **Tab key autocompletion in the editor** via the Thonny menu bar **Tools → Options** for easier development. **The autocompletion content is from the device connected to the interpreter — in the case of remote connection, it will autocomplete from the WalnutPi's Python libraries.**

![thonny14](./img/python_run/thonny14.png)

Below, after typing **led.**, press the Tab key to autocomplete:

![thonny15](./img/python_run/thonny15.png)


## VSCode Remote Connection (Windows-based)

Thonny, used above, is mainly for Python programming. Some users may prefer VS Code, so here's how to set up remote development with VS Code. The advantage of VS Code is its convenience for multi-language programming.

::::danger Warning

The VS Code remote method consumes a considerable amount of the WalnutPi's memory. It is not recommended to run other memory-intensive applications on the WalnutPi when using this method.

::::

First, install VS Code. Download: https://code.visualstudio.com/download

After installation, search for the **ssh** extension in the VS Code extensions panel and install it:

![vscode1](./img/python_run/vscode1.png)

After the extension is installed, open it on the left and click the **+** button on the right to create a new remote connection:

![vscode2](./img/python_run/vscode2.png)

In the popup box, enter: **pi@192.168.2.180**. `pi` is the default WalnutPi username, and the part after `@` is the IP address. You can use "sudo ifconfig" to find the WalnutPi's IP address.

![vscode3](./img/python_run/vscode3.png)

Next, choose where to save the information. The default first option is fine:

![vscode4](./img/python_run/vscode4.png)

Then click the "Connect" button at the bottom right:

![vscode5](./img/python_run/vscode5.png)

Next, select "Linux" from the top:

![vscode6](./img/python_run/vscode6.png)

Select "Continue":

![vscode7](./img/python_run/vscode7.png)

Enter the WalnutPi `pi` user password: **pi**

![vscode8](./img/python_run/vscode8.png)

Wait for the connection until the WalnutPi IP address appears at the bottom left:

![vscode9](./img/python_run/vscode9.png)

Click position 1 in the image below to view files, then click position 2 to open a folder. At position 3, you can enter your desired path — the default /home/pi is fine. Click OK.

![vscode10](./img/python_run/vscode10.png)

Check the trust option:

![vscode11](./img/python_run/vscode11.png)

After opening, you can see the WalnutPi directory on the left. You can download files from the WalnutPi board or upload files. The right side is the document editing area.

![vscode12](./img/python_run/vscode12.png)

You can create a new WalnutPi terminal for easy command operations:

![vscode13](./img/python_run/vscode13.png)

You can see the familiar terminal appear at the bottom.
![vscode14](./img/python_run/vscode14.png)


The VS Code remote terminal works just like the WalnutPi local terminal. Edit your Python code, then use the **python xx.py** command to run the Python program.

![vscode15](./img/python_run/vscode15.png)

Logged-in IPs and accounts are saved, so next time you can simply open them in the remote manager:

![vscode16](./img/python_run/vscode16.png)

## Troubleshooting: Cannot Connect via SSH

One common scenario: if you have previously used Thonny or VSCode to remotely connect to a WalnutPi, and then the WalnutPi has been re-imaged or its SD card replaced, you need to delete the SSH key information on your computer to reconnect.

For Windows users, this file is located at **C:\Users\[username]\.ssh\known_hosts**

Open the file, find the current WalnutPi IP, and delete the IP and its key information.

![ssh_error1](./img/python_run/ssh_error1.png)

![ssh_error2](./img/python_run/ssh_error2.png)
