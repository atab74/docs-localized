.. _Konfigurationsreferenz:

Konfigurationsreferenz
======================

.. _Platzhaltervariablen:

Platzhaltervariablen für Dateipfade
-----------------------------------

Platzhaltervariablen können auf jedem Betriebssystem in beiden unter Windows oder Linux geläufigen Formen ``$VARIABLE`` und ``%VARIABLE%`` verwendet werden.

============= =================
Variable      Expandierter Pfad
============= =================
APPDATA       Benutzerspezifisches Verzeichnis für Programmdaten von Veyon, z. B. ...\Benutzer\Anwendungsdaten\Veyon unter Windows oder ~/.veyon unter Linux
HOME, PROFILE Homeverzeichnis des angemeldeten Benutzers, z. B. C:\Benutzer\Admin unter Windows oder /home/admin unter Linux
GLOBALAPPDATA Systemweites Verzeichnis für Programmdaten von Veyon, z. B. C:\ProgramData\Veyon unter Windows oder /etc/veyon unter Linux
TMP, TEMP     Benutzerspezifisches Verzeichnis für temporäre Dateien, für den Veyon-Dienst unter Windows wird C:\Windows\Temp verwendet, unter Linux immer /tmp
============= =================
