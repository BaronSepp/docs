# Allow app from local addresses only
```shell
sudo ufw allow from 192.168.0.0/16 to any app Deluge
```

# Create a custom app
- Create a new file in the `/etc/ufw/applications.d` directory
- Add the following layout:
```toml
[Apache]
title=Web Server (HTTP,HTTPS)
description=Apache v2 is the next generation of the omnipresent Apache web server.
ports=80,443/tcp
```
