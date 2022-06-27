# Globalization issue in Alpine [[Linux]] containers
```Dockerfile
# Install cultures (same approach as Alpine SDK image)
RUN apk add --no-cache icu-libs

# Disable the invariant mode (set in base image)
ENV DOTNET_SYSTEM_GLOBALIZATION_INVARIANT=false
```

# Enable support for older cryptography ciphers in Ubuntu [[Linux]]
[Microsoft Documentation](https://docs.microsoft.com/en-us/dotnet/core/compatibility/cryptography/5.0/default-cipher-suites-for-tls-on-linux)

Script to downgrade the containers internal security as older cypher suites which have been disabled for Linux since .NET 5

```bash
#!/bin/bash

# Variables
PREPEND="openssl_conf = default_conf"
APPEND="[ default_conf ]\nssl_conf = ssl_sect\n\n[ssl_sect]\nsystem_default = system_default_sect\n\n[system_default_sect]\nCipherString = DEFAULT:@SECLEVEL=1"

# Modify OpenSSL config
mv /etc/ssl/openssl.cnf /etc/ssl/openssl.cnf.bak
echo ${PREPEND} > /etc/ssl/openssl.cnf
cat /etc/ssl/openssl.cnf.bak >> /etc/ssl/openssl.cnf
echo -e ${APPEND} >> /etc/ssl/openssl.cnf
rm /etc/ssl/openssl.cnf.bak

# Refresh certificates
update-ca-certificates --fresh
```