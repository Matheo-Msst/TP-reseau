# TP1 : Les premiers pas de bébé B1
### 🌞 Adresses IP de ta machine : 
## **- Carte réseau sans fil de ma machine:** 
```powershell 
PS C:\Users\mathe> ipconfig

Configuration IP de Windows

Carte réseau sans fil Wi-Fi :

   Suffixe DNS propre à la connexion. . . :
   Adresse IPv6 de liaison locale. . . . .: fe80::4e85:67fa:c4c7:ec7d%17
   Adresse IPv4. . . . . . . . . . . . . .: 10.33.77.179
   Masque de sous-réseau. . . . . . . . . : 255.255.240.0
   Passerelle par défaut. . . . . . . . . : 10.33.79.254
```
## **- Carte Ethernet de ma machine:** 
```powershell 
PS C:\Users\mathe> ipconfig

Configuration IP de Windows

Carte Ethernet Ethernet :

   Statut du média. . . . . . . . . . . . : Média déconnecté
   Suffixe DNS propre à la connexion. . . :
```
>#### Je n'ai pas d'adresse IP pour l'Ethernet car je n'ai pas de câble dessus
### 🌞 Si t'as un accès internet normal, d'autres infos sont forcément dispos...
## **- Adresse IP de la passerelle, DNS et DHCP du réseau local**
```powershell
PS C:\Users\mathe> ipconfig /all

Configuration IP de Windows

Carte réseau sans fil Wi-Fi :

    Adresse IPv4. . . . . . . . . . . . . .: 10.33.77.179
    Masque de sous-réseau. . . . . . . . . : 255.255.240.0
    Passerelle par défaut. . . . . . . . . : 10.33.79.254
    Serveur DHCP . . . . . . . . . . . . . : 10.33.79.254
    Serveurs DNS. . .  . . . . . . . . . . : 8.8.8.8
                                             1.1.1.1
```

### 🌟 BONUS : Détermine s'il y a un pare-feu actif sur ta machine
```powershell
PS C:\WINDOWS\system32> Get-NetFirewallProfile | ft Name,Enabled

Name    Enabled
----    -------
Domain     True
Private    True
Public     True
```

```powershell
PS C:\WINDOWS\system32> Get-NetFirewallRule

Name                          : {23793C97-36C4-494D-8CB9-99997C9B272E}
DisplayName                   : TUF Aura Core
Description                   : TUF Aura Core
DisplayGroup                  : TUF Aura Core
Group                         : TUF Aura Core
Enabled                       : True
Profile                       : Domain, Private, Public
Platform                      : {6.2+}
Direction                     : Outbound
Action                        : Allow
EdgeTraversalPolicy           : Block
LooseSourceMapping            : False
LocalOnlyMapping              : False
Owner                         : S-1-5-21-729681103-3198086912-2845233188-1001
PrimaryStatus                 : OK
Status                        : La règle a été analysée à partir de la banque. (65536)
EnforcementStatus             : NotApplicable
PolicyStoreSource             : PersistentStore
PolicyStoreSourceType         : Local
RemoteDynamicKeywordAddresses :
PolicyAppId                   :
```
### 🌞 Envoie un ping vers...
## **- Moi-même !**
```powershell 
PS C:\WINDOWS\system32> ping 10.33.77.179

Envoi d’une requête 'Ping'  10.33.77.179 avec 32 octets de données :
Réponse de 10.33.77.179 : octets=32 temps<1ms TTL=128
Réponse de 10.33.77.179 : octets=32 temps<1ms TTL=128
Réponse de 10.33.77.179 : octets=32 temps<1ms TTL=128
Réponse de 10.33.77.179 : octets=32 temps<1ms TTL=128

Statistiques Ping pour 10.33.77.179:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms
```
## **- Vers l'adresse IP ```127.0.0.1```***
```powershell
PS C:\WINDOWS\system32> ping 127.0.0.1

Envoi d’une requête 'Ping'  127.0.0.1 avec 32 octets de données :
Réponse de 127.0.0.1 : octets=32 temps<1ms TTL=128
Réponse de 127.0.0.1 : octets=32 temps<1ms TTL=128
Réponse de 127.0.0.1 : octets=32 temps<1ms TTL=128
Réponse de 127.0.0.1 : octets=32 temps<1ms TTL=128

Statistiques Ping pour 127.0.0.1:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms
```
### 🌞 On continue avec ping. Envoie un ping vers...
## **- La passerelle***
```powershell
PS C:\WINDOWS\system32> ping 10.33.79.254

Envoi d’une requête 'Ping'  10.33.79.254 avec 32 octets de données :
Délai d’attente de la demande dépassé.
```
## **- Un(e) pote sur le réseau ```10.33.77.147```**
```powershell 
PS C:\WINDOWS\system32> ping 10.33.77.147

Envoi d’une requête 'Ping'  10.33.77.147 avec 32 octets de données :
Réponse de 10.33.77.147 : octets=32 temps=9 ms TTL=128
Réponse de 10.33.77.147 : octets=32 temps=10 ms TTL=128
Réponse de 10.33.77.147 : octets=32 temps=6 ms TTL=128
Réponse de 10.33.77.147 : octets=32 temps=7 ms TTL=128

Statistiques Ping pour 10.33.77.147:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 6ms, Maximum = 10ms, Moyenne = 8ms
```
## **- Un site internet ```www.youtube.com```**
```powershell
PS C:\WINDOWS\system32> ping www.youtube.com

Envoi d’une requête 'ping' sur youtube-ui.l.google.com [142.250.179.110] avec 32 octets de données :
Réponse de 142.250.179.110 : octets=32 temps=19 ms TTL=117
Réponse de 142.250.179.110 : octets=32 temps=18 ms TTL=117
Réponse de 142.250.179.110 : octets=32 temps=17 ms TTL=117
Réponse de 142.250.179.110 : octets=32 temps=18 ms TTL=117

Statistiques Ping pour 142.250.179.110:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 17ms, Maximum = 19ms, Moyenne = 18ms
```
### 🌞 Faire une requête DNS à la main
```powershell
nslookup www.youtube.com
Serveur :   dns.google
Address:  8.8.8.8

Réponse ne faisant pas autorité :
Nom :    youtube-ui.l.google.com
Addresses:  2a00:1450:4007:80c::200e
          2a00:1450:4007:80d::200e
          2a00:1450:4007:80e::200e
          2a00:1450:4007:810::200e
          142.250.201.174
          216.58.215.46
          142.250.75.238
          142.250.179.78
          172.217.20.174
          142.250.178.142
          172.217.20.206
          142.250.179.110
          216.58.214.174
Aliases:  www.youtube.com
```
### 🌞 J'attends dans le dépôt git de rendu un fichier ping.pcap
>#### Dans le dossier ```ping.pcap```

### 🌞 Livrez un deuxième fichier : dns.pcap
>#### Dans le dossier ```dns.pcap```

### 🌞 Effectue un scan du réseau auquel tu es connecté
>#### 10.33.64.0 est l'adresse réseau 
```powershell
PS C:\Users\mathe> nmap.exe -sn -PR  10.33.64.0/20

Nmap scan report for 10.33.69.208
Host is up (0.016s latency).
MAC Address: 30:89:4A:0D:DA:8B (Intel Corporate)
Nmap scan report for 10.33.69.232
Host is up (0.10s latency).
MAC Address: 3C:06:30:3B:B5:3C (Apple)
Nmap scan report for 10.33.70.41
Host is up (0.43s latency).
MAC Address: CE:71:C6:DF:63:76 (Unknown)
Nmap scan report for 10.33.70.42
Host is up (0.0060s latency).
MAC Address: 9C:FC:E8:42:F1:7B (Intel Corporate)
```

> #### j'en déduis que la 10.33.69.210 n'est pas prise je vais donc prendre celle la pour la suite

```powershell
PS C:\Users\mathe> Get-NetAdapter

Name                      InterfaceDescription                    ifIndex Status       MacAddress          LinkSpeed
----                      --------------------                    ------- ------       ----------          ---------
Wi-Fi                     MediaTek Wi-Fi 6 MT7921 Wireless 
```

```powershell
PS C:\Users\mathe> New-NetIPAddress -InterfaceAlias Wi-Fi -IPAddress 10.33.69.210 -PrefixLength 20 -DefaultGateway 10.33.79.254
>>


IPAddress         : 10.33.69.210
InterfaceIndex    : 17
InterfaceAlias    : Wi-Fi
AddressFamily     : IPv4
Type              : Unicast
PrefixLength      : 20
PrefixOrigin      : Manual
SuffixOrigin      : Manual
AddressState      : Tentative
ValidLifetime     : Infinite ([TimeSpan]::MaxValue)
PreferredLifetime : Infinite ([TimeSpan]::MaxValue)
SkipAsSource      : False
PolicyStore       : ActiveStore
```

```powershell
PS C:\Users\mathe> ipconfig

Configuration IP de Windows

Carte réseau sans fil Wi-Fi :

   Adresse IPv4. . . . . . . . . . . . . .: 10.33.69.210
   Masque de sous-réseau. . . . . . . . . : 255.255.240.0
   Passerelle par défaut. . . . . . . . . : 10.33.79.254
```
> #### L'IPV4 à donc bien été changer.