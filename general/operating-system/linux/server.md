# Server

## Allow a server to use a password to do an ssh login

install ssh server: `sudo apt-get install openssh-server`

enable and start the ssh service: 

```text
sudo systemctl enable ssh
sudo systemctl start ssh
```

go to `/etc/ssh/sshd_config` 

replace old commands to:

```text
ListenAddress 0.0.0.0
PermitRootLogin yes
PasswordAuthentication yes
ChallengeResponseAuthentication yes
```

restart the ssh service: `sudo service ssh restart`

## Sent your ssh public key to a server

```bash
ssh-copy-id pi@192.168.49.17
```

## Disable password login

```text
PermitRootLogin yes
PasswordAuthentication no
UsePAM no
ChallengeResponseAuthentication no
```

restart the ssh service: `sudo systemctl reload ssh`

