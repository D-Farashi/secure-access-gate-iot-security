# secure-access-gate-iot-security
Entwicklung und Sicherheitsanalyse eines IoT-Zugangssystems mit RFID, QR-Code und Bluetooth auf Raspberry Pi.
# Secure Access Gate – IoT-Sicherheitsanalyse

## 📌 Überblick
Dieses Projekt umfasst die Konzeption, den Aufbau und die Sicherheitsanalyse eines physischen Zugangssystems auf Basis eines Raspberry Pi 4. Das System kombiniert drei Technologien: **RFID**, **QR-Code** und **Bluetooth Low Energy (BLE)**. Ziel ist es nicht nur, ein funktionierendes System zu bauen, sondern gezielt die Schwachstellen dieser Technologien aus Angreiferperspektive zu demonstrieren und Härtungsmaßnahmen abzuleiten.

## 🎯 Zielsetzung & Threat Model
- **Schutzobjekt:** Physischer Zutritt zu einem Raum (simuliert).
- **Angreiferprofil:** Gelegenheitsdieb bis technisch versierter Angreifer mit einfachen Mitteln (Hardware < 50 €).
- **Angriffsvektoren:** RFID-Klonen, QR-Code-Spoofing, BLE-Sniffing/MAC-Spoofing.
- **Ziel:** Nachweis, dass einfache Authentifizierungsmethoden ohne gegenseitige Verschlüsselung unsicher sind.

## 🛠️ Hardware-Architektur
- **Raspberry Pi 4 Model B (1 GB RAM)** als zentrale Steuereinheit
- **MFRC522 RFID-Reader** (SPI-Schnittstelle)
- **USB-Webcam** zur QR-Code-Erkennung
- **Grüne und rote LED** als Statusanzeige (Zugriff gewährt/verweigert)
- **Breadboard, Jumperkabel, 220-Ohm-Widerstände**

## 💻 Software-Architektur
- **Betriebssystem:** Raspberry Pi OS Lite (32-bit)
- **Programmiersprache:** Python 3
- **Bibliotheken:** `RPI.GPIO`, `spidev`, `mfrc522`, `opencv-python`, `pyzbar`, `pybluez`

## 🔒 Sicherheitsanalyse (Kern des Projekts)

### 1. RFID (MIFARE Classic)
**Theoretischer Hintergrund:** MIFARE Classic verwendet den Crypto-1-Algorithmus, der seit 2008 als gebrochen gilt. Mit einem Proxmark3 oder einfacheren Readern lassen sich Karten in Sekunden klonen. Das System vertraut lediglich auf die UID der Karte, die jedoch frei auslesbar und fälschbar ist.
- **Angriffsszenario:** Klonen der Karte mit handelsüblichem Reader.
- **Durchführung:** Die UID der berechtigten Karte wurde mit dem MFRC522-Reader ausgelesen. Die UID lautet `81BBF305CC`. Ein Angreifer mit einem handelsüblichen RFID-Reader (z.B. einem Smartphone mit NFC oder einem Proxmark3) kann diese UID auslesen. Mit einer "Magic Card" oder einem Proxmark3 lässt sich die UID auf eine leere Karte schreiben, wodurch ein Klon entsteht. Das System prüft lediglich die UID und kann einen Klon nicht von der Originalkarte unterscheiden.
- **Gegenmaßnahme:** Einsatz von Karten mit Secure Element (z.B. MIFARE DESFire), Challenge-Response-Verfahren.

### 2. QR-Code
**Theoretischer Hintergrund:** QR-Codes sind lediglich visuelle Träger von Daten. Sie besitzen keine eigene Authentifizierung. Ein Angreifer kann einen legitimen Code überkleben (QRLjacking) oder einen manipulierten Code unterschieben.
- **Angriffsszenario:** Aufkleben eines bösartigen QR-Codes über den legitimen.
- **Durchführung:** Ein QR-Code mit dem Inhalt `SECRET_KEY_123` wurde erstellt und vor die Webcam gehalten. Das System hat den Code erkannt und Zutritt gewährt. Da das System nur den Textinhalt prüft, kann ein Angreifer einen bösartigen QR-Code mit demselben Inhalt über den legitimen Code kleben (QRLjacking). Es findet keine Überprüfung der Quelle oder Signatur statt.
- **Gegenmaßnahme:** Digitale Signatur des QR-Inhalts, visuelle Bestätigung auf separatem Display.

### 3. Bluetooth Low Energy (BLE)
**Theoretischer Hintergrund:** Bluetooth Low Energy sendet MAC-Adressen im Klartext. Ohne Secure Connections ist ein Replay-Angriff oder MAC-Spoofing möglich. Das System prüft lediglich die MAC-Adresse, die von jedem Angreifer mit einfachen Mitteln gefälscht werden kann.
- **Angriffsszenario:** Sniffing der MAC-Adresse und Replay-Angriff.
- **Durchführung:** Mit `bluetoothctl scan on` wurden alle Bluetooth-Geräte in der Umgebung aufgelistet. Die MAC-Adressen der Geräte sind im Klartext sichtbar. Ein Angreifer kann mit einem Linux-System (z.B. `macchanger` oder `hciconfig`) seine eigene MAC-Adresse auf die eines berechtigten Geräts ändern (MAC-Spoofing). Da das System lediglich die MAC-Adresse prüft, wird der Angreifer als berechtigt eingestuft.
- **Gegenmaßnahme:** BLE Secure Connections, App-seitige Challenge-Response.

## 🚀 Fazit & Learnings
*[Platzhalter:]*

## 📫 Kontakt


