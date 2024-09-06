# Configure the SSH server for Ed25510 certificates

Check version:

```Bash
ssh -V
``` 

## Edit the config file

```Bash
sudo vim /etc/ssh/sshd_config
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
sudo systemctl restart sshd
```

Or:

```Bash
sudo service sshd restart
```

## Generate Host Keys

```Bash
sudo ssh-keygen -t ed25519 -f /etc/ssh/ssh_host_ed25519_key -N ''
```

## Verify

```Bash
sudo journalctl -u sshd
```

