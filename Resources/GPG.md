# List Keys
```shell
gpg --list-secret-keys
gpg --list-keys
```

# Delete Keys
```shell
gpg --delete-secret-key <ID>
gpg --delete-key <ID>
```

# Import key
```shell
gpg --import <FilePath>
```

# Change key password
```shell
gpg --edit-key <ID>
passwd
```

# Edit key trust
```shell
gpg --edit-key <ID> trust
gpg --update-trustdb
```