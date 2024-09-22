---
title: Java - Einführung
draft: false
tags:
  - Java
---
### High-level language
- für Menschen "leicht" lesbar
- näher an text als object code
- nicht ohne compilation/art compilation lesbar für Maschinen
---
### Low-level language
- für Menschen schwerer lesbar
- näher am object code/machine code(binär code)
---
### Compilation
- um den machine code zu "übersetzen"
- im fall von Java werden .java Dateien kompilieren
- jedoch gibt es dabei ein Problem
	- wenn der code compiliert wird, kann der kompilieren code nur noch von diesem System gelesen werden
	- dadurch wird die platform Unabhängigkeit zerstört
- dazu hat java eine Lösung:
	- der .java code wird nicht direkt für das System kompiliert
	- der code wird zu Bytecode, einer .class Datei formatiert
	- dieser code ist cross Platform unabhängig
---
### Java Virtual Machine
- kurz JVM
- genauere Infos [[Java - Virtual Machine]]

- **Bytecode** wird vom **Class Loader** in die JVM geladen.
- **Bytecode** wird auf Gültigkeit und Sicherheit überprüft.
- **Ausführung** durch **Interpreter** oder **JIT-Compiler**.
- **Garbage Collector** verwaltet automatisch den Speicher.