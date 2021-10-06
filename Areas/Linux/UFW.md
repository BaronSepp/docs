# Allow app from local addresses only
```shell
sudo ufw allow from 192.168.0.0/16 to any app Deluge
```

# Create a custom app
- Create a new file in the `/etc/ufw/applications.d` directory
- Add the following layout:
```ini
[Plex]
title=Plex Media Server
description=Plex is a global streaming media service and a client–server media player platform.
ports=32400/tcp

[Plex Services]
title=Plex Services
description=Different discovery services for use within the local network.
ports=1900,5353,32410,32412,32413,32414/udp|32469,8324/tcp
```
- Reload the UFW app:  `ufw app update Plex`