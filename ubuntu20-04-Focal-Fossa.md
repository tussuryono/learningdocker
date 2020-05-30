# Docker di Ubuntu 20.04 Focal Fossa
Environment requirement :
1. Virtualbox
2. VM:
    - CPU : 2 vCPU
    - RAM : 4 GB
    - DISK : 50 GB
    - OS : Ubuntu 20.04 Focal Fossa
## 1. Instalasi Docker
Dokumentasi untuk instalasi dapat diperoleh di https://docs.docker.com/engine/install/ubuntu/
### Simple way
Metode ini dikenal sebagai install using the convenience script
```script
osboxes@osboxes:~$ curl -fsSL https://get.docker.com -o get-docker.sh
osboxes@osboxes:~$ sudo sh get-docker.sh
```
## 2. First Run
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

## 3. Docker Pull
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
## 4. Docker Run
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
## 5. Docker Stop
### Menghentikan (stop) docker yang aktive
Seperti di contoh sebelumnya, perintah untuk stop container docker adalah sebagai berikut:
```script
root@osboxes:~# docker container ps
CONTAINER ID        IMAGE               COMMAND             CREATED              STATUS              PORTS               NAMES
cd2796d6ba12        ubuntu:16.04        "sleep 300"         About a minute ago   Up About a minute                       strange_chaplygin

root@osboxes:~# docker container stop strange_chaplygin
strange_chaplygin
root@osboxes:~#
```

### Menghapus container yang sudah exited
Semua container yang sudah dalam kondisi exited dapat di remove dari docker list dengan command sebagai berikut:
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
```script
root@osboxes:/home/osboxes# docker container run ubuntu cat /etc/hosts
127.0.0.1       localhost
::1     localhost ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
172.17.0.2      a9a34ec509fc

root@osboxes:/home/osboxes# docker container run ubuntu cat /etc/netplan/00-installer-config.yaml
cat: /etc/netplan/00-installer-config.yaml: No such file or directory

root@osboxes:/home/osboxes# docker container ps -a -s
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                      PORTS               NAMES                   SIZE
0004e58f77fd        ubuntu              "cat /etc/netplan/00…"   46 seconds ago      Exited (1) 44 seconds ago                       pedantic_joliot         0B (virtual 73.9MB)
a9a34ec509fc        ubuntu              "cat /etc/hosts"         2 minutes ago       Exited (0) 2 minutes ago                        frosty_einstein         0B (virtual 73.9MB)
8487c62eee52        ubuntu              "cat /etc/lsb-releas…"   4 minutes ago       Exited (0) 4 minutes ago                        wizardly_visvesvaraya   0B (virtual 73.9MB)
root@osboxes:/home/osboxes#

```
Setelah melakukan penghapusan container yang tidak aktif maka free space akan tersedia kembali, karena setiap perintah docker run akan berdampak penggunaan space storage.

Metode menghapus container dengan menggunakan keyword container id
```script
root@osboxes:/home/osboxes# docker container ps -a -s
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                      PORTS               NAMES                   SIZE
d03c5ca1a1a5        ubuntu              "cat /etc/hosts"         6 minutes ago       Exited (0) 6 minutes ago                        sweet_wescoff           0B (virtual 73.9MB)
0004e58f77fd        ubuntu              "cat /etc/netplan/00…"   10 minutes ago      Exited (1) 10 minutes ago                       pedantic_joliot         0B (virtual 73.9MB)
a9a34ec509fc        ubuntu              "cat /etc/hosts"         12 minutes ago      Exited (0) 12 minutes ago                       frosty_einstein         0B (virtual 73.9MB)
8487c62eee52        ubuntu              "cat /etc/lsb-releas…"   14 minutes ago      Exited (0) 14 minutes ago                       wizardly_visvesvaraya   0B (virtual 73.9MB)
root@osboxes:/home/osboxes# docker container rm d03c 0004 a9a34 8487c
d03c
0004
a9a34
8487c
root@osboxes:/home/osboxes# docker container ps -a -s
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES               SIZE
root@osboxes:/home/osboxes#
```
## 6. Docker Images
Mendownload image dari docker hub
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
Menghapus image docker
```script
root@osboxes:/home/osboxes# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ubuntu              16.04               005d2078bdfa        5 weeks ago         125MB
ubuntu              latest              1d622ef86b13        5 weeks ago         73.9MB
root@osboxes:/home/osboxes# docker rmi ubuntu
Untagged: ubuntu:latest
Untagged: ubuntu@sha256:747d2dbbaaee995098c9792d99bd333c6783ce56150d1b11e333bbceed5c54d7
Deleted: sha256:1d622ef86b138c7e96d4f797bf5e4baca3249f030c575b9337638594f2b63f01
Deleted: sha256:279e836b58d9996b5715e82a97b024563f2b175e86a53176846684f0717661c3
Deleted: sha256:39865913f677c50ea236b68d81560d8fefe491661ce6e668fd331b4b680b1d47
Deleted: sha256:cac81188485e011e56459f1d9fc9936625a1b62cacdb4fcd3526e5f32e280387
Deleted: sha256:7789f1a3d4e9258fbe5469a8d657deb6aba168d86967063e9b80ac3e1154333f

root@osboxes:/home/osboxes# docker rmi ubuntu
Error: No such image: ubuntu

root@osboxes:/home/osboxes# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ubuntu              16.04               005d2078bdfa        5 weeks ago         125MB
root@osboxes:/home/osboxes# docker rmi ubuntu:16.04
Untagged: ubuntu:16.04
Untagged: ubuntu@sha256:db6697a61d5679b7ca69dbde3dad6be0d17064d5b6b0e9f7be8d456ebb337209
Deleted: sha256:005d2078bdfab5066ae941cea93f644f5fd25521849c870f4e1496f4526d1d5b
Deleted: sha256:a83c92a7c7a0f4a52fc74fa38496be9a5e6b738bc5fd5d60e54768fed238c173
Deleted: sha256:c6a36d55655e576fc8166a32fd05e281d03bedc26b1118902e92e7ba421dfa72
Deleted: sha256:d1c997f15060e07ff557383387d6839e0377873837025fc843fa5d94bea2c4e5
Deleted: sha256:b592b5433bbffb04389a0e6349cdba6af8d006779bbb93beb69aa77d59133be4
root@osboxes:/home/osboxes#
```
## 7. Docker Compose
## 8. Docker Engine and Storage
## 8. Docker Networking
## 9. Docker Registry
## 10. Lab Node JS
## 11. Lab Python
## 12. Lab Java
## 13. Summary
