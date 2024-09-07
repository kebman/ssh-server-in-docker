# Sync Project With Dropbox

Create the project in Dropbox if it doesn't already exist:

```Bash
mkdir -p /mnt/d/Users/kebman/Dropbox/projects/linux/ssh-server-in-docker
```

Then spin up `rsync`:

```Bash
rsync -av /home/kebman/projects/ssh-server-in-docker/ /mnt/d/Users/kebman/Dropbox/projects/linux/ssh-server-in-docker/
```

