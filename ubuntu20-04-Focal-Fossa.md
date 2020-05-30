# Docker di Ubuntu 20.04 Focal Fossa
Environment requirement :
1. Virtualbox
2. VM:
    - CPU : 2 vCPU
    - RAM : 4 GB
    - DISK : 50 GB
    - OS : Ubuntu 20.04 Focal Fossa
## Instalasi Docker
Dokumentasi untuk instalasi dapat diperoleh di https://docs.docker.com/engine/install/ubuntu/

## First Run
```script
root@osboxes:/home/osboxes# docker container ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES

root@osboxes:/home/osboxes# docker container run ubuntu cat /etc/*release*
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=20.04
DISTRIB_CODENAME=focal
DISTRIB_DESCRIPTION="Ubuntu 20.04 LTS"
NAME="Ubuntu"
VERSION="20.04 LTS (Focal Fossa)"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu 20.04 LTS"
VERSION_ID="20.04"
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
VERSION_CODENAME=focal
UBUNTU_CODENAME=focal

root@osboxes:/home/osboxes# docker container ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAME

root@osboxes:/home/osboxes# docker container ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                      PORTS               NAMES
5abd135b2c0d        ubuntu              "cat /etc/lsb-releas…"   15 seconds ago      Exited (0) 13 seconds ago                       zealous_feynman

root@osboxes:/home/osboxes#
```

## Docker Run
## Docker Images
## Docker Compose
## Docker Engine and Storage
## Docker Networking
## Docker Registry
## Lab Node JS
## Lab Python
## Lab Java
## Summary
