# View Connected RS232 Ports
```shell
cat /proc/tty/driver/serial
```

# Restart all edge modules
```shell
iotedge list | awk '{if (NR!=1 && $1!="edgeAgent" && $1!="edgeHub" && $1!="Controller"){print $1}}' | xargs -L 1 iotedge restart
```