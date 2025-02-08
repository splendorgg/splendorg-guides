---
title: VM SSH Connection Guide
---


This guide provides step-by-step instructions to set up and configure an SSH connection to a virtual machine(VM) securely.

## On the Local Machine

##### 1. Install and Start OpenSSH Server

Run the following commands to install and start the SSH server:

```bash
sudo apt install openssh-server
sudo systemctl start ssh
```

##### 2. Get the Local IP Address

Retrieve your local IP address using one of the following commands:

```` ip a ```` or ```` hostname -I ````


##### 3. Generate an SSH Key Pair

Create a new SSH key pair with the following command:

```bash
ssh-keygen -t ed25519 -f ~/.ssh/<filename> -C "<comment>"
```

Replace filename with your desired key file name.

Replace comment with a descriptive comment.


##### 4. Copy the Public Key to the Server

Transfer the public key to the server:

```bash
ssh-copy-id -i ~/.ssh/filename.pub user@ip
```

Replace user with the server username.

Replace ip with the server’s IP address.

##### 5. Test the SSH Connection

Log in to the server to verify the key-based authentication:

```bash
ssh user@ip
```

If successful, you will authenticate using the key.

##### 6. Configure the SSH Client (Optional)

To simplify future connections, configure your SSH client:

```bash
nano ~/.ssh/config
```

Add the following lines to the file:

```
Host <name>
    HostName <server_ip>
    IdentityFile ~/.ssh/<filename>
    User <server_user>
```
Replace *name* with an alias for the connection.

Replace *server_ip* with the server’s IP address.

Replace *filename* with the private key file name.

Replace *server_user* with the server’s username.

You can now connect using the alias:

```bash
ssh <name>
```

## On the VM or Server

##### 1. Update SSH Configuration for Security

Edit the SSH server configuration file:

```bash
sudo nano /etc/ssh/sshd_config
```

Modify the following settings:

```
PasswordAuthentication no
PermitRootLogin no
```

PasswordAuthentication no: Disables password-based login.

PermitRootLogin no: Prevents root user login via SSH.

##### 2. Reload the SSH Service

Apply the changes by reloading the SSH service:

```bash
sudo systemctl reload ssh
```

Your SSH setup is now complete. Ensure that the private key is stored securely and avoid sharing it.

