# Configure the SSH server for Ed25510 certificates

Check version:

```Bash
ssh -V
``` 

## Edit the config file

Assuming that you're root, otherwise add `sudo`:

```Bash
vim /etc/ssh/sshd_config
```

Add:

```
HostKey /etc/ssh/ssh_host_ed25519_key
```

Ensure that the PubkeyAcceptedAlgorithms line includes ssh-ed25519. 
If it doesn’t, you can add or update it:

```
PubkeyAcceptedAlgorithms ssh-ed25519,ecdsa-sha2-nistp256,ecdsa-sha2-nistp384,ecdsa-sha2-nistp521,rsa-sha2-256,rsa-sha2-512
```

## Restart SSH

```Bash
service ssh restart
```

## Generate Host Keys

```Bash
ssh-keygen -t ed25519 -f /etc/ssh/ssh_host_ed25519_key -N ''
```

## Insure

```Bash
chown root:root /etc/ssh/ssh_host_*
chmod 600 /etc/ssh/ssh_host_*
```

## Verify

```Bash
journalctl -u sshd
```

