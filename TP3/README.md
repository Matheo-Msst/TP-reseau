# TP3 : 32°13'34"N 95°03'27"W :
## I. ARP basics
## ☀️ Avant de continuer...
```powershell
PS C:\Users\mathe> ipconfig /all

Carte réseau sans fil Wi-Fi :

   Suffixe DNS propre à la connexion. . . :
   Description. . . . . . . . . . . . . . : MediaTek Wi-Fi 6 MT7921 Wireless LAN Card
   Adresse physique . . . . . . . . . . . : 88-CE-43-20-FA-36
   DHCP activé. . . . . . . . . . . . . . : Oui
   Configuration automatique activée. . . : Oui
   Adresse IPv6 de liaison locale. . . . .: fe80::57c0:1edf:7116:7be7%18(préféré)
   Adresse IPv4. . . . . . . . . . . . . .: 10.33.69.1(préféré)
   Masque de sous-réseau. . . . . . . . . : 255.255.240.0
   Bail obtenu. . . . . . . . . . . . . . : jeudi 10 octobre 2024 09:12:26
   Bail expirant. . . . . . . . . . . . . : vendredi 11 octobre 2024 09:12:26
   Passerelle par défaut. . . . . . . . . : 10.33.79.254
   Serveur DHCP . . . . . . . . . . . . . : 10.33.79.254
   IAID DHCPv6 . . . . . . . . . . . : 126937192
   DUID de client DHCPv6. . . . . . . . : 00-01-00-01-2E-32-FB-CC-04-42-1A-A0-D9-9D
   Serveurs DNS. . .  . . . . . . . . . . : 8.8.8.8
                                       1.1.1.1
   NetBIOS sur Tcpip. . . . . . . . . . . : Activé
```
## ☀️ Affichez votre table ARP
```powershell
PS C:\Users\mathe> arp -a

Interface : 192.168.56.1 --- 0x8
  Adresse Internet      Adresse physique      Type
  192.168.56.255        ff-ff-ff-ff-ff-ff     statique
  224.0.0.2             01-00-5e-00-00-02     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  224.76.78.75          01-00-5e-4c-4e-4b     statique
  239.255.132.178       01-00-5e-7f-84-b2     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique

Interface : 169.254.248.113 --- 0x10
  Adresse Internet      Adresse physique      Type
  169.254.255.255       ff-ff-ff-ff-ff-ff     statique
  224.0.0.2             01-00-5e-00-00-02     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  224.76.78.75          01-00-5e-4c-4e-4b     statique
  239.255.132.178       01-00-5e-7f-84-b2     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique

Interface : 10.33.69.1 --- 0x12
  Adresse Internet      Adresse physique      Type
  10.33.64.180          8c-f8-c5-fc-8b-1d     dynamique
  10.33.65.2            10-63-c8-59-e5-af     dynamique
  10.33.65.8            34-7d-f6-5a-20-da     dynamique
  10.33.65.63           44-af-28-c3-6a-9f     dynamique
  10.33.65.156          9c-da-3e-76-6c-b3     dynamique
  10.33.67.165          60-e3-2b-ac-bf-89     dynamique
  10.33.67.222          b0-fc-36-52-84-9d     dynamique
  10.33.70.144          b0-68-e6-bc-ef-e3     dynamique
  10.33.72.53           54-8c-a0-18-46-ea     dynamique
  10.33.73.71           40-1a-58-3b-37-ec     dynamique
  10.33.73.75           70-d8-23-5e-1b-c2     dynamique
  10.33.73.77           98-8d-46-c4-fa-e5     dynamique
  10.33.73.98           38-7a-0e-c6-72-0d     dynamique
  10.33.74.153          48-e7-da-f0-f6-6d     dynamique
  10.33.77.125          20-0d-b0-cc-68-bb     dynamique
  10.33.77.160          c8-94-02-f8-ab-97     dynamique
  10.33.79.254          7c-5a-1c-d3-d8-76     dynamique
  10.33.79.255          ff-ff-ff-ff-ff-ff     statique
  224.0.0.2             01-00-5e-00-00-02     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  224.76.78.75          01-00-5e-4c-4e-4b     statique
  239.255.132.178       01-00-5e-7f-84-b2     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique
```
## ☀️ Déterminez l'adresse MAC de la passerelle du réseau de l'école
```powershell
PS C:\Users\mathe> arp -a

Interface : 10.33.69.1 --- 0x12
  Adresse Internet      Adresse physique      Type
  10.33.79.254          7c-5a-1c-d3-d8-76     dynamique
```
## ☀️ Supprimez la ligne qui concerne la passerelle
```powershell
PS C:\WINDOWS\system32> arp -d 10.33.79.254 
PS C:\WINDOWS\system32> arp -a 

Interface : 169.254.248.113 --- 0x10 
  Adresse Internet Adresse physique Type 
  169.254.255.255 ff-ff-ff-ff-ff-ff statique 
  224.0.0.22 01-00-5e-00-00-16 statique 
  224.0.0.251 01-00-5e-00-00-fb statique 
  224.0.0.252 01-00-5e-00-00-fc statique 
  239.255.255.250 01-00-5e-7f-ff-fa statique 
  255.255.255.255 ff-ff-ff-ff-ff-ff statique

Interface : 10.33.69.1 --- 0x12 
  Adresse Internet Adresse physique Type 
  10.33.79.254 7c-5a-1c-d3-d8-76 dynamique 
  10.33.79.255 ff-ff-ff-ff-ff-ff statique 
  224.0.0.22 01-00-5e-00-00-16 statique 
  224.0.0.251 01-00-5e-00-00-fb statique 
  224.0.0.252 01-00-5e-00-00-fc statique 
  239.255.255.250 01-00-5e-7f-ff-fa statique 
  255.255.255.255 ff-ff-ff-ff-ff-ff statique
```
## ☀️ Prouvez que vous avez supprimé la ligne dans la table ARP

```powershell 
PS C:\WINDOWS\system32> arp -d 10.33.79.254 
PS C:\WINDOWS\system32> arp -a

Interface : 169.254.63.157 --- 0x8 
  Adresse Internet Adresse physique Type 
  169.254.255.255 ff-ff-ff-ff-ff-ff statique 
  224.0.0.22 01-00-5e-00-00-16 statique 
  224.0.0.251 01-00-5e-00-00-fb statique 
  224.0.0.252 01-00-5e-00-00-fc statique 
  239.255.255.250 01-00-5e-7f-ff-fa statique 
  255.255.255.255 ff-ff-ff-ff-ff-ff statique
```
## ☀️ Wireshark
>####  -arp1.pcap

## II. ARP dans un réseau local
### 1. Basics
### ☀️ Déterminer
```powershell
Carte réseau sans fil Wi-Fi :

   Suffixe DNS propre à la connexion. . . :
   Description. . . . . . . . . . . . . . : MediaTek Wi-Fi 6 MT7921 Wireless LAN Card
   Adresse physique . . . . . . . . . . . : 90-E8-68-40-98-F7
   Adresse IPv4. . . . . . . . . . . . . .: 172.20.10.4(préféré)
   Masque de sous-réseau. . . . . . . . . : 255.255.255.240
   Passerelle par défaut. . . . . . . . . : 172.20.10.1
   Serveur DHCP . . . . . . . . . . . . . : 172.20.10.1
   Serveurs DNS. . .  . . . . . . . . . . : 172.20.10.1
```
### ☀️ DIY

```powershell 
PS C:\WINDOWS\system32> New-NetIPAddress -InterfaceAlias "Wi-Fi" -IPAddress 172.20.10.13 -PrefixLength 28 -DefaultGateway 172.20.10.1


IPAddress         : 172.20.10.13
InterfaceIndex    : 18
InterfaceAlias    : Wi-Fi
AddressFamily     : IPv4
Type              : Unicast
PrefixLength      : 28
PrefixOrigin      : Manual
SuffixOrigin      : Manual
AddressState      : Tentative
ValidLifetime     : Infinite ([TimeSpan]::MaxValue)
PreferredLifetime : Infinite ([TimeSpan]::MaxValue)
SkipAsSource      : False
PolicyStore       : ActiveStore
```
### ☀️ Pingz !

>### j'analyse mon réseaux pour connaître les adresses IP des machines ( j'ai mis deux téléphoone et mon ordi dessus chez moi):
```powershell 
PS C:\WINDOWS\system32> nmap 172.20.10.0/28
Starting Nmap 7.95 ( https://nmap.org ) at 2024-10-13 22:07 Paris, Madrid (heure dÆÚtÚ)
mass_dns: warning: Unable to determine any DNS servers. Reverse DNS is disabled. Try using --system-dns or specify valid servers with --dns-servers
Nmap scan report for 172.20.10.1
Host is up (0.031s latency).
Not shown: 996 closed tcp ports (reset)
PORT      STATE SERVICE
21/tcp    open  ftp
53/tcp    open  domain
49152/tcp open  unknown
62078/tcp open  iphone-sync
MAC Address: 3A:65:B2:8D:C0:64 (Unknown)

Nmap scan report for 172.20.10.4
Host is up (0.021s latency).
Not shown: 998 closed tcp ports (reset)
PORT      STATE SERVICE
49152/tcp open  unknown
62078/tcp open  iphone-sync
MAC Address: 76:62:1F:3D:1C:03 (Unknown)

Nmap scan report for 172.20.10.6
Host is up (0.020s latency).
Not shown: 999 closed tcp ports (reset)
PORT     STATE    SERVICE
5060/tcp filtered sip
MAC Address: BC:7F:A4:07:C5:CF (Xiaomi Communications)

Nmap scan report for 172.20.10.13
Host is up (0.00014s latency).
Not shown: 995 closed tcp ports (reset)
PORT     STATE SERVICE
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
808/tcp  open  ccproxy-http
9001/tcp open  tor-orport

Nmap done: 16 IP addresses (4 hosts up) scanned in 9.37 seconds
```
>### je ping chaque machine et je met les resultats dans wireshark : **"ping.pcap"**
```powershell 
Statistiques Ping pour 172.20.10.4:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 39ms, Maximum = 252ms, Moyenne = 131ms

PS C:\WINDOWS\system32> ping 172.20.10.6

Envoi d’une requête 'Ping'  172.20.10.6 avec 32 octets de données :
Réponse de 172.20.10.6 : octets=32 temps=109 ms TTL=64
Réponse de 172.20.10.6 : octets=32 temps=274 ms TTL=64
Réponse de 172.20.10.6 : octets=32 temps=42 ms TTL=64
Réponse de 172.20.10.6 : octets=32 temps=50 ms TTL=64

Statistiques Ping pour 172.20.10.6:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 42ms, Maximum = 274ms, Moyenne = 118ms`

PS C:\WINDOWS\system32> ping youtube.com

Envoi d’une requête 'ping' sur youtube.com [2a00:1450:4007:818::200e] avec 32 octets de données :
Réponse de 2a00:1450:4007:818::200e : temps=74 ms
Réponse de 2a00:1450:4007:818::200e : temps=46 ms
Réponse de 2a00:1450:4007:818::200e : temps=36 ms
Réponse de 2a00:1450:4007:818::200e : temps=49 ms

Statistiques Ping pour 2a00:1450:4007:818::200e:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 36ms, Maximum = 74ms, Moyenne = 51ms
```
## 2. ARP
## ☀️ Affichez votre table ARP !
```powershell
PS C:\WINDOWS\system32> arp -a

Interface : 192.168.56.1 --- 0x8
  Adresse Internet      Adresse physique      Type
  192.168.56.255        ff-ff-ff-ff-ff-ff     statique
  224.0.0.2             01-00-5e-00-00-02     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique

Interface : 169.254.248.113 --- 0x10
  Adresse Internet      Adresse physique      Type
  169.254.255.255       ff-ff-ff-ff-ff-ff     statique
  224.0.0.2             01-00-5e-00-00-02     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique

Interface : 172.20.10.13 --- 0x12
  Adresse Internet      Adresse physique      Type
  172.20.10.1           3a-65-b2-8d-c0-64     dynamique
  172.20.10.4           76-62-1f-3d-1c-03     dynamique
  172.20.10.6           bc-7f-a4-07-c5-cf     dynamique
  172.20.10.15          ff-ff-ff-ff-ff-ff     statique
  224.0.0.2             01-00-5e-00-00-02     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
```
>### Le message qui doit etre affiché avant les ping dans wireshark est "Who has ? + ensuite l'adresse IP" mais avec mon réseaux de télépones connectés à mon partage de connexion je n'ai pas réussi à les ping sans qu'ils soient directement remis dans la table ARP