# TP5 : Un ptit LAN à nous
## I. Setup
## ☀️ Uniquement avec des commandes, prouvez-que :
### - vous avez bien configuré les adresses IP demandées
### Pour le client1 :
```powershell
matheo@matheo-VirtualBox:~$ ip a

2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:fe:26:ae brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.11/24 brd 10.5.1.255 scope global noprefixroute enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fefe:26ae/64 scope link
       valid_lft forever preferred_lft forever

matheo@matheo-VirtualBox:~$ ip r s

default via 10.5.1.254 dev enp0s8 proto static metric 20100
10.5.1.0/24 dev enp0s8 proto kernel scope link src 10.5.1.11 metric 100
```
### Pour le client2 :
```powershell
matheo@matheo-VirtualBox:~$ ip a

2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:6e:af:81 brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.12/24 brd 10.5.1.255 scope global noprefixroute enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe6e:af81/64 scope link
       valid_lft forever preferred_lft forever

matheo@matheo-VirtualBox:~$ ip r s

default via 10.5.1.254 dev enp0s8 proto static metric 20100
10.5.1.0/24 dev enp0s8 proto kernel scope link src 10.5.1.12 metric 100
```
### Pour le routeur :
```powershell 
[root@localhost matheo]# ip a

3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:c2:60:09 brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.254/24 brd 10.5.1.255 scope global noprefixroute enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fec2:6009/64 scope link
       valid_lft forever preferred_lft forever
```
### Pour Mon PC :
```powershell 
PS C:\Users\mathe> ipconfig

Carte Ethernet Ethernet 4 :

   Suffixe DNS propre à la connexion. . . :
   Adresse IPv6 de liaison locale. . . . .: fe80::3ccd:81d3:1d7c:1fb4%66
   Adresse IPv4. . . . . . . . . . . . . .: 10.5.1.1
   Masque de sous-réseau. . . . . . . . . : 255.255.255.0
   Passerelle par défaut. . . . . . . . . :
```
### - vous avez bien configuré les hostnames demandés
### Pour le client1 :
```powershell
matheo@matheo-VirtualBox:~$ sudo hostnamectl set-hostname client1.tp5.b1

matheo@matheo-VirtualBox:~$ sudo hostnamectl
 Static hostname: client1.tp5.b1
       Icon name: computer-vm
         Chassis: vm 🖴
      Machine ID: 51d4c1831e3b4e3880c7058278608ed4
         Boot ID: ef9659663a934d5daee25ba50163c512
  Virtualization: oracle
Operating System: Ubuntu 24.04.1 LTS
          Kernel: Linux 6.8.0-45-generic
    Architecture: x86-64
 Hardware Vendor: innotek GmbH
  Hardware Model: VirtualBox
Firmware Version: VirtualBox
   Firmware Date: Fri 2006-12-01
    Firmware Age: 17y 10month 2w
```
### Pour le client2 :
```powershell
matheo@matheo-VirtualBox:~$ sudo hostnamectl set-hostname client2.tp5.b1

matheo@matheo-VirtualBox:~$ sudo hostnamectl
 Static hostname: client2.tp5.b1
       Icon name: computer-vm
         Chassis: vm 🖴
      Machine ID: 51d4c1831e3b4e3880c7058278608ed4
         Boot ID: 81377c32ab854ed186af25ca99785c66
  Virtualization: oracle
Operating System: Ubuntu 24.04.1 LTS
          Kernel: Linux 6.8.0-45-generic
    Architecture: x86-64
 Hardware Vendor: innotek GmbH
  Hardware Model: VirtualBox
Firmware Version: VirtualBox
   Firmware Date: Fri 2006-12-01
    Firmware Age: 17y 10month 2w
```
### Pour le routeur :
```powershell
[root@localhost matheo]# sudo hostnamectl set-hostname routeur.tp5.b1
[root@localhost matheo]# sudo hostnamectl
 Static hostname: routeur.tp5.b1
       Icon name: computer-vm
         Chassis: vm 🖴
      Machine ID: 28aeb8b755d44fac9a255d433031a303
         Boot ID: 5acf4dc0803340c8af40a483becdd23c
  Virtualization: oracle
Operating System: Rocky Linux 9.4 (Blue Onyx)
     CPE OS Name: cpe:/o:rocky:rocky:9::baseos
          Kernel: Linux 5.14.0-427.13.1.el9_4.x86_64
    Architecture: x86-64
 Hardware Vendor: innotek GmbH
  Hardware Model: VirtualBox
Firmware Version: VirtualBox
```
### - tout le monde peut se ping au sein du réseau 10.5.1.0/24

## Ping du :
### Routeur vers client1 :
```powershell
[root@localhost matheo]# ping 10.5.1.11
PING 10.5.1.11 (10.5.1.11) 56(84) bytes of data.
64 bytes from 10.5.1.11: icmp_seq=1 ttl=64 time=0.934 ms
64 bytes from 10.5.1.11: icmp_seq=2 ttl=64 time=0.413 ms
64 bytes from 10.5.1.11: icmp_seq=3 ttl=64 time=0.449 ms
64 bytes from 10.5.1.11: icmp_seq=4 ttl=64 time=0.288 ms
^C
--- 10.5.1.11 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3066ms
rtt min/avg/max/mdev = 0.288/0.521/0.934/0.245 ms
```
### Routeur vers client2 :
```powershell
[root@localhost matheo]# ping 10.5.1.12
PING 10.5.1.12 (10.5.1.12) 56(84) bytes of data.
64 bytes from 10.5.1.12: icmp_seq=1 ttl=64 time=0.698 ms
64 bytes from 10.5.1.12: icmp_seq=2 ttl=64 time=0.434 ms
64 bytes from 10.5.1.12: icmp_seq=3 ttl=64 time=0.382 ms
64 bytes from 10.5.1.12: icmp_seq=4 ttl=64 time=0.446 ms
^C
--- 10.5.1.12 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3102ms
rtt min/avg/max/mdev = 0.382/0.490/0.698/0.122 ms
```
### Client1 vers routeur :
```powershell
matheo@matheo-VirtualBox:~$ ping 10.5.1.254
PING 10.5.1.254 (10.5.1.254) 56(84) bytes of data.
64 bytes from 10.5.1.254: icmp_seq=1 ttl=64 time=0.304 ms
64 bytes from 10.5.1.254: icmp_seq=2 ttl=64 time=0.384 ms
64 bytes from 10.5.1.254: icmp_seq=3 ttl=64 time=0.521 ms
64 bytes from 10.5.1.254: icmp_seq=4 ttl=64 time=0.434 ms
^C
--- 10.5.1.254 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3094ms
rtt min/avg/max/mdev = 0.304/0.410/0.521/0.078 ms
```
### Client2 vers routeur :
```powershell
matheo@matheo-VirtualBox:~$ ping 10.5.1.254
PING 10.5.1.254 (10.5.1.254) 56(84) bytes of data.
64 bytes from 10.5.1.254: icmp_seq=1 ttl=64 time=0.247 ms
64 bytes from 10.5.1.254: icmp_seq=2 ttl=64 time=0.312 ms
64 bytes from 10.5.1.254: icmp_seq=3 ttl=64 time=1.43 ms
64 bytes from 10.5.1.254: icmp_seq=4 ttl=64 time=0.313 ms
^C
--- 10.5.1.254 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3068ms
rtt min/avg/max/mdev = 0.247/0.574/1.425/0.491 ms
```
### Client1 vers Mon PC :
```powershell
[root@localhost matheo]# ping 10.5.1.11
PING 10.5.1.11 (10.5.1.11) 56(84) bytes of data.
64 bytes from 10.5.1.11: icmp_seq=1 ttl=64 time=0.934 ms
64 bytes from 10.5.1.11: icmp_seq=2 ttl=64 time=0.413 ms
64 bytes from 10.5.1.11: icmp_seq=3 ttl=64 time=0.449 ms
64 bytes from 10.5.1.11: icmp_seq=4 ttl=64 time=0.288 ms
^C
--- 10.5.1.11 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3066ms
rtt min/avg/max/mdev = 0.288/0.521/0.934/0.245 ms
```
### Mon PC vers routeur :
```powershell
PS C:\Users\mathe> ping 10.5.1.254

Envoi d’une requête 'Ping'  10.5.1.254 avec 32 octets de données :
Réponse de 10.5.1.254 : octets=32 temps<1ms TTL=64
Réponse de 10.5.1.254 : octets=32 temps<1ms TTL=64
Réponse de 10.5.1.254 : octets=32 temps<1ms TTL=64
Réponse de 10.5.1.254 : octets=32 temps<1ms TTL=64

Statistiques Ping pour 10.5.1.254:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms
```
## II. Accès internet pour tous
## ☀️ Prouvez que les clients ont un accès internet
```powershell
matheo@matheo-VirtualBox:~$ ping www.ynov.com
PING www.ynov.com (104.26.10.233) 56(84) bytes of data.
64 bytes from 104.26.10.233: icmp_seq=1 ttl=51 time=15.6 ms
64 bytes from 104.26.10.233: icmp_seq=2 ttl=51 time=15.3 ms
64 bytes from 104.26.10.233: icmp_seq=3 ttl=51 time=17.1 ms
64 bytes from 104.26.10.233: icmp_seq=4 ttl=51 time=14.7 ms
64 bytes from 104.26.10.233: icmp_seq=5 ttl=51 time=16.9 ms
^C
--- www.ynov.com ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4092ms
rtt min/avg/max/mdev = 14.748/15.912/17.132/0.928 ms
```
## ☀️ Montrez-moi le contenu final du fichier de configuration de l'interface réseau
```powershell
matheo@matheo-VirtualBox:~$ cat /etc/netplan/01-netcfg.yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s8:
      dhcp4: no
      addresses: [10.5.1.12/24]
      gateway4: 10.5.1.254
      nameservers:
        adresses: [1.1.1.1]
```
## III. Serveur SSH
