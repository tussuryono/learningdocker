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
## Docker Pull
```script
root@osboxes:/home/osboxes# docker pull ubuntu:16.04
16.04: Pulling from library/ubuntu
e92ed755c008: Pull complete
b9fd7cb1ff8f: Pull complete
ee690f2d57a1: Pull complete
53e3366ec435: Pull complete
Digest: sha256:db6697a61d5679b7ca69dbde3dad6be0d17064d5b6b0e9f7be8d456ebb337209
Status: Downloaded newer image for ubuntu:16.04
docker.io/library/ubuntu:16.04

root@osboxes:/home/osboxes# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ubuntu              16.04               005d2078bdfa        5 weeks ago         125MB
ubuntu              latest              1d622ef86b13        5 weeks ago         73.9MB
root@osboxes:/home/osboxes#

```
## Docker Run
Menghapus container yang sudah exited
```script
root@osboxes:/home/osboxes# docker container ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES

root@osboxes:/home/osboxes# docker container ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                      PORTS               NAMES
5abd135b2c0d        ubuntu              "cat /etc/lsb-releas…"   13 minutes ago      Exited (0) 13 minutes ago                       zealous_feynman

root@osboxes:/home/osboxes# docker container rm zealous_feynman
zealous_feynman

root@osboxes:/home/osboxes# docker container ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
root@osboxes:/home/osboxes#
```

## Docker Images
## Docker Compose
## Docker Engine and Storage
## Docker Networking
## Docker Registry
## Lab Node JS
## Lab Python
## Lab Java
## Summary
