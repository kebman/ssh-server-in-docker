# Check SSHD Status

As root:

```Bash
service ssh status
```

If it's not running:

```Bash
service ssh start
```

## Alternative Status Check

```Bash
ssh localhost
```

You don't have to actually connect, just check that the process starts.

```Bash
ps aux | grep sshd
```

## Debugging

Run SSHD in the foreground for debugging

```Bash
/usr/sbin/sshd -D
```

