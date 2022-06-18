# load module @ startup

## Load module when Linux system comes up. File /etc/modules use to load kernel boot time. This file should contain the names of kernel modules that are to be loaded at boot time, one per line. First copy your module to /lib/modules/$(uname -r)/kernel/drivers. Following are suggested steps:

### 1. Create directory for hello module

 ```bash
mkdir -p /lib/modules/$(uname -r)/kernel/drivers/hello
```

### 2. Copy module

 ```bash
cp hello.ko /lib/modules/$(uname -r)/kernel/drivers/hello/
```

### 3. Edit /etc/modules file under Debian Linux

 ```bash
nano /etc/modules
```

### 4.  Add following line to it

 ```bash
hello
```

### 5. Reboot to see changes. Use lsmod or dmesg command to verify module loaded or not.

 ```bash
cat /proc/modules
```
or
 ```bash
```