# TP3 : 32°13'34"N 95°03'27"W :
## I. ARP basics
## ☀️ Avant de continuer...
```powershell
PS C:\Users\mathe> ipconfig /all

Carte réseau sans fil Wi-Fi :

   Suffixe DNS propre à la connexion. . . : lan
   Description. . . . . . . . . . . . . . : MediaTek Wi-Fi 6 MT7921 Wireless LAN Card
   Adresse physique . . . . . . . . . . . : 90-E8-68-40-98-F7
   DHCP activé. . . . . . . . . . . . . . : Oui
   Configuration automatique activée. . . : Oui
   Adresse IPv4. . . . . . . . . . . . . .: 192.168.1.144(préféré)
   Masque de sous-réseau. . . . . . . . . : 255.255.255.0
   Passerelle par défaut. . . . . . . . . : fe80::56c4:5bff:fe4b:362c%17
                                       192.168.1.254
   Serveur DHCP . . . . . . . . . . . . . : 192.168.1.254
```
## ☀️ Affichez votre table ARP
```powershell
PS C:\Users\mathe> arp -a

Interface : 169.254.22.221 --- 0xf
  Adresse Internet      Adresse physique      Type
  169.254.255.255       ff-ff-ff-ff-ff-ff     statique
  224.0.0.2             01-00-5e-00-00-02     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique

Interface : 192.168.1.144 --- 0x11
  Adresse Internet      Adresse physique      Type
  192.168.1.175         ec-6c-9a-f8-ff-be     dynamique
  192.168.1.254         54-c4-5b-4b-36-2c     dynamique
  192.168.1.255         ff-ff-ff-ff-ff-ff     statique
  224.0.0.2             01-00-5e-00-00-02     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique

Interface : 192.168.56.1 --- 0x17
  Adresse Internet      Adresse physique      Type
  192.168.56.255        ff-ff-ff-ff-ff-ff     statique
  224.0.0.2             01-00-5e-00-00-02     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
```