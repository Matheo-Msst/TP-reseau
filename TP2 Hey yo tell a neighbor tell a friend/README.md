# TP2 : Hey yo tell a neighbor tell a friend :
## I. Simplest LAN 
### **0. Setup** 
>Configurez vos adresses IP
```powershell
PS C:\WINDOWS\system32> New-NetIPAddress -InterfaceAlias "Ethernet" -IPAddress 10.10.13.20 -PrefixLength 24


IPAddress         : 10.10.13.20
InterfaceIndex    : 22
InterfaceAlias    : Ethernet
AddressFamily     : IPv4
Type              : Unicast
PrefixLength      : 24
PrefixOrigin      : Manual
SuffixOrigin      : Manual
AddressState      : Tentative
ValidLifetime     : Infinite ([TimeSpan]::MaxValue)
PreferredLifetime : Infinite ([TimeSpan]::MaxValue)
SkipAsSource      : False
PolicyStore       : ActiveStore
```

### **1. Quelques pings**
## 🌞 Prouvez que votre configuration est effective
```powershell
PS C:\WINDOWS\system32> Get-NetIPAddress -InterfaceAlias "Ethernet"


IPAddress         : 10.10.13.20
InterfaceIndex    : 22
InterfaceAlias    : Ethernet
AddressFamily     : IPv4
Type              : Unicast
PrefixLength      : 24
PrefixOrigin      : Manual
SuffixOrigin      : Manual
AddressState      : Preferred
ValidLifetime     : Infinite ([TimeSpan]::MaxValue)
PreferredLifetime : Infinite ([TimeSpan]::MaxValue)
SkipAsSource      : False
PolicyStore       : ActiveStore
```
## 🌞 Tester que votre LAN + votre adressage IP est fonctionnel
## 🌞 Capture de ping
> Dans le fichier "ping.pcapng"
## II. Utilisation des ports
### **0. Intro blabla**
### **1. Animal numérique**
## 🌞 Sur le PC serveur
```powersell
PS C:\Users\mathe\Downloads\netcat-win32-1.11\netcat-1.11> ./nc.exe -l -p 1234
```
## 🌞 Sur le PC client
```powershell
PS C:\Users\mathe\Downloads\netcat-win32-1.11\netcat-1.11> ./nc.exe 10.10.13.20 1234
```
## 🌞 Echangez-vous des messages
```powershell
PS C:\Users\mathe\Downloads\netcat-win32-1.11\netcat-1.11> ./nc.exe -l -p 1234
yo
quoi

feur
ça marche
```
## 🌞 Utilisez une commande qui permet de voir la connexion en cours
```powershell
PS C:\WINDOWS\system32> netstat -a -b -n

 TCP    10.10.13.20:1234       10.10.13.15:39962      ESTABLISHED
 [nc.exe]
 ```

#🌞 Inversez les rôles
 ## 🌞 Sur le PC serveur
```powersell
PS C:\Users\mathe\Downloads\netcat-win32-1.11\netcat-1.11> ./nc.exe -l -p 1234
```
## 🌞 Sur le PC client
```powershell
PS C:\Users\mathe\Downloads\netcat-win32-1.11\netcat-1.11> ./nc.exe 10.10.13.15 1234
```
```powershell
PS C:\Users\mathe\Downloads\netcat-win32-1.11\netcat-1.11> ./nc.exe 10.10.13.15 1234
salut
je suis ton pere
BYBEYEBYEBEYBE
```
## III. Analyse de vos applications usuelles
### **1. Serveur web**
> Dans le fichier "http.pcap"
### **2. Autres services**
## - Service 1 (spotify) 
```powershell
netstat -a -b -n 

TCP    192.168.1.144:15479    192.168.1.175:8009     ESTABLISHED
[Spotify.exe]
```
|Adresse Ip :   |192.168.1.175 |
|:-------------:|:------------:|
|**Port** **:** |**8009**      |

> Dans le fichier "service1.pcap"

## - Service 2 (Valorant "jeux")
```powershell
netstat -a -b -n 

TCP    192.168.1.144:15856    172.65.252.238:5223    ESTABLISHED
[RiotClientServices.exe]
```
|Adresse Ip :   |172.65.252.238 |
|:-------------:|:-------------:|
|**Port** **:** |**5223**       |

> Dans le fichier "service2.pcap"

## - Service 3 (Opéra GX "navigateur")
```powershell
netstat -a -b -n 

TCP    192.168.1.144:22504    192.168.1.175:8009     ESTABLISHED
[opera.exe]
```
|Adresse Ip :   |192.168.1.175  |
|:-------------:|:-------------:|
|**Port** **:** |**8009**       |

> Dans le fichier "service3.pcap"

## - Service 4 (teams)
```powershell
netstat -a -b -n 

TCP    192.168.1.144:30223    52.123.200.60:443      ESTABLISHED
[ms-teams.exe]
```
|Adresse Ip :   |52.123.200.60  |
|:-------------:|:-------------:|
|**Port** **:** |**443**        |

> Dans le fichier "service4.pcap"

## - Service 5 (Phasmophobia "jeux")
```powershell
netstat -a -b -n 

TCP    192.168.1.144:30487    34.102.143.233:443     ESTABLISHED
[Phasmophobia.exe]
```
|Adresse Ip :   |34.102.143.233 |
|:-------------:|:-------------:|
|**Port** **:** |**443**        |

> Dans le fichier "service5.pcap"