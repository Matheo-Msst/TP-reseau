# TP7 : On dit chiffrer pas crypter
## I. Le setup
## II. Serveur Web
### 0. Setup
## 1. HTTP
### A. Install
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
matheo@client1:~$ sudo tcpdump -w tcp_http2.pcap -i enp0s8
```
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