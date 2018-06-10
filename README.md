# Image Builder

This is a sample project to create base images using [Packer](https://www.packer.io/) and [Ansible](https://www.ansible.com/).

The images created from this project are thought to be used as base images and not to be used as final VM images.

Included images:

- **Base Ubuntu Server for Azure**. Includes:
  - Ubuntu 18.04-LTS
  - Unattended upgrades activated
  - `vim` and `htop`
- **Dotnet Linux for Azure**. Includes:
  - Base Ubuntu Server for Azure
  - Dotnet SDK 2.1
- **Nginx Linux for Azure**. Includes:
  - Base Ubuntu Server for Azure
  - Nginx

## Running locally/CI

1. Install [Ansible](https://docs.ansible.com/ansible/2.3/intro_installation.html) and [Packer](https://www.packer.io/docs/install/index.html).

2. Set Azure service principal auth values as environment variables:

```bash
export ARM_SUBSCRIPTION_ID="XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX"
export ARM_CLIENT_ID="XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX"
export ARM_CLIENT_SECRET="XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX"
export ARM_TENANT_ID="XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX"
```


1. Install project required modules from ansible-galaxy:

```bash
ansible-galaxy install ocha.dotnet-core
ansible-galaxy install jnv.unattended-upgrades
```

4. Create images:

```bash
sudo useradd -m ansibledeploy
sudo usermod -aG sudo ansibledeploy
cd src/packer
export IMAGE_VERSION="version-number"
packer build imagename.yml
```
