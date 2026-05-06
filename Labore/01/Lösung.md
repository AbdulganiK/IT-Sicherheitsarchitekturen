# Lösung des ersten Labors

## Aufgabe 1

_Nennen Sie Maßnahmen, wie man es einem potenziellen Angreifer schwerer machen kann,_  
_das Passwort zu erraten._

Maßnahmen zum schützen eines Passwortes wären:

*   Eine lange Passwort länge wählen
*   Passphrases nutzen und dabei den ersten Buchstaben des wortes Wählen
*   Möglichst verschiedene Kombination an Zeichen auswählen
*   keine Standard Pattern wählen wie zum Beispiel den eigenen Namen oder Geburtsjahr

## Aufgabe 2

_Suchen Sie im Internet nach Tools für Wörterbuchangriffe. Welche On- bzw. Offline-Tools_  
_gibt es und welche Arten von Hashwerten können mit den jeweiligen Tools geknackt werden?_

<table><tbody><tr><td>Tool</td><td>Offline/Online</td><td>Crackables Hashes</td></tr><tr><td>John the ripper</td><td>Offline</td><td><code>crypt(3)</code>, <code>bigcrypt</code>, <code>BSDi, Raw MD5, Raw SHA-1, Raw SHA-256, Raw SHA-512...</code></td></tr><tr><td>Hashcat</td><td>Offline</td><td><ul><li>MD4</li><li>MD5</li><li>MD6 (256)</li><li>SHA1</li><li>SHA2-224</li><li>SHA2-256</li><li>SHA2-384</li><li>SHA2-512</li><li>SHA3-224</li><li>SHA3-256</li><li>SHA3-384</li><li>SHA3-512</li><li>RIPEMD-160</li><li>RIPEMD-320</li><li>BLAKE2b-256</li><li>BLAKE2b-512</li><li>BLAKE2s-256</li><li>GOST R 34.11-2012 (Streebog) 256-bit, big-endian</li><li>GOST R 34.11-2012 (Streebog) 512-bit, big-endian</li><li>GOST R 34.11-94</li><li>Half MD5</li><li>Keccak-224</li><li>Keccak-256</li><li>Keccak-384</li><li>...</li></ul></td></tr><tr><td>Hydra</td><td>Online</td><td>einfach alles liste zu lang von https bis ssh</td></tr></tbody></table>

## Aufgabe 3

_John The Ripper“ ist als freie Version erhältlich. Erläutern Sie die Funktionsweise. Welche_  
_Algorithmen zur Hash-Berechnung beherrscht „John The Ripper“? Welche verschiedene_  
_Crack-Modi werden unterstützt? Nennen und erläutern Sie die Unterschiede._

Oben Hashes genannt.

Crackmodi:

*   **Wordlist**: testet Passwortlisten 
*   **Rule-Based**: verändert Listenwörter 
*   **Brute Force**: alle Kombinationen 
*   **Mask**: nutzt bekannte Muster 
*   **Single Mode**: nutzt Userdaten

## Aufgabe 4

_Welcher Schritt ist zunächst notwendig, um auf Linux-Distributionen, die Passwörter in einer_  
_Shadow-Datei speichern, das Cracking der Passwortliste zu starten?_  

Als ersten Schritt muss der unshadow command ausgeführt werden, welcher dafür sorgt das die passwd (Benutzer) und shadow (Passwörter) Datei zusammengeführt werden und eine einzelne Hash Datei entsteht die gecracked wird von John the ripper.

shadow Datei enthält:

*   Benutzername
*   Verschlüsselter Passwort-Hash
*   Anzahl der Tage seit dem Unix-Epoch (1970-01-01), seitdem das Passwort zuletzt geändert wurde
*   Mindestanzahl der Tage, die zwischen Passwortänderungen vergehen müssen
*   Maximale Anzahl der Tage, für die das Passwort gültig ist
*   Anzahl der Tage vor Passwortablauf, um den Benutzer zu warnen
*   Anzahl der Tage nach Passwortablauf, bevor das Konto deaktiviert wird
*   Anzahl der Tage seit dem Unix-Epoch (1970-01-01), an dem das Konto deaktiviert wird
*   Ein reserviertes Feld für zukünftige Verwendung

passwd Datei enthält:

*   **Benutzername** Der Login-Name des Users.
*   **Passwort-Platzhalter**Meist ein `x`. Es signalisiert, dass das echte Passwort verschlüsselt in der `/etc/shadow` liegt.
*   **User ID (UID)** Die eindeutige numerische ID des Benutzers (0 ist immer `root`). 
*   \*\*Group ID (GID)\*\*Die ID der primären Gruppe des Benutzers. 
*   **Benutzerinfo (GECOS)** Ein optionales Feld für den vollen Namen, Telefonnummer oder Büro-Nr. 
*   **Home-Verzeichnis** Der absolute Pfad zum Ordner des Benutzers (z. B. `/home/benutzername`).
*   **Login-Shell** Das Programm, das nach dem Login startet (meist `/bin/bash` oder `/bin/zsh`).

## Aufgabe 5

_Stellen Sie sich folgendes Szenario vor:_  
_Sie haben durch einen schlecht gesicherten Account eines Users Zugriff auf ein System_  
_erlangt. Der User ist privilegiert und steht auf der sudo-Liste. Mit Hilfe des sudo-Befehls war_  
_es Ihnen möglich, die Inhalte der Dateien „/etc/passwd“ und „/etc/shadow“ in lokale Dateien_  
_zu kopieren. In der vorherigen Aufgabe haben Sie bereits einen Befehl recherchiert, mit dem_  
_Sie diese beiden Dateien für eine JTR-geeignete Datei zusammenführen können. Um vollen_  
_Zugriff auf das System zu erlangen, wollen Sie nun das Passwort des root-Account cracken._  
_Die „passwd“ und „shadow“ Dateien liegen im Home Verzeichnis des Kali Containers vor._  
_Benutzen Sie John The Ripper im Terminal, um das Passwort zu cracken._  
_Starten Sie den Crackvorgang von der zusammengeführten Datei mit Hilfe der Wortliste_  
_„pwd.txt“. Die Wortliste liegt im Home-Verzeichnis des Kali-Linux. Beschränken Sie sich_  
_dabei nur auf den root-Account. Andere Passwörter sind nicht von Interesse! Wie lautet das_  
_Passwort von root? Wie lauten die Befehle, um das Passwort zu ermitteln?_  
_Bemerkung: Das Root-Passwort wird für das nächste Praktikum benötigt!_

Dateien zusammenführen und in einer unshadow.txt speichern:

`unshadow passwd shadow > unshadow.txt`

Extrahierter Hash:

`root:$6$2RcXHrjf$kxNZmPkiq2MI7frEKF6wEKhE68Kop2nFs5G7eQesØSVjdg0XwDvlyUG6wzQPh0003QLGimzLVoTHrQKwBiA/h.:0:0:root:/root:/bin/bash`

Die Dollarzeichen (`$`) im Hash-Feld sind bedeutsam. Die Zahl zwischen den ersten beiden `$`\-Zeichen gibt den Hashing-Algorithmus an. In diesem Fall bedeutet `$6$` , dass das Passwort mit dem `sha512crypt`\-Algorithmus gehasht wurde.

*   `$1$` = `md5crypt` (MD5)
*   `$2a$` oder `$2y$` = `bcrypt` (Blowfish)
*   `$5$` = `sha256crypt` (SHA-256)
*   `$6$` = `sha512crypt` (SHA-512)

[https://labex.io/de/tutorials/kali-extract-and-crack-hashes-from-a-linux-shadow-file-594501](https://labex.io/de/tutorials/kali-extract-and-crack-hashes-from-a-linux-shadow-file-594501)

Wordlistcracking ausführen für root user:

`john --wordlist=pwd.txt --users=root unshadow.txt`

Passwörter anzeigen die gecracked wurden:

`john --show unshadow.txt`

Ergebnis dessen ist:

`root:notsafe987:0:0:root:/root:/bin/bash`

Quellen zu John the Ripper Command: [Kommand](https://www.openwall.com/john/doc/)

## Aufgabe 6

_Mitunter kann der Vorgang zum Cracken per Brute-Force oder mit Wortlisten sehr lange_  
_dauern. Allerdings gibt es ein paar Möglichkeiten, in JTR das Cracken zu beschleunigen._  
_Nennen Sie drei Methoden._

*   GPU statt CPU verwenden
*   passende Strategie wählen
*   Hardware ausnutzen mehrere Threads parallel

## Aufgabe 7

_Für Windows-LM-/-NTLM-Passworthashes gibt es eine effektivere und i.d.R. schnellere_  
_Methode das Klartext-Passwort herauszufinden - die Rainbow Tables._  
_Erklären Sie die Funktionsweise von Rainbow Tables. Welche Vorteile haben sie gegenüber_  
_Brute-Force- oder Wörterbuchattacken? Warum sind Rainbow Tables in der Regel effektiver?_

Rainbow tables funktionieren für Hashwerte ohne Salt. Extrem schnelle methode zum knacken von Hashes hat aber ein schlechtes Time-Memoy Tradeoff. Ist gegeben bei früheren Windows Versionen.  
Rainbow Tables sind vorab berechnete Tabellen aus Passwort-Hash-Ketten. Statt Passwörter live zu testen, wird ein Hash einfach in der Tabelle nachgeschlagen.

**Vorteile gegenüber Brute Force/Wörterbuch:**

*   sehr schnelle Suche (Lookup statt Rechnen)
*   viel weniger Hash-Berechnungen im Angriff

**Warum effektiver:**

*   Rechenaufwand wird komplett in die Vorbereitungsphase verlagert

## Aufgabe 8

_Die LM-/NTLM-Hashes von lokalen Benutzerkonten sind in einer SAM-Datenbank abgelegt._  
_Wofür steht SAM und welche Funktion hat der Dienst? Kann man über die SAM-Datenbank_  
_auch Domain-Passwörter auslesen?_

**SAM (Security Account Manager)** ist die Windows-Datenbank für **lokale Benutzerkonten und deren Passwort-Hashes**.

**Domain-Passwörter** liegen im **Active Directory (NTDS.dit)** auf dem Domain Controller, nicht in der SAM.

```
ophcrack-cli -g -d /root/ophcrack -t vista_proba_free,0,1,2 -f /root/ophcrack/win7-victim2.pwdump
```

---

#### `-g`

*   Steht für **„no GUI"** (kein grafisches Fenster)
*   Erzwingt den **Kommandozeilen-Modus**
*   Ohne `-g` würde ophcrack versuchen ein Fenster zu öffnen

---

#### `-d /root/ophcrack`

*   Steht für **„directory"** (Verzeichnis)
*   Gibt an **wo die Rainbow Tables liegen**
*   Ophcrack sucht dort automatisch nach dem passenden Unterordner (`vista_proba_free`)

---

#### `-t vista_free,0,1,2`

*   Steht für **„tables"**
*   Sagt ophcrack **welchen Tabellentyp** und **welche Tabellen-Dateien** genutzt werden sollen
*   `vista_free` → der Typ (kostenloser Vista/Win7-Tabellensatz)
*   `,0,1,2` → die drei Tabellen-Dateien:
    *   `table0.bin` + `table0.index` + `table0.start`
    *   `table1.bin` + `table1.index` + `table1.start`
    *   `table2.bin` + `table2.index` + `table2.start`

---

#### `-f /root/ophcrack/win7-victim.pwdump`

*   Steht für **„file"**
*   Die **Eingabedatei** mit den Windows-Passwort-Hashes
*   Das `.pwdump`\-Format sieht so aus

Ergebnis des Befehls:

```
1 hashes have been found in /root/ophcrack/win7-victim2.pwdump. 
Opened 3 table(s) from /root/ophcrack/vista_proba_free,0,1,2.
0h  0m 29s; Found password 12!34 for user Alice (NT hash #0) in table Vista probabilistic free #1 at column 30146.
0h  0m 33s; search (100%); tables: total 3, done 3, using 0; pwd found 1/1.

Results:

username / hash                  LM password    NT password
Alice   


                                \*\*\* empty \*\*\*  12!34
```