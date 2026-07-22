# SSH Keys vs Password Login

## Hostinger

- Root password is auto-generated
- SSH keys are not provided automatically
- Login: ssh root@SERVER_IP

## AWS EC2

- Download .pem key during server creation
- No password login by default
- Login: ssh -i key.pem ubuntu@SERVER_IP

## Hetzner

- Add public SSH key during server creation
- No password required

## Create SSH key

ssh-keygen -t ed25519 -C "devi@wizinoa.com"

## Public key

~/.ssh/id_ed25519.pub

Safe to share and upload to servers.

## Private key

~/.ssh/id_ed25519

Never share this file.

## Add public key to server

mkdir -p ~/.ssh
nano ~/.ssh/authorized_keys
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys

## Password-less login

ssh devi@SERVER_IP

## Recommendation for beginners

Start with Hostinger password login, then configure your own SSH key after the initial setup.
