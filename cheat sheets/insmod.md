#         insmod

## 1. create files
> create a compiling folder with the app name, then create tow file the .c and the make file

the hello.c file:
```cpp

/*  
 *  hello.c - The simplest kernel module.
 */

#include <linux/module.h>   /* Needed by all modules */
#include <linux/kernel.h>   /* Needed for KERN_INFO */

int init_module(void)
{
    printk(KERN_INFO "Hello world 1.\n");

    /* 
     * A non 0 return means init_module failed; module can't be loaded. 
     */
    return 0;
}

void cleanup_module(void)
{
    printk(KERN_INFO "Goodbye world 1.\n");
}
```

## 2. compile
Makefile:
> !make sure to have a capital 'M' in the file name, otherwise it wont works
```
obj-m = hello.o
KVERSION = $(shell uname -r)
all:
        make -C /lib/modules/$(KVERSION)/build M=$(PWD) modules
clean:
        make -C /lib/modules/$(KVERSION)/build M=$(PWD) clean
```

then run make then insmod app.ko :
> ! be careful to install your 'linux-headers-5.xx.xx-xx-amd64' before run make comman
```bash
make
insmod hello.ko
```

## 2. Check

Verify that module loaded using the
 ```bash
lsmod | grep hello
```

See message in /var/log/message file using the tail command
 ```bash
tail -f /var/log/message
```
or

Unload the module using the rmmod command
 ```bash
rmmod hello
```