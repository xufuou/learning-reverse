## Source code
```c
/* stack3-stdin.c                               *
 * specially crafted to feed your brain by gera */

#include <stdio.h>

int main() {
	int cookie;
	char buf[80];

	printf("buf: %08x cookie: %08x\n", &buf, &cookie);
	gets(buf);

	if (cookie == 0x01020005)
  		printf("you win!\n");
}
```

## Setup
Check if ASLR is disabled
```bash
sysctl kernel.randomize_va_space
kernel.randomize_va_space = 0
```

Check gcc version
```bash 
gcc -v 
gcc version 7.2.0 (Debian 7.2.0-8)
```

Compile the code with gcc without protections for 32-bits
```bash
gcc -m32 -z execstack -fno-stack-protector -o stack3 stack3.c
```

If you fall into a similar error ```/usr/include/features.h:364:25: fatal error: sys/cdefs.h: No such file or directory``` run
```bash
sudo apt-get install g++-multilib
```

## Exploitation

The resolution for this exercise is exactly the same than the [stack2](https://github.com/xufuou/learning-reverse/tree/master/InsecureProgramming/stack2) we only have to change the second byte value to \x00

![alt text](https://imgur.com/itr5Dif.png)

