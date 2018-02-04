### ssh
`systemctl status sshd` => check the status of the ssh service

create a config file
~/.ssh/config

example:
Host server1
        HostName 192.168.1.115
        User root
        Port 22

`ssh-keygen -t rsa` => generating a public/private rsa key

`ssh-copy-id -i id_rsa.pub server1` => copies the public key onto the server

`ssh-agent bash` => new bash shell
`ssh-add` => athenticate a key passphrase

### scp - secure copy protocol

`scp ~/file.txt 192.168.1.115:/tmp` => copy files to server

`scp 192.168.1.115:/tmp/file.txt .` => copy the file from the server to the current local directory

use `winscp` to copy files from windows machine to linux via a gui client.

