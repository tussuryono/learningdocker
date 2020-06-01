# Konfigurasi lab environment

### Tools
- virtualbox.org
- osboxes.org
- OS Linux Ubuntu 20.04
### Konfigurasi
Konfigurasi VM :
1. Virtual Network Card untuk vm lab-docker disetting menjadi bridge adapter
2. CPU 2 Core
3. RAM 4 GB
4. Disk kurang lebih 5 GB : Menggunakan file VDI dari osboxes.org

Konfigurasi OS:
1. Setting IP Address VM menjadi static
```script
$ cat /etc/cloud/cloud.cfg.d/subiquity-disable-cloudinit-networking.cfg
network: {config: disabled}
$

$ ip add show

// Perubahan konfigurasi dari DHCP ke Stati IP
$ sudo vi /etc/netplan/00-installer-config.yaml
# This is the network config written by 'subiquity'
network:
  ethernets:
    enp0s3:
      dhcp4: true
  version: 2

// Menjadi
network:
  ethernets:
    enp0s3:
      addresses: [192.168.1.3/24]
      gateway4: 192.168.1.1
      nameservers:
        addresses: [4.2.2.2, 8.8.8.8]
  version: 2

// apply konfigurasi 
$ sudo netplan apply

// Verifikasi konfigurasi
$ ip add show
$ ip route show

```

2. Konfigurasi ssh
```script

$ sudo apt-get install ssh
$ sudo systemctl enable --now ssh
$ sudo systemctl status ssh

```
