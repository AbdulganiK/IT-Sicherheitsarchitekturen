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

## Aufgabe 6