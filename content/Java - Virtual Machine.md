---
title: Java - Virtual Machine
draft: false
tags:
  - Java
---
![[Java - JVM visualisation.png]]
### Laden des Bytecodes

- Die JVM nimmt den Bytecode und lädt ihn mit einer Komponente namens **Class Loader** in den Speicher.
- Der Class Loader ist dafür verantwortlich:
    - Den Bytecode zu finden.
    - Ihn in den Speicher zu laden.
    - Zu überprüfen, ob der Bytecode gültig und sicher ist.
---
### Bytecode-Verifizierung

- Bevor der Bytecode ausgeführt wird, führt die JVM eine Reihe von Überprüfungen durch, um sicherzustellen, dass der Bytecode gültig ist und keine Sicherheitsregeln verletzt.
- Dies verhindert, dass schädlicher oder fehlerhafter Code ausgeführt wird, und sorgt dafür, dass der Bytecode sicher funktioniert.
---
### Ausführung durch Interpretation oder Just-In-Time (JIT) Kompilierung

- Die JVM führt den Bytecode auf eine von zwei Arten aus:
    
	- **a. Interpretation**: Die JVM interpretiert den Bytecode zeilenweise und wandelt jede Anweisung zur Laufzeit in Maschinencode um. Das ist zwar einfach, kann aber langsam sein, weil jede Anweisung jedes Mal neu übersetzt wird.
    
	- **b. Just-In-Time (JIT) Kompilierung**: Um die Leistung zu verbessern, verwendet die JVM einen Just-In-Time-Compiler, der den Bytecode während der Programmausführung in Maschinencode (nativen Code) kompiliert. Der native Code wird dann direkt von der Hardware des Systems ausgeführt, was die Leistung erheblich steigert. Die JVM kann häufig verwendete Abschnitte (Hot Spots) des Codes erneut kompilieren, um sie weiter zu optimieren.
---
### Garbage Collection

- [[Java - Garbage Collector]]
- Eine der Hauptfunktionen der JVM ist die automatische **Garbage Collection**. Die JVM verwaltet automatisch die Speicherzuweisung und -freigabe für Java-Objekte. Wenn ein Objekt nicht mehr benötigt wird (d. h. keine Referenzen mehr darauf bestehen), gibt der Garbage Collector den Speicher zurück, um Speicherlecks zu vermeiden.
---
### JVM-Komponenten

Die JVM besteht aus mehreren wichtigen Komponenten, die zusammenarbeiten, um Java-Programme auszuführen:

- **Class Loader Subsystem**: Lädt, verknüpft und initialisiert Klassen.
- **Speicherbereich**: Verwalten des zur Ausführung verwendeten Speichers. Dazu gehören:
    - **Heap**: Speichert Objekte.
    - **Stack**: Verwaltet Methodenaufrufe und lokale Variablen.
    - **Method Area**: Enthält die Struktur der Klasse (z. B. Methoden, Felder).
    - **PC-Register**: Verfolgt die Ausführung der aktuellen Methode.
- **Execution Engine**: Führt den Bytecode mithilfe des Interpreters oder JIT-Compilers aus.
- **Native Method Interface (JNI)**: Ermöglicht der JVM den Aufruf von Funktionen, die in anderen Sprachen wie C oder C++ geschrieben sind.
- **Garbage Collector**: Verwaltet den Speicher und löscht automatisch Objekte, die nicht mehr verwendet werden.
---
### Plattformunabhängigkeit

- Da die JVM das zugrunde liegende Betriebssystem und die Hardware abstrahiert, kann dasselbe Java-Programm auf jedem Gerät ausgeführt werden, auf dem eine JVM installiert ist, unabhängig vom Betriebssystem oder der Hardwarearchitektur. So erreicht Java Plattformunabhängigkeit.