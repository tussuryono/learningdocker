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
## 7. Excecuting command on docker
Simple lab to running command di docker
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

root@osboxes:/home/osboxes# docker container run -d ubuntu:16.04 sleep 300
aea3999d5b268eb6b6cdcef7d0c45ec2c1b6ef2f491a0a8516759017997692f6

root@osboxes:/home/osboxes# docker container ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
aea3999d5b26        ubuntu:16.04        "sleep 300"         9 seconds ago       Up 6 seconds                            suspicious_black

root@osboxes:/home/osboxes# docker container exec suspicious_black cat /etc/hosts
127.0.0.1       localhost
::1     localhost ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
172.17.0.2      aea3999d5b26
root@osboxes:/home/osboxes#
```

docker run - attach dan detach
```script
root@osboxes:/home/osboxes# docker container run -d ubuntu:16.04 sleep 300
aea3999d5b268eb6b6cdcef7d0c45ec2c1b6ef2f491a0a8516759017997692f6

root@osboxes:/home/osboxes# docker container ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
aea3999d5b26        ubuntu:16.04        "sleep 300"         9 seconds ago       Up 6 seconds                            suspicious_black

root@osboxes:/home/osboxes# docker container run -d ubuntu:16.04 sleep 300
06c4106f404ba8b9ced4534a8ed95d0d7988b5544f642afb14b8c0d91f6e76b2
root@osboxes:/home/osboxes# docker container attach 06c41
^C^C^C^C
root@osboxes:/home/osboxes#

```

login on docker container
```script
root@osboxes:/home/osboxes# docker container run -it centos bash
Unable to find image 'centos:latest' locally
latest: Pulling from library/centos
8a29a15cefae: Pull complete
Digest: sha256:fe8d824220415eed5477b63addf40fb06c3b049404242b31982106ac204f6700
Status: Downloaded newer image for centos:latest

[root@b3d3a9d4000f /]# cat /etc/*release*
CentOS Linux release 8.1.1911 (Core)
Derived from Red Hat Enterprise Linux 8.1 (Source)
NAME="CentOS Linux"
VERSION="8 (Core)"
ID="centos"
ID_LIKE="rhel fedora"
VERSION_ID="8"
PLATFORM_ID="platform:el8"
PRETTY_NAME="CentOS Linux 8 (Core)"
ANSI_COLOR="0;31"
CPE_NAME="cpe:/o:centos:centos:8"
HOME_URL="https://www.centos.org/"
BUG_REPORT_URL="https://bugs.centos.org/"

CENTOS_MANTISBT_PROJECT="CentOS-8"
CENTOS_MANTISBT_PROJECT_VERSION="8"
REDHAT_SUPPORT_PRODUCT="centos"
REDHAT_SUPPORT_PRODUCT_VERSION="8"

CentOS Linux release 8.1.1911 (Core)
CentOS Linux release 8.1.1911 (Core)
cpe:/o:centos:centos:8

[root@b3d3a9d4000f /]# cat /etc/hosts
127.0.0.1       localhost
::1     localhost ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
172.17.0.2      b3d3a9d4000f
[root@b3d3a9d4000f /]#

```

re-run killed atau exited docker
```script
root@osboxes:/home/osboxes# docker container ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                      PORTS               NAMES
b3d3a9d4000f        centos              "bash"              3 minutes ago       Exited (0) 16 seconds ago                       xenodochial_einstein

root@osboxes:/home/osboxes# docker container start -a -i b3d3a
[root@b3d3a9d4000f /]# ls
bin  dev  etc  home  lib  lib64  lost+found  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
[root@b3d3a9d4000f /]# 

```

```script
root@osboxes:/home/osboxes# docker container ps
CONTAINER ID        IMAGE                     COMMAND             CREATED             STATUS              PORTS               NAMES
6fe3512b1450        kodekloud/simple-webapp   "python app.py"     7 minutes ago       Up 7 minutes        8080/tcp            frosty_sutherland
root@osboxes:/home/osboxes# docker exec -it frosty_sutherland /bin/sh
/opt # ls
Dockerfile        app.py            requirements.txt  templates
/opt # cat Dockerfile
FROM python:3.6-alpine

RUN pip install flask

COPY . /opt/

EXPOSE 8080

WORKDIR /opt

ENTRYPOINT ["python", "app.py"]
/opt #
```
running simple webapp on local server
```script
root@osboxes:/home/osboxes# docker run -p 38282:8080 --name blue-app -e APP_COLOR=blue kodekloud/simple-webapp
 This is a sample web application that displays a colored background.
 A color can be specified in two ways.

 1. As a command line argument with --color as the argument. Accepts one of red,green,blue,blue2,pink,darkblue
 2. As an Environment variable APP_COLOR. Accepts one of red,green,blue,blue2,pink,darkblue
 3. If none of the above then a random color is picked from the above list.
 Note: Command line argument precedes over environment variable.


No Command line argument. Color from environment variable =blue
 * Serving Flask app "app" (lazy loading)
 * Environment: production
   WARNING: Do not use the development server in a production environment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://0.0.0.0:8080/ (Press CTRL+C to quit)

root@osboxes:~# docker ps
CONTAINER ID        IMAGE                     COMMAND             CREATED             STATUS              PORTS                     NAMES
22766de4fa20        kodekloud/simple-webapp   "python app.py"     9 minutes ago       Up 9 minutes        0.0.0.0:38282->8080/tcp   blue-app
6fe3512b1450        kodekloud/simple-webapp   "python app.py"     22 hours ago        Up 22 hours         8080/tcp                  frosty_sutherland

root@osboxes:~# docker inspect blue-app
[
    {
        "Id": "22766de4fa20d3c6e3d663fb7bf5c781a62bba389da6c93eb9aa2edc3ca45e6f",
        "Created": "2020-05-31T07:57:37.639733617Z",
        "Path": "python",
        "Args": [
            "app.py"
        ],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 37261,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2020-05-31T07:57:40.485860708Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:c6e3cd9aae3645a98dd69c15b048614603efce6cda26c60f5f7e867ef68f729f",
        "ResolvConfPath": "/var/lib/docker/containers/22766de4fa20d3c6e3d663fb7bf5c781a62bba389da6c93eb9aa2edc3ca45e6f/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/22766de4fa20d3c6e3d663fb7bf5c781a62bba389da6c93eb9aa2edc3ca45e6f/hostname",
        "HostsPath": "/var/lib/docker/containers/22766de4fa20d3c6e3d663fb7bf5c781a62bba389da6c93eb9aa2edc3ca45e6f/hosts",
        "LogPath": "/var/lib/docker/containers/22766de4fa20d3c6e3d663fb7bf5c781a62bba389da6c93eb9aa2edc3ca45e6f/22766de4fa20d3c6e3d663fb7bf5c781a62bba389da6c93eb9aa2edc3ca45e6f-json.log",
        "Name": "/blue-app",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "docker-default",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "default",
            "PortBindings": {
                "8080/tcp": [
                    {
                        "HostIp": "",
                        "HostPort": "38282"
                    }
                ]
            },
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "CapAdd": null,
            "CapDrop": null,
            "Capabilities": null,
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "private",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "ConsoleSize": [
                0,
                0
            ],
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": null,
            "BlkioDeviceWriteBps": null,
            "BlkioDeviceReadIOps": null,
            "BlkioDeviceWriteIOps": null,
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "KernelMemory": 0,
            "KernelMemoryTCP": 0,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": false,
            "PidsLimit": null,
            "Ulimits": null,
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": [
                "/proc/asound",
                "/proc/acpi",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/sys/firmware"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/4b03b1aafdb338a2497bfbe1bf690e9ba795c70d3bdae2a716d457cbcc5005df-init/diff:/var/lib/docker/overlay2/c4933861030098dff97726213264fcaa9d6821a669dc0041eedf6e92b9ca2f96/diff:/var/lib/docker/overlay2/c68b72a25144dcc2d2d3cba077db82ef7cad637714428a0fbf0eb56230b4c8a9/diff:/var/lib/docker/overlay2/367b8e5b88f6f0e84574fcb38d68f3d9841a2e890ada8e6cc9a8aa1a1616dcdc/diff:/var/lib/docker/overlay2/7c263abcc505f9a7ebae040f8cfd8b705e2fc7d2b59d7f13795f510de4f5c4bb/diff:/var/lib/docker/overlay2/eb755a607ea9653d7cede0f5fde810d06b600d88cb445191ca306ef040081de8/diff:/var/lib/docker/overlay2/c945ce1e74cfb882dd1e503e06e1b16f96689de929cec56250a3f2c47eb0aa8e/diff:/var/lib/docker/overlay2/c36d93d426445d035b495d89314e54ba98cc24bbc971d01f8e1ecceaeecc79de/diff",
                "MergedDir": "/var/lib/docker/overlay2/4b03b1aafdb338a2497bfbe1bf690e9ba795c70d3bdae2a716d457cbcc5005df/merged",
                "UpperDir": "/var/lib/docker/overlay2/4b03b1aafdb338a2497bfbe1bf690e9ba795c70d3bdae2a716d457cbcc5005df/diff",
                "WorkDir": "/var/lib/docker/overlay2/4b03b1aafdb338a2497bfbe1bf690e9ba795c70d3bdae2a716d457cbcc5005df/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [],
        "Config": {
            "Hostname": "22766de4fa20",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": true,
            "AttachStderr": true,
            "ExposedPorts": {
                "8080/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "APP_COLOR=blue",
                "PATH=/usr/local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "LANG=C.UTF-8",
                "GPG_KEY=0D96DF4D4110E5C43FBFB17F2D347EA6AA65421D",
                "PYTHON_VERSION=3.6.6",
                "PYTHON_PIP_VERSION=18.1"
            ],
            "Cmd": null,
            "Image": "kodekloud/simple-webapp",
            "Volumes": null,
            "WorkingDir": "/opt",
            "Entrypoint": [
                "python",
                "app.py"
            ],
            "OnBuild": null,
            "Labels": {}
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "384452bdbaffd51d74a42edcd9ec4ad2fb4b19e2e9c5832af1aafab4b4200fab",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {
                "8080/tcp": [
                    {
                        "HostIp": "0.0.0.0",
                        "HostPort": "38282"
                    }
                ]
            },
            "SandboxKey": "/var/run/docker/netns/384452bdbaff",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "934af6a6e608cc443112516d11a99b45ec21f1628af10e4a6d43b3c9e5188bcc",
            "Gateway": "172.17.0.1",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "172.17.0.3",
            "IPPrefixLen": 16,
            "IPv6Gateway": "",
            "MacAddress": "02:42:ac:11:00:03",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "02759cbf6afa2110d53906492df0fd5af095e7413cee5b04506b9db2ea929ba3",
                    "EndpointID": "934af6a6e608cc443112516d11a99b45ec21f1628af10e4a6d43b3c9e5188bcc",
                    "Gateway": "172.17.0.1",
                    "IPAddress": "172.17.0.3",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:11:00:03",
                    "DriverOpts": null
                }
            }
        }
    }
]
root@osboxes:~# curl http://172.17.0.3:8080
<!doctype html>
<title>Hello from Flask</title>
<body style="background: #2980b9;"></body>
<div style="color: #e4e4e4;
    text-align:  center;
    height: 90px;
    vertical-align:  middle;">

  <h1>Hello from 22766de4fa20!</h1>

</div>root@osboxes:~#
```
running mysql database on docker
```script
root@osboxes:/home/osboxes# docker container run -d -e MYSQL_ROOT_PASSWORD=db_pass123 --name mysql-db mysql
Unable to find image 'mysql:latest' locally
latest: Pulling from library/mysql
afb6ec6fdc1c: Pull complete
0bdc5971ba40: Pull complete
97ae94a2c729: Pull complete
f777521d340e: Pull complete
1393ff7fc871: Pull complete
a499b89994d9: Pull complete
7ebe8eefbafe: Pull complete
597069368ef1: Pull complete
ce39a5501878: Pull complete
7d545bca14bf: Pull complete
211e5bb2ae7b: Pull complete
5914e537c077: Pull complete
Digest: sha256:a31a277d8d39450220c722c1302a345c84206e7fd4cdb619e7face046e89031d
Status: Downloaded newer image for mysql:latest
3d3e3524869715685dddc1147d58bed766705556fa53074ebafd4d58e757bac1
root@osboxes:/home/osboxes#

root@osboxes:~# docker container ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                 NAMES
3d3e35248697        mysql               "docker-entrypoint.s…"   About a minute ago   Up About a minute   3306/tcp, 33060/tcp   mysql-db
root@osboxes:~#

root@osboxes:~# docker exec mysql-db cat /etc/*release*
PRETTY_NAME="Debian GNU/Linux 10 (buster)"
NAME="Debian GNU/Linux"
VERSION_ID="10"
VERSION="10 (buster)"
VERSION_CODENAME=buster
ID=debian
HOME_URL="https://www.debian.org/"
SUPPORT_URL="https://www.debian.org/support"
BUG_REPORT_URL="https://bugs.debian.org/"
cat: /etc/lsb-release: No such file or directory

root@osboxes:~# docker exec -it mysql-db /bin/bash

root@3d3e35248697:/# mysql -u root -p
Enter password:
ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: YES)
root@3d3e35248697:/# mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 9
Server version: 8.0.20 MySQL Community Server - GPL

Copyright (c) 2000, 2020, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.02 sec)

mysql>

```

Membuat image
```script
$ docker build -t webapp-color
$ docker run -p 8282:8080 webapp-color

to check operating running on docker image use this command
$ docker run python:3.6 cat /etc/*release*
```
## 8. Docker Compose
## 9. Docker Engine and Storage
## 10. Docker Networking
## 11. Docker Registry
## 12. Lab Node JS
## 13. Lab Python
## 14. Lab Java
## 15. Summary
