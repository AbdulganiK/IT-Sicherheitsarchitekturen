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