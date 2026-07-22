---
sidebar_position: 1
---

# Compiling C Code on the Development Board

## Command Line Method

First, create a test.c file in the current directory on WalnutPi and enter the following content (this code prints "Hello WalnutPi" to the terminal):

```c
#include <stdio.h>

int main (void)
{
  printf ("Hello WalnutPi\n") ;

  return 0 ;
}
```

To compile the code, use the `gcc` command, which is very simple. For example, to compile test.c into an executable named test, just run:

```bash
gcc test.c -o test
```

Run the compiled program:

```bash
./test
```

You will see "Hello WalnutPi" printed in the terminal:

![c1](./img/c_run/gcc_compile.png)

## Geany IDE (Local on WalnutPi)

The WalnutPi desktop system comes pre-installed with Geany IDE, located in the **Start--Development** menu. You can use Geany for C programming, compiling, and running.

Open Geany:

![c2](./img/c_run/c2.png)

Create a new file, enter the following test code, and save it as a .c file.

```c
#include <stdio.h>

int main (void)
{
  printf ("Hello WalnutPi\n") ;

  return 0 ;
}
```

![c3](./img/c_run/c3.png)

Click the **Build** button, and you will see the compilation result below. If the compilation is successful, an executable file will be generated in the current directory.

![c6](./img/c_run/c6.png)

Click the **Execute** button to run the compiled executable. A new terminal will pop up, displaying "Hello WalnutPi".

![c7](./img/c_run/geany_run.png)
