# Jarkom-Modul-2-IT14-2024

| No. | Nama Anggota | NRP |
| :---         |     :---:      |          ---: |
| 1.   | Rizki Ramadhani     | 5027221013    |
| git diff     | git diff       | git diff      |

## NO.1
### Konfigurasi GNS3
* Erangel - Router
```
auto eth0
iface eth0 inet dhcp
    hostname ubuntu-1-1

auto eth1
iface eth1 inet static
    address 192.240.1.1
    netmask 255.255.255.0
    
auto eth2
iface eth2 inet static
    address 192.240.2.1
    netmask 255.255.255.0
    
auto eth3
iface eth3 inet static
    address 192.240.3.1
    netmask 255.255.255.0
```
* Pochinki - DNS master

```
  auto eth0
iface eth0 inet static
        address 192.240.3.2
        netmask 255.255.255.0
        gatewa192.240.3.1
```

* Gergopol - DNS slave
```
auto eth0
iface eth0 inet static
        address 192.240.2.2
        netmask 255.255.255.0
        gatewa192.240.2.1
```
* Rohzok - Client
```
auto eth0
iface eth0 inet static
        address 192.240.1.2
        netmask 255.255.255.0
        gateway 192.240.1.1
```
* School - Client
```
auto eth0
iface eth0 inet static
        address 192.240.1.3
        netmask 255.255.255.0
        gateway 192.240.1.1
```
* Mylta - Load Balancer
```
auto eth0
iface eth0 inet static
        address 192.240.1.3
        netmask 255.255.255.0
        gateway 192.240.1.1
```
* Severny - Web Server
```
  auto eth0
iface eth0 inet static
        address 192.240.2.4
        netmask 255.255.255.0
        gatewa192.240.2.1
```
* Stalber - Web Server
```
auto eth0
iface eth0 inet static
        address 192.240.2.5
        netmask 255.255.255.0
        gateway 192.240.2.1
```
* Lipvoka - Web Server
```
auto eth0
iface eth0 inet static
        address 192.240.2.6
        netmask 255.255.255.0
        gateway 192.240.2.1
```
### Menambahkan di Router - Erangel
```
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.240.0.0/16
```
## No.2
### Scrip
* 
