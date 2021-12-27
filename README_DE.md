# Dell-Precision-7520-legacy-macOS

Dieses Repository enthält ein OpenCore EFI für das Dell Precision 7520 (i7-6820HQ, Skylake) für alte
Versionen von macOS, derzeit nur High Sierra und Big Sur, Big Sur wird in einem EFI unterstützt, das sowohl Big Sur als auch Monterey unterstützt, und mit etwas Glück wird dieses EFI alle auf Skylake möglichen macOS-Versionen unterstützen.

# High Sierra
 
### Warnung
Dieses EFI ist derzeit noch komplett unfertig und hat
einige große Probleme. Nur benutzen, wenn man Ahnung von OpenCore hat!

### Bevor man diese EFI ausprobiert, bitte [das hier](#generieren-der-eigenen-serien--und-bearbeitungs-rom) und [das hier](#probleme-im-macos-installer) durchlesen!

Tests passieren auf folgender Hardware:

Modell | Dell Precision 7520
------------- | ---------------
CPU | Intel Core i7-6820HQ
iGPU | Intel HD Graphics 530
dGPU | NVIDIA Quadro M2200 (funktioniert mit Webdrivers)
RAM | 32 GB DDR4
WiFi | Intel® Dual Band-Wireless-AC 8265 (funktioniert teilweise)

## Was funktioniert?
currently not completely known
 - Audio
 - Batterieanzeige
 - Boot
 - Helligkeitseinstellungen
 - Ethernet
 - GPU-Beschleunigung
 - Tastatur + Trackpad
 - Energieverwaltung
 - WLAN
 - Standby
 - USB
 - Kamera
 - Lautsprecher
 - Trackpoint

## Was funktioniert nicht?
currently not completely known
 - Bluetooth
 - SD-Karten Leser
 - Klinkenanschluss

## BIOS-Einstellungen

- Virtualisierungsunterstützung: Aktiviert
- SATA-Modus: AHCI
- Thunderbolt: Deaktiviert
- TPM: Deaktiviert
- Legacy Mode: Deaktiviert
- (für Nvidia-Treiber) Schaltbare Grafik: Deaktiviert

## Wie installiert man EFIs?

Diese Repository herunterladen und in die interne EFI-Partition kopieren, indem man sie einbindet, das ist alles.

## Wie installiert man macOS?

Es gibt zwei Wege, wie man einen Installer auf einem USB Stick macht:

1. Wenn man einen funktionierende Installation von macOS hat, den macOS Installer aus dem AppStore herunterladen, dann mit `createinstallmedia` einen Installer erstellen, indem man den folgenden Command ins Terminal eingibt `sudo /Applications/Install\ macOS\ Monterey.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume`.

2. Mit Windows muss man [macrecovery.py](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/winblows-install.html) vom offiziellen OpenCore-Paket nutzen.

Nachdem du einen startbaren Installer erstellt hast, die EFI in die EFI-Partition vom Installer kopieren und dann wie auf einem realen Mac installieren (GUID Partitionstabelle; APFS). Nach der Installation die EFI-Partition vom gerade installierten macOS einbinden und die EFI in die Partition kopieren..

## Probleme im macOS Installer
Wenn USB und Trackpad nicht wie gedacht im Installer funktionieren, gehe ich hier
zumindest schnell darüber, wie man das Trackpad funktionsfähig bekommt.
Was passiert, ist , dass AlpsHID, der Kext für Magic Trackpad Emulation im Installer nicht 
wie gedacht funktioniert, also muss man temporär für die Installation AlpsHID deaktivieren.
Das macht man, indem man die „config.plist“ (EFI/OC) in einem Plist-Editor öffnet und
dort in die Sektion Kernel geht, nach AlpsHID sucht und „ENABLED“ auf „false“ stellt.
Nach der Installation das am besten wieder auf true stellen, weil AlpsHID für die
reibungslose Funktion des Trackpads erforderlich ist.

## WLAN
Damit WLAN auf High Sierra funktioniert, muss man das Programm HeliPort installieren, man
findet es hier: https://github.com/OpenIntelWireless/HeliPort, und dann einfach auf macOS installieren
und dann bei jedem Start ausführen. Es ist nicht perfekt, aber Airportlvm hat zumindest bei mir
die Funktion vollständig verweigert. 

## Nvidia-Treiber
Um Nvidia-Treiber zu installieren, muss man https://www.tonymacx86.com/nvidia-drivers/ im Browser öffnen und einfach die neueste Version herunterladen und installieren. Wenn noch nicht erledigt muss man dann im UEFI Schaltbare Grafik deaktivieren und Neustarten. Danach sollte das System auf der Nvidia-Karte laufen. 

## Generieren der eigenen Serien- und Bearbeitungs-ROM

Benutze GenSMBIOS (https://github.com/corpnewt/GenSMBIOS) um eine eigene Serial für MacBookPro13,3 zu generieren.

Benutze PlistEdit Pro oder irgendeinen guten Plist-Editor, um manuell die Daten in die folgenden Sektionen der plist einzugeben, wie auch im Video gezeigt: (SystemSerialNumber, MLB, and UUID)

https://user-images.githubusercontent.com/59102649/116117179-3ea51200-a6bc-11eb-8a18-a03f7bb5bf1d.mp4
Man sollte auch die Ethernet-Adapter und Mac-Adresse in die ROM-Sektion eingeben.

## Credits

* [acidanthera](https://github.com/acidanthera) (for OpenCore and the kexts)
* [dortania](https://dortania.github.io/OpenCore-Install-Guide/) (for their awesome guide)
* [OpenIntelWireless](https://github.com/OpenIntelWireless) (for Intel WiFi and Bluetooth)
* [blankmac](https://github.com/blankmac/AlpsHID) (for the APLS I2C TouchPad kext)
# Dell-Precision-7520-legacy-macOS

Dieses Repository enthält ein OpenCore EFI für das Dell Precision 7520 (i7-6820HQ, Skylake) für alte
Versionen von macOS, derzeit nur High Sierra und Big Sur, Big Sur wird in einem EFI unterstützt, das sowohl Big Sur als auch Monterey unterstützt, und mit etwas Glück wird dieses EFI alle auf Skylake möglichen macOS-Versionen unterstützen.

# High Sierra
 
### Warnung
Dieses EFI ist derzeit noch komplett unfertig und hat
einige große Probleme. Nur benutzen, wenn man Ahnung von OpenCore hat!

### Bevor man diese EFI ausprobiert, bitte [das hier](#Generating-your-own-serial-and-Editing-ROM) und [das hier](#trouble-in-the-macos-installer) durchlesen!

Tests passieren auf folgender Hardware:

Modell | Dell Precision 7520
------------- | ---------------
CPU | Intel Core i7-6820HQ
iGPU | Intel HD Graphics 530
dGPU | NVIDIA Quadro M2200 (funktionieren mit Webdrivers)
RAM | 32 GB DDR4
WiFi | Intel® Dual Band-Wireless-AC 8265 (funktioniert teilweise)

## Was funktioniert?
currently not completely known
 - Audio
 - Batterieanzeige
 - Boot
 - Helligkeitseinstellungen
 - Ethernet
 - GPU-Beschleunigung
 - Tastatur + Trackpad
 - Energieverwaltung
 - WLAN
 - Standby
 - USB
 - Kamera
 - Lautsprecher
 - Trackpoint

## Was funktioniert nicht?
currently not completely known
 - Bluetooth
 - SD-Karten Leser
 - Klinkenanschluss

## BIOS-Einstellungen

- Virtualisierungsunterstützung: Aktiviert
- SATA-Modus: AHCI
- Thunderbolt: Deaktiviert
- TPM: Deaktiviert
- Legacy Mode: Deaktiviert
- (für Nvidia-Treiber) Schaltbare Grafik: Deaktiviert

## Wie installiert man EFIs?

Diese Repository herunterladen und in die interne EFI-Partition kopieren, indem man sie einbindet, das ist alles.

## Wie installiert man macOS?

Es gibt zwei Wege, wie man einen Installer auf einem USB Stick macht:

1. Wenn man einen funktionierende Installation von macOS hat, den macOS Installer aus dem AppStore herunterladen, dann mit `createinstallmedia` einen Installer erstellen, indem man den folgenden Command ins Terminal eingibt `sudo /Applications/Install\ macOS\ Monterey.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume`.

2. Mit Windows muss man [macrecovery.py](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/winblows-install.html) vom offiziellen OpenCore-Paket nutzen.

Nachdem du einen startbaren Installer erstellt hast, die EFI in die EFI-Partition vom Installer kopieren und dann wie auf einem realen Mac installieren (GUID Partitionstabelle; APFS). Nach der Installation die EFI-Partition vom gerade installierten macOS einbinden und die EFI in die Partition kopieren..

## Probleme im macOS Installer
Wenn USB und Trackpad nicht wie gedacht im Installer funktionieren, gehe ich hier
zumindest schnell darüber, wie man das Trackpad funktionsfähig bekommt.
Was passiert, ist , dass AlpsHID, der Kext für Magic Trackpad Emulation im Installer nicht 
wie gedacht funktioniert, also muss man temporär für die Installation AlpsHID deaktivieren.
Das macht man, indem man die „config.plist“ (EFI/OC) in einem Plist-Editor öffnet und
dort in die Sektion Kernel geht, nach AlpsHID sucht und „ENABLED“ auf „false“ stellt.
Nach der Installation das am besten wieder auf true stellen, weil AlpsHID für die
reibungslose Funktion des Trackpads erforderlich ist.

## WLAN
Damit WLAN auf High Sierra funktioniert, muss man das Programm HeliPort installieren, man
findet es hier: https://github.com/OpenIntelWireless/HeliPort, und dann einfach auf macOS installieren
und dann bei jedem Start ausführen. Es ist nicht perfekt, aber Airportlvm hat zumindest bei mir
die Funktion vollständig verweigert. 

## Nvidia-Treiber
Um Nvidia-Treiber zu installieren, muss man https://www.tonymacx86.com/nvidia-drivers/ im Browser öffnen und einfach die neueste Version herunterladen und installieren. Wenn noch nicht erledigt muss man dann im UEFI Schaltbare Grafik deaktivieren und Neustarten. Danach sollte das System auf der Nvidia-Karte laufen. 

## Generieren der eigenen Serien- und Bearbeitungs-ROM

Benutze GenSMBIOS (https://github.com/corpnewt/GenSMBIOS) um eine eigene Serial für MacBookPro13,3 zu generieren.

Benutze PlistEdit Pro oder irgendeinen guten Plist-Editor, um manuell die Daten in die folgenden Sektionen der plist einzugeben, wie auch im Video gezeigt: (SystemSerialNumber, MLB, and UUID)

https://user-images.githubusercontent.com/59102649/116117179-3ea51200-a6bc-11eb-8a18-a03f7bb5bf1d.mp4
Man sollte auch die Ethernet-Adapter und Mac-Adresse in die ROM-Sektion eingeben.

## Credits

* [acidanthera](https://github.com/acidanthera) (for OpenCore and the kexts)
* [dortania](https://dortania.github.io/OpenCore-Install-Guide/) (for their awesome guide)
* [OpenIntelWireless](https://github.com/OpenIntelWireless) (for Intel WiFi and Bluetooth)
* [blankmac](https://github.com/blankmac/AlpsHID) (for the APLS I2C TouchPad kext)
