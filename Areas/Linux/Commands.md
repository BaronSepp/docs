# View Connected RS232 Ports
```shell
cat /proc/tty/driver/serial
```

# Restart all edge modules
```shell
iotedge list | awk '{if (NR!=1){print $1}}' | xargs -L 1 iotedge restart
```