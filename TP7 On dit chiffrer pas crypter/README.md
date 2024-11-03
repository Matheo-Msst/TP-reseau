# TP7 : On dit chiffrer pas crypter
## I. Le setup
## II. Serveur Web
## 1. HTTP
### B. Configuration

## 🌞 Lister les ports en écoute sur la machine
```powershell 
[root@web matheo]# ss -lnpt
State  Recv-Q Send-Q Local Address:Port   Peer Address:Port Process
LISTEN 0      128          0.0.0.0:22          0.0.0.0:*     users:(("sshd",pid=693,fd=3))
LISTEN 0      511          0.0.0.0:80          0.0.0.0:*     users:(("nginx",pid=1439,fd=6),("nginx",pid=1438,fd=6))
LISTEN 0      128             [::]:22             [::]:*     users:(("sshd",pid=693,fd=4))
LISTEN 0      511             [::]:80             [::]:*     users:(("nginx",pid=1439,fd=7),("nginx",pid=1438,fd=7))
```
```powershell
[root@web matheo]# ss -lnpt | grep 80
LISTEN 0      511          0.0.0.0:80        0.0.0.0:*    users:(("nginx",pid=1439,fd=6),("nginx",pid=1438,fd=6))
LISTEN 0      511             [::]:80           [::]:*    users:(("nginx",pid=1439,fd=7),("nginx",pid=1438,fd=7))
```
## 🌞 Ouvrir le port dans le firewall de la machine
```powershell
[root@web matheo]# sudo firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s8
  sources:
  services: ssh
  ports: 80/tcp
  protocols:
  forward: yes
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
```
### C. Tests client
## 🌞 Vérifier que ça a pris effet
```powershell 
matheo@client1:~$ ping sitedefou.tp7.b1
PING sitedefou.tp7.b1 (10.7.1.11) 56(84) bytes of data.
64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=1 ttl=64 time=0.389 ms
64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=2 ttl=64 time=0.465 ms
64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=3 ttl=64 time=0.405 ms
^C
--- sitedefou.tp7.b1 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2036ms
rtt min/avg/max/mdev = 0.389/0.419/0.465/0.032 ms
```
```powershell
matheo@client1:~$ curl http://sitedefou.tp7.b1
meow !
```
### D. Analyze
## 🌞 Capture tcp_http.pcap
```powershell
matheo@client1:~$ sudo tcpdump -w tcp_http.pcap -i enp0s8
```
>fichier : ```tcp_http.pcap```
## 🌞 Voir la connexion établie
```powershell
matheo@client1:~$ sudo ss -npt
State              Recv-Q              Send-Q                                 Local Address:Port                                 Peer Address:Port              Process
ESTAB              0                   0                                         10.7.1.101:44990                                   10.7.1.11:80                 users:(("firefox",pid=6671,fd=64))
ESTAB              0                   0                                         10.7.1.101:56154                               34.107.243.93:443                users:(("firefox",pid=6671,fd=138))
ESTAB              36                  0                                [::ffff:10.7.1.101]:22                              [::ffff:10.7.1.1]:31571              users:(("sshd",pid=3915,fd=4),("sshd",pid=3770,fd=4))
```
## 2. On rajoute un S
### A. Config
## 🌞 Lister les ports en écoute sur la machine
```powershell
[root@web ~]# sudo ss -lnpt | grep 443
LISTEN 0      511        10.7.1.11:443       0.0.0.0:*    users:(("nginx",pid=1340,fd=6),("nginx",pid=1339,fd=6))
```
## 🌞 Gérer le firewall
```powershell
[root@web ~]# sudo firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s8
  sources:
  services: ssh
  ports: 443/tcp
  protocols:
  forward: yes
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
```
### B. Test test test analyyyze
## 🌞 Capture tcp_https.pcap
```powershell
matheo@client1:~$ sudo tcpdump -w tcp_https.pcap -i enp0s8
```
>fichier : ```tcp_https.pcap```

## III. Serveur VPN
## 1. Install et conf Wireguard
## 🌞 Prouvez que vous avez bien une nouvelle carte réseau wg0
```powershell 
[root@vpn matheo]# ip a
4: wg0: <POINTOPOINT,NOARP,UP,LOWER_UP> mtu 1420 qdisc noqueue state UNKNOWN group default qlen 1000
    link/none
    inet 10.7.200.1/24 scope global wg0
       valid_lft forever preferred_lft forever
```
## 🌞 Déterminer sur quel port écoute Wireguard
```powershell
[root@vpn matheo]# ss -lnpu | grep 51820
UNCONN 0      0            0.0.0.0:51820      0.0.0.0:*
UNCONN 0      0               [::]:51820         [::]:*
```
## 🌞 Ouvrez ce port dans le firewall
```powershell 
[root@vpn matheo]# sudo firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s8 enp0s9
  sources:
  services: cockpit dhcpv6-client ssh
  ports: 51820/udp
  protocols:
  forward: yes
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
```
## 2. Ajout d'un client VPN
## 3. Proofs
## 🌞 Ping ping ping !
```powershell
root@client1:/home/matheo# ping 10.7.200.1
PING 10.7.200.1 (10.7.200.1) 56(84) bytes of data.
64 bytes from 10.7.200.1: icmp_seq=1 ttl=64 time=0.601 ms
64 bytes from 10.7.200.1: icmp_seq=2 ttl=64 time=0.618 ms
64 bytes from 10.7.200.1: icmp_seq=3 ttl=64 time=1.61 ms
^C
--- 10.7.200.1 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2050ms
rtt min/avg/max/mdev = 0.601/0.941/1.606/0.469 ms
```
## 🌞 Capture ping1_vpn.pcap
```powershell
matheo@client1:~$ sudo tcpdump -w ping1_vpn.pcap -i enp0s8
```
>fichier : ```ping1_vpn.pcap```
## 🌞 Capture ping2_vpn.pcap
```powershell
matheo@client1:~$ sudo tcpdump -w ping2_vpn.pcap -i enp0s8
```
>fichier : ```ping2_vpn.pcap```
## 🌞 Prouvez que vous avez toujours un accès internet
```powershell
root@client1:/home/matheo# ip route
default via 10.7.200.1 dev wg0
10.7.1.0/24 dev enp0s8 proto kernel scope link src 10.7.1.101 metric 100
10.7.200.0/24 dev wg0 proto kernel scope link src 10.7.200.11

```
```powershell
root@client1:/home/matheo# ping ynov.com
PING ynov.com (104.26.11.233) 56(84) bytes of data.
64 bytes from 104.26.11.233: icmp_seq=1 ttl=52 time=17.5 ms
64 bytes from 104.26.11.233: icmp_seq=2 ttl=52 time=17.6 ms
64 bytes from 104.26.11.233: icmp_seq=3 ttl=52 time=95.6 ms
^C
--- ynov.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 17.501/43.569/95.646/36.823 ms
```
## 4. Private service
## 🌞 Visitez le service Web à travers le VPN