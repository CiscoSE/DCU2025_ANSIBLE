# DCU2025 ANSIBLE
Willkommen zum Ansible Lab der Cisco Secure Datacenter University 2025 in Eschborn.

Table of contents
=================

<!--ts-->
   * [Abflugkontrolle](#abflugkontrolle)
   * [Aufgabe 1: Hallo Welt](#aufgabe-1-hallo-welt)
   * [Aufgabe 2: Lists & Dictionaries](#aufgabe-2-lists--dictionaries)
   * [Aufgabe 3: Read Input](#aufgabe-3-read-input)
   * [Aufgabe 4: ACI Tenant anlegen](#aufgabe-4-aci-tenant-anlegen)
   * [Aufgabe 5: ACI Umgebung erstellen](#aufgabe-5-aci-umgebung-erstellen)
   * [Additional Information](#additional-information)
<!--te-->

Links
=====

APIC: https://10.2.0.43/  
APIC: https://10.2.0.44/  
APIC: https://10.2.0.45/  

Abflugkontrolle
===============

* Öffnen sie ihren Link zu der dcloudsession und klicken dann auf das Laptop-Symbol.
  Nun auf "Web RDP" (unten links) klicken, zum öffnen der Browser RDP Session.
<img width="923" alt="Screenshot 2025-03-18 at 17 34 05" src="https://github.com/user-attachments/assets/90b29a58-6df8-4668-ad64-36382c3acd55" />

* Im Windows starten sie bitte den Cisco Secure Client
<img width="321" alt="Screenshot 2025-03-18 at 07 35 02" src="https://github.com/user-attachments/assets/97fc8eaf-a951-4e00-a3a8-94a5928eada4" />

  und melden sich mit den Lab Zugangsdaten an.
<img width="784" alt="Screenshot 2025-03-18 at 08 41 01" src="https://github.com/user-attachments/assets/3b492908-613f-4f4f-b396-b7acf85b3dd5" />

* Prüfen sie ob sie mit ihren Zugangsdaten auf einen der APIC zugreifen können.
<img width="1288" alt="Screenshot 2025-03-18 at 07 49 23" src="https://github.com/user-attachments/assets/22d0604f-4679-4fe2-844d-756b35ba9c4d" />

- Starten sie Visual Studio Code.
<img width="1289" alt="Screenshot 2025-03-18 at 08 05 44" src="https://github.com/user-attachments/assets/3fbae774-4908-4ef6-b485-447186d27077" />
  Es sollte sich automatisch mit dem Windows-Substem für Linux verbinden.

  Falls dies nicht der Fall sein sollte, starten sie WSL  
<img width="456" alt="Screenshot 2025-03-18 at 08 07 43" src="https://github.com/user-attachments/assets/b75a5b69-7641-49c8-950c-085953db5bd3" />

  wechseln in den Ordner code "cd code"
  und führen das commando "code" aus.
<img width="1267" alt="Screenshot 2025-03-18 at 08 13 36" src="https://github.com/user-attachments/assets/3728becc-4f17-451b-ac71-a0fa4d38cb01" />

- Laden sie die restlichen Tasks aus dem Repo in Github als .zip runter
<img width="923" alt="Screenshot 2025-03-18 at 17 16 27" src="https://github.com/user-attachments/assets/950cb111-84ae-484c-bfb4-6041debf08a8" />
  
  und kopieren sie die Dateien in das Linux "code" Verzeichnis (WSL starten, ins code Verzeichnis wechseln und folgendes Kommando absetzen):
  ````
  cp /mnt/c/Users/dcloud/Downloads/DCU2025_ANSIBLE-main/DCU2025_ANSIBLE-main/*.yaml .
  ````

Geschafft

Aufgabe 1: Hallo Welt
=====================

- Öffnen sie in VS Code die Datei task01-hallo_world.yaml
  Das ist ein simples Playbook, welches eine Eingabeaufforderung startet, der sie einen Wert (ihren Namen) übergeben können.
  Dieser Wert wird im nächsten Schritt als Text wieder ausgegeben oder bei verwendung des -v Schalter zusätzlich der Wert der entsprechenden Variabel ausgegeben

  ````
  ansible-playbook task01-hallo_world.yaml
  ````

  ````
  ansible-playbook task01-hallo_world.yaml -v
  ````
  

Aufgabe 2: Lists & Dictionaries
===============================    

- Öffnen sie in VS Code die Datei task02-list_dict.yaml
  Hier werden sollen die Unterschiede von Lists & Dictionaries dargestellt werden, um ihnen eine Idee zu geben wann welche Variante hilfreich sein kann
  Die Werte der jeweiligen variante werden wieder über das debug Modul im Playbook ausgegeben.

  ````
  ansible-playbook task02-list_dict.yaml
  ````

  ````
  ansible-playbook task02-list_dict.yaml -v
  ````
  
Aufgabe 3: Read Input
================

- Öffnen sie in VS Code die Datei task03-read_input.yaml  
  Jetzt nutzen wir eine externe Data Source und nutzen die Informationen im Playbook.

  ````
  ansible-playbook task03-read_input.yaml
  ````


Aufgabe 4: ACI Tenant anlegen
=============================

- Nun legen sie einen Tenant in der ACI Fabric an.
- Öffnen sie in VS Code die Datei task04-aci_create_tenant.yaml und passen den Wert für die Variable student_id an.
- Prüfen sie in VS Code ob ihre Anmelde Daten in inventory.ini korrekt sind und änderen sie diese ggf.
- Öffnen sie den Chrome Browser, melden sich bei einem der APICs an(sofern noch nicht geschehen) und gehen auf den Punkt Tenants>ALL TENANTS.
- Führen sie das Kommando aus und beobachten im wie ihr Tenant angelegt wird im Debug Modul wird der Rückgabe-Wert des Moduls gespeichert.
  
  ````
  ansible-playbook task04-aci_create_tenant.yaml
  ````

Aufgabe 5: ACI Umgebung erstellen
=============================

- Es ist soweit, sie legen eine komplette Umgebung an und prüfen im Nachgang ob der Proxy erreichbar ist (.11 in ihrem Subnetz) und ob die Webseite über den Proxy aufgerufen werden kann (Port 80 des Proxy)
- Öffnen sie in VS Code die Datei task05-aci_create_environment.yaml
- In diesem Playbook fehlen Teile (Tasks oder Loops) die sie finden und korrigieren müssen.
- Passen sie die Werte unter anderen für student_id und subnet_address an.
- Beachten sie bitte:
  - EPG: proxy_EPG soll an den Leaf 311 und 312 am Port 1/1 mit der Enkapsulierung 33+ihre student_id (für student11 wäre die Enkapsulierung 3311 korrekt) angelegt werden
  - EPG: webserver_EPG soll an den Leaf 311 und 312 am Port 1/1 mit der Enkapsulierung 34+ihre student_id (für student11 wäre die Enkapsulierung 3411 korrekt) angelegt werden
  - beide EPG sollen der Domain bm_DOM hinzugefügt werden

  ````
  ansible-playbook task05-aci_create_environment.yaml
  ````


* BONUS: 
  * Generieren sie die subnet_address in dem sie das 3te Oktett 130+student_id berechnen lassen
  * Erweitern sie das Playbook um einen Prompt um die student_id abzufragen
  * Berechnen die die Enkapsuliereng mit der student_id
  * Nutzen sie eine externe Datenquelle

Additional Information
======================


## Tips: 
 

