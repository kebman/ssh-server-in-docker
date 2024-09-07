# Generate Client Keys (for the respective client)

Assuming you've `passwd` and `su` to `clientuser`.

```Bash
ssh-keygen -t ed25519 -a 101 -f ~/.ssh/id_ed25519
```

`-t` ed25519 specifies the key type. 
- Ed25519 keys are based on the X25519 key exchange curve.
`-a` 101 specifies the number of rounds for key derivation function (KDF). 
- This makes brute-force attacks more difficult.
`-f ~/.ssh/id_ed25519` specifies the file where the private key will be saved.

## Simpler (normal)

```Bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

## Simplest

```Bash
ssh-keygen -t ed25519
```

## Copy Client Keys to the Server

```Bash
ssh-copy-id -i ~/.ssh/id_ed25519.pub testuser@remote_server
```

```Bash
ssh-copy-id -i ~/.ssh/id_ed25519.pub testuser@172.19.0.2
```

# Ed25519 vs X25519

The Ed25519 algorithm is a specific instantiation of the X25519 curve for digital signatures. 
Meanwhile X25519 is used for key exchange.
When dealing with SSH keys, you use Ed25519 for signing and authentication.

