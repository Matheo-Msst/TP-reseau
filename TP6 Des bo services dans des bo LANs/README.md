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
### 1. Serveur DHCP
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
## 
