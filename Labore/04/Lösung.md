# Lösung des vierten Labors

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

1)

1.  Exploits: Dieses Modul nutzt eine spezifische Sicherheitslücke in einem Zielsystem aus, um dort unberechtigten Zugriff zu erlangen.
2.  Payloads:  Der Payload ist der eigentliche Schadcode, der nach einem erfolgreichen Exploit auf dem Zielsystem ausgeführt wird, um beispielsweise eine interaktive Konsole (Shell) zu öffnen.
3.  Auxiliary: Diese Hilfsmodule führen unterstützende Aufgaben ohne direkten Einbruch durch, wie das Scannen von Ports, das Erkennen von Diensten oder das Aufspüren von Schwachstellen.
4.  Post: Post-Exploitation-Module werden auf bereits kompromittierten Systemen eingesetzt, um Daten zu stehlen, Rechte zu erweitern oder tiefer in das Netzwerk vorzudringen.

2)

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