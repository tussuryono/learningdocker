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
### Simple way
Metode ini dikenal sebagai install using the convenience script
```script
osboxes@osboxes:~$ curl -fsSL https://get.docker.com -o get-docker.sh
osboxes@osboxes:~$ sudo sh get-docker.sh
```
## First Run
```script
root@osboxes:/home/osboxes# docker container ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES

root@osboxes:/home/osboxes# docker container run ubuntu sleep 10
Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
d51af753c3d3: Pull complete
fc878cd0a91c: Pull complete
6154df8ff988: Pull complete
fee5db0ff82f: Pull complete
Digest: sha256:747d2dbbaaee995098c9792d99bd333c6783ce56150d1b11e333bbceed5c54d7
Status: Downloaded newer image for ubuntu:latest

root@osboxes:/home/osboxes#

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
Menampilkan list container
```script
root@osboxes:/home/osboxes# docker run -d ubuntu sleep 60
c3ffc4493de512db116b59e0f9fe0f52f418c380771fafbe4a2974c568e4e05e

root@osboxes:/home/osboxes# docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
c3ffc4493de5        ubuntu              "sleep 60"          9 seconds ago       Up 6 seconds                            clever_goldberg

root@osboxes:/home/osboxes# docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED              STATUS                           PORTS               NAMES
c3ffc4493de5        ubuntu              "sleep 60"          20 seconds ago       Up 18 seconds                                        clever_goldberg
529e5910b15b        ubuntu              "sleep 60"          About a minute ago   Exited (0) 35 seconds ago                            intelligent_khorana
3e706ab05f6c        ubuntu              "sleep 10"          49 minutes ago       Exited (0) 48 minutes ago                            elastic_hoover
cd2796d6ba12        ubuntu:16.04        "sleep 300"         About an hour ago    Exited (137) About an hour ago                       strange_chaplygin
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
### Membuat container aktif selama 5 menit
```script
root@osboxes:/home/osboxes# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ubuntu              16.04               005d2078bdfa        5 weeks ago         125MB
ubuntu              latest              1d622ef86b13        5 weeks ago         73.9MB

root@osboxes:/home/osboxes# docker run ubuntu:16.04 sleep 300
```
Pada posisi tersebut container akan aktif selama 5 menit dan kita tidak bisa exit dari kondisi tersebut sampai container secara otomatis exited (off).
Proses exited dapat dilakukan secara manual dengan re-login ssh dan menjalankan perintah berikut
```script
root@osboxes:~# docker container ps
CONTAINER ID        IMAGE               COMMAND             CREATED              STATUS              PORTS               NAMES
cd2796d6ba12        ubuntu:16.04        "sleep 300"         About a minute ago   Up About a minute                       strange_chaplygin

root@osboxes:~# docker container stop strange_chaplygin
strange_chaplygin
root@osboxes:~#
```

### Menghapus container yang sudah exited
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
