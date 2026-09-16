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
*Hinweis: Dieser Abschnitt wird nach den praktischen Tests mit konkreten Ergebnissen, Fotos und Code-Ausschnitten gefüllt.*

### 1. RFID (MIFARE Classic)
- **Angriffsszenario:** Klonen der Karte mit handelsüblichem Reader.
- **Durchführung:** [Platzhalter für Ergebnis]
- **Gegenmaßnahme:** Einsatz von Karten mit Secure Element (z.B. MIFARE DESFire), Challenge-Response-Verfahren.

### 2. QR-Code
- **Angriffsszenario:** Aufkleben eines bösartigen QR-Codes über den legitimen (QRLjacking).
- **Durchführung:** [Platzhalter für Ergebnis]
- **Gegenmaßnahme:** Digitale Signatur des QR-Inhalts, visuelle Bestätigung auf separatem Display.

### 3. Bluetooth Low Energy (BLE)
- **Angriffsszenario:** Sniffing der MAC-Adresse und Replay-Angriff.
- **Durchführung:** [Platzhalter für Ergebnis]
- **Gegenmaßnahme:** BLE Secure Connections, App-seitige Challenge-Response.

## 🚀 Fazit & Learnings
*[Platzhalter: Was hast du gelernt? Was würdest du beim nächsten Mal anders machen?]*

## 📫 Kontakt
davoud.farashi@outlook.com

