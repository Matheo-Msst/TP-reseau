# TP6 : Des bo services dans des bo LANs
## I. Le setup
### 2. Marche à suivre
## ☀️ ️ Prouvez que ...
### - une machine du LAN1 peut joindre internet :
```powershell
matheo@client1:~$ ping google.com
PING google.com (142.251.37.46) 56(84) bytes of data.
64 bytes from mrs09s13-in-f14.1e100.net (142.251.37.46): icmp_seq=1 ttl=112 time=24.4 ms
64 bytes from mrs09s13-in-f14.1e100.net (142.251.37.46): icmp_seq=2 ttl=112 time=23.9 ms
64 bytes from mrs09s13-in-f14.1e100.net (142.251.37.46): icmp_seq=3 ttl=112 time=18.5 ms
^C
--- google.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 18.454/22.248/24.394/2.690 ms
```
### - une machine du LAN2 peut joindre internet :
```powershell
[root@web matheo]# ping ynov.com
PING ynov.com (104.26.10.233) 56(84) bytes of data.
64 bytes from 104.26.10.233 (104.26.10.233): icmp_seq=1 ttl=53 time=20.0 ms
64 bytes from 104.26.10.233 (104.26.10.233): icmp_seq=2 ttl=53 time=19.4 ms
64 bytes from 104.26.10.233 (104.26.10.233): icmp_seq=3 ttl=53 time=18.3 ms
^C
--- ynov.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 18.290/19.205/19.969/0.693 ms
```
### - une machine du LAN1 peut joindre une machine du LAN2 :
```powershell
[root@dhcd matheo]# ping 10.6.2.12
PING 10.6.2.12 (10.6.2.12) 56(84) bytes of data.
64 bytes from 10.6.2.12: icmp_seq=1 ttl=63 time=0.621 ms
64 bytes from 10.6.2.12: icmp_seq=2 ttl=63 time=0.730 ms
64 bytes from 10.6.2.12: icmp_seq=3 ttl=63 time=0.666 ms
^C
--- 10.6.2.12 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2029ms
rtt min/avg/max/mdev = 0.621/0.672/0.730/0.044 ms
```
## II. LAN clients
### *1. Serveur DHCP*
### 2. Client
## ☀️ ️ Prouvez que ...
```powershell
matheo@client1:~$ ip a
2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:1b:19:19 brd ff:ff:ff:ff:ff:ff
    inet 10.6.1.37/24 brd 10.6.1.255 scope global dynamic noprefixroute enp0s8
       valid_lft 40590sec preferred_lft 40590sec
    inet6 fe80::a00:27ff:fe1b:1919/64 scope link
       valid_lft forever preferred_lft forever
```
```powershell
matheo@client1:~$ resolvectl
Global
         Protocols: -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
  resolv.conf mode: stub

Link 2 (enp0s8)
    Current Scopes: DNS
         Protocols: +DefaultRoute -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
Current DNS Server: 1.1.1.1
       DNS Servers: 1.1.1.1
```
```powershell
matheo@client1:~$ ip r s
default via 10.6.1.254 dev enp0s8 proto dhcp src 10.6.1.37 metric 100
10.6.1.0/24 dev enp0s8 proto kernel scope link src 10.6.1.37 metric 100
```
```powershell
matheo@client1:~$ ping youtube.com
PING youtube.com (216.58.205.206) 56(84) bytes of data.
64 bytes from mrs09s09-in-f14.1e100.net (216.58.205.206): icmp_seq=1 ttl=112 time=17.9 ms
64 bytes from mrs09s09-in-f14.1e100.net (216.58.205.206): icmp_seq=2 ttl=112 time=22.6 ms
64 bytes from mrs09s09-in-f14.1e100.net (216.58.205.206): icmp_seq=3 ttl=112 time=19.3 ms
^C
--- youtube.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 17.945/19.944/22.628/1.972 ms
```
## III. LAN serveurzzzz
### 1. Serveur Web
### 2. Install this shiet
### 3. Analyse et test
## ☀️ Déterminer sur quel port écoute le serveur NGINX
```powershell 
[root@web matheo]# ss -lnpt
State                 Recv-Q                Send-Q                                 Local Address:Port                                 Peer Address:Port                Process
LISTEN                0                     128                                          0.0.0.0:22                                        0.0.0.0:*                    users:(("sshd",pid=697,fd=3))
LISTEN                0                     511                                          0.0.0.0:80                                        0.0.0.0:*                    users:(("nginx",pid=766,fd=6),("nginx",pid=765,fd=6))
LISTEN                0                     128                                             [::]:22                                           [::]:*                    users:(("sshd",pid=697,fd=4))
LISTEN                0                     511                                             [::]:80                                           [::]:*                    users:(("nginx",pid=766,fd=7),("nginx",pid=765,fd=7))
```
```powershell
[root@web matheo]# ss -lnpt | grep 80
LISTEN 0      511          0.0.0.0:80        0.0.0.0:*    users:(("nginx",pid=766,fd=6),("nginx",pid=765,fd=6))
LISTEN 0      511             [::]:80           [::]:*    users:(("nginx",pid=766,fd=7),("nginx",pid=765,fd=7))
```
## ☀️ Ouvrir ce port dans le firewall
```powershell
[root@web matheo]# firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s8
  sources:
  services: http ssh
  ports: 80/tcp
```
## ☀️ Visitez le site web !
```powershell
matheo@client1:~$ curl http://10.6.2.11
<!doctype html>
<html>
  <head>
    <meta charset='utf-8'>
    <meta name='viewport' content='width=device-width, initial-scale=1'>
    <title>HTTP Server Test Page powered by: Rocky Linux</title>
    <style type="text/css">
      /*<![CDATA[*/
```
### *2. Serveur DNS*
### 1. Présentation serveur DNS
### 2. Dans notre TP
### 3. Zé bardi
### 4. Analyse du service
## ☀️ Déterminer sur quel(s) port(s) écoute le service BIND9
```powershell 
[root@dns matheo]# sudo ss -lnpt | grep 53
LISTEN 0      10         127.0.0.1:53        0.0.0.0:*    users:(("named",pid=1912,fd=22))
LISTEN 0      10         10.6.2.12:53        0.0.0.0:*    users:(("named",pid=1912,fd=25))
LISTEN 0      4096       127.0.0.1:953       0.0.0.0:*    users:(("named",pid=1912,fd=28))
LISTEN 0      4096           [::1]:953          [::]:*    users:(("named",pid=1912,fd=29))
LISTEN 0      10             [::1]:53           [::]:*    users:(("named",pid=1912,fd=27))
```
## ☀️ Ouvrir ce(s) port(s) dans le firewall
```powershell
[root@dns matheo]# sudo firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s8
  sources:
  services: cockpit dhcpv6-client ssh
  ports: 53/tcp 53/udp
```
### 5. Tests manuels
## ☀️ Effectuez des requêtes DNS manuellement depuis le serveur DNS lui-même dans un premier temps
```powershell
[root@dns matheo]# dig web.tp6.b1 @10.6.2.12
;; QUESTION SECTION:
;web.tp6.b1.                    IN      A

;; ANSWER SECTION:
web.tp6.b1.             86400   IN      A       10.6.2.11
```
```powershell
[root@dns matheo]# dig dns.tp6.b1 @10.6.2.12
;; QUESTION SECTION:
;dns.tp6.b1.                    IN      A

;; ANSWER SECTION:
dns.tp6.b1.             86400   IN      A       10.6.2.12
```
```powershell
[root@dns matheo]# dig ynov.com @10.6.2.12
;; QUESTION SECTION:
;ynov.com.                      IN      A

;; ANSWER SECTION:
ynov.com.               300     IN      A       104.26.10.233
ynov.com.               300     IN      A       172.67.74.226
ynov.com.               300     IN      A       104.26.11.233
```
```powershell
[root@dns matheo]# dig -x 10.6.2.11 @10.6.2.12
;; QUESTION SECTION:
;11.2.6.10.in-addr.arpa.                IN      PTR

;; ANSWER SECTION:
11.2.6.10.in-addr.arpa. 86400   IN      PTR     web.tp6.b1.
```
```powershell
[root@dns matheo]# dig -x 10.6.2.12 @10.6.2.12
;; QUESTION SECTION:
;12.2.6.10.in-addr.arpa.                IN      PTR

;; ANSWER SECTION:
12.2.6.10.in-addr.arpa. 86400   IN      PTR     dns.tp6.b1.
```
## ☀️ Effectuez une requête DNS manuellement depuis client1.tp6.b1
```powershell
[root@dns matheo]# dig web.tp6.b1 @10.6.2.12
;; QUESTION SECTION:
;web.tp6.b1.                    IN      A

;; ANSWER SECTION:
web.tp6.b1.             86400   IN      A       10.6.2.11
```
## ☀️ Capturez une requête DNS et la réponse de votre serveur
### 3. Serveur DHCP
#### - récupérez une IP en DHCP sur ce nouveau client2.tp6.b1
```powershell
matheo@client2:~$ ip a
2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:93:ad:7e brd ff:ff:ff:ff:ff:ff
    inet 10.6.1.39/24 brd 10.6.1.255 scope global dynamic noprefixroute enp0s8
       valid_lft 42496sec preferred_lft 42496sec
    inet6 fe80::a00:27ff:fe93:ad7e/64 scope link
       valid_lft forever preferred_lft forever
```
#### - vérifiez que vous avez bien 10.6.2.12 comme serveur DNS à contacter
```powershell
matheo@client2:~$ resolvectl
Global
         Protocols: -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
  resolv.conf mode: stub

Link 2 (enp0s8)
    Current Scopes: DNS
         Protocols: +DefaultRoute -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
Current DNS Server: 10.6.2.12
       DNS Servers: 10.6.2.12
```