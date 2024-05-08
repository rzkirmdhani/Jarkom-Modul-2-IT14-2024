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
![topologidni](https://github.com/rzkirmdhani/Jarkom-Modul-2-IT14-2024/assets/141987387/33ce5871-2f13-4fe7-8bdf-c26e71b4edae)

## No.2
### Scrip
* /root/scrip.sh
```
apt-get update
apt-get install dnsutils bind9 -y
```
### Config
* etc/bind/named.conf.local
```
zone "airdrop.it14.com" {
        type master;
        file "/etc/bind/it14/airdrop.it14.com";
};
```
### Lakukan sebelum config DNS
```
cp /etc/bind/db.local /etc/bind/it14/name.it14.com
```
### Restart setelah config

```
service bind9 restart
```

### Config DNS

- /etc/bind/it14/airdrop.it14.com

```
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     airdrop.it14.com. root.airdrop.it14.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@             IN      NS      airdrop.it14.com.
@             IN      A       192.240.1.3 ; IP airdrop
www           IN      CNAME   airdrop.it14.com.
```

- Ubah nameserver client Rohzok ke Pochinki

```
#nameserver 192.168.122.1
nameserver 192.240.3.2
```

- testing di Ruins

```
ping airdrop.it14.com
```

- Ubah nameserver client School ke Pochinki

```
#nameserver 192.168.122.1
nameserver 192.240.3.2
```

- testing di School

```
ping airdrop.it14.com
```
