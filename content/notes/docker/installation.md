---
title: Docker Installation
---

### Set up the repository
```bash
sudo dnf -y install dnf-plugins-core
sudo dnf-3 config-manager --add-repo https://download.docker.com/linux/fedora/docker-ce.repo
```
### Install the docker packages
```bash
sudo dnf install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
### Start docker engine
```bash
sudo systemctl enable --now docker
```
### Verify the installation
```bash
sudo docker run hello-world
```
### Download the RPM package
### Install the package (go to package directory)
```bash
sudo dnf install ./docker-desktop-x86_64.rpm
```

# Sign in
### Generate key
```bash
gpg --generate-key
```
### Get the key
```bash
gpg --list-secret-keys

sec rsa4096 2025-01-11 [SC] [expires: 2027-01-11] 
ABCDEFGH12345678 -- This the key
uid [ultimate] Your Name <your-email@example.com> 
ssb rsa4096 2025-01-11 [E]
```
### Initialize pass
```bash
pass init <your_generated_gpg-id_public_key>
```
