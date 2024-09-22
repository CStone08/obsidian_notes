---
title: Java - Compiler
draft: false
tags:
  - Java
---
Der Java-Compiler (typischerweise **Javac**) ist dafür verantwortlich, den menschenlesbaren **Java-Quellcode** in eine Form zu transformieren, die von der Java Virtual Machine (JVM) ausgeführt werden kann. Der Vorgang besteht aus mehreren Schritten, von der Analyse des Quellcodes bis zur Erzeugung von Bytecode, der von der JVM ausgeführt werden kann. Hier ist eine Schritt-für-Schritt-Erklärung, wie der Java-Compiler funktioniert:
![[Java - compilation visualisatoion.png]]

---

### 1. **Eingabe des Quellcodes**
Wenn du ein Java-Programm schreibst, erstellst du eine **Quellcode-Datei** mit der Endung `.java`. Diese Datei enthält den in Java geschriebenen, menschenlesbaren Code. Zum Beispiel:

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hallo, Welt!");
    }
}
```

Das ist die Eingabe für den Java-Compiler.

---

### 2. **Lexikalische Analyse (Tokenisierung)**
Der erste Schritt des Kompilierungsvorgangs ist die **lexikalische Analyse**, bei der der Compiler den Quellcode in **Token** zerlegt. Diese Tokens repräsentieren die kleinsten bedeutungsvollen Einheiten im Quellcode, wie Schlüsselwörter, Bezeichner, Operatoren und Satzzeichen.

Zum Beispiel im Code:

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("HelloWorld!");
    }
}
```

Die Tokens wären:
- `public`
- `class`
- `HelloWorld`
- `{`, `}`, `(`, `)` usw.

Diese Tokens werden in den nächsten Schritt übergeben, um weiter analysiert zu werden.

---

### 3. **Syntaxanalyse (Parsing)**
Nach der lexikalischen Analyse überprüft der Compiler die **Syntax** des Programms. In dieser Phase stellt der Compiler sicher, dass die Struktur des Programms den Regeln der Java-Sprache folgt.

Der Compiler erstellt dabei einen **Syntaxbaum** (Parse Tree). Dieser Baum repräsentiert die grammatikalische Struktur des Programms. Wenn Syntaxfehler wie fehlende Semikolons oder falsch strukturierte Schleifen vorliegen, gibt der Compiler einen Fehler aus und stoppt den Vorgang.

Zum Beispiel in der Anweisung:

```java
System.out.println("Hallo, Welt!");
```

Überprüft der Compiler, ob die Methode `println` korrekt aufgerufen wird und ob `"Hallo, Welt!"` ein gültiges Argument ist. Ist die Syntax fehlerhaft, etwa bei einem fehlenden Semikolon (`;`), meldet der Compiler einen Fehler.

---

### 4. **Semantische Analyse**
In dieser Phase überprüft der Compiler die **Bedeutung** (Semantik) des Programms. Dies umfasst:
- Sicherstellen, dass Variablen deklariert wurden, bevor sie verwendet werden.
- Typüberprüfung: Sicherstellen, dass Ausdrücke mit kompatiblen Datentypen verwendet werden (z.B. kann man keinen `String` einer `int`-Variable zuweisen).
- Überprüfung von Methodenaufrufen und Klassenvererbung.

Zum Beispiel:

```java
int a = "Hallo"; // Dieser Code würde bei der semantischen Analyse scheitern, da der Typ nicht übereinstimmt.
```

---

### 5. **Erzeugung des Zwischencodes**
Nach der semantischen Analyse generiert der Compiler einen **Zwischencode**. Im Fall von Java ist dieser Zwischencode der **Bytecode**. Bytecode ist eine Reihe von Anweisungen, die von der Java Virtual Machine (JVM) ausgeführt werden können und unabhängig von der Plattform sind.

Jede `.java`-Datei wird in eine entsprechende `.class`-Datei kompiliert. Zum Beispiel wird die Datei `HelloWorld.java` die Datei `HelloWorld.class` erzeugen, die den Bytecode für das Programm enthält.

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hallo, Welt!");
    }
}
```

Dies wird Bytecode-Anweisungen wie diese erzeugen:

```asm
0: getstatic     #2  // Field java/lang/System.out:Ljava/io/PrintStream;
3: ldc           #3  // String Hallo, Welt!
5: invokevirtual #4  // Method java/io/PrintStream.println:(Ljava/lang/String;)V
8: return
```

Dieser Bytecode kann nun auf jeder Plattform ausgeführt werden, die eine JVM installiert hat.

---

### 6. **Optimierung**
Der Compiler kann während dieser Phase einige grundlegende Optimierungen durchführen, obwohl Java-Bytecode normalerweise eine direkte Übersetzung des Quellcodes ist. Komplexere Optimierungen werden oft der **JIT (Just-In-Time) Compiler** zur Laufzeit überlassen (dies wird weiter unten erklärt).

---

### 7. **Erzeugung des Bytecodes**
Das endgültige Ergebnis des Java-Compilers sind eine oder mehrere **`.class`-Dateien**, die den Bytecode für jede in der Quellcodedatei definierte Klasse oder Schnittstelle enthalten.

Zum Beispiel wird das Kompilieren von `HelloWorld.java` die Datei `HelloWorld.class` erzeugen.

---

### 8. **Ausführung durch die JVM**
Die vom Compiler erzeugten `.class`-Dateien enthalten Bytecode, der nicht an eine bestimmte Plattform gebunden ist, was Java **plattformunabhängig** macht. Diese Bytecode-Dateien werden von der **Java Virtual Machine (JVM)** ausgeführt.

Wenn die JVM ein Java-Programm ausführt, werden zwei wichtige Schritte ausgeführt:
1. **Laden der Klassen**: Die JVM lädt die `.class`-Dateien in den Speicher.
2. **Interpretation des Bytecodes und JIT-Kompilierung**:
   - Zunächst **interpretiert** die JVM den Bytecode und führt ihn Anweisung für Anweisung aus.
   - Während das Programm läuft, verwendet die JVM den **JIT (Just-In-Time) Compiler**, um häufig verwendeten Bytecode in **nativen Maschinencode** zu übersetzen, der schneller ausgeführt werden kann. Dieser kompilierte Code wird im Speicher gespeichert und während der Programmausführung wiederverwendet.

---

### Übersicht über den Java-Kompilierungsprozess:

1. **Schreiben des Quellcodes** → Schreiben von `.java`-Dateien in menschenlesbarem Java-Code.
2. **Kompilierung**:
   - **Lexikalische Analyse** → Zerlegen des Quellcodes in Token.
   - **Syntaxanalyse** → Überprüfung der Struktur des Codes gemäß den Java-Syntaxregeln.
   - **Semantische Analyse** → Sicherstellen, dass der Code sinnvoll ist (Deklaration von Variablen, Überprüfung der Typen).
   - **Erzeugung des Bytecodes** → Übersetzung des Quellcodes in plattformunabhängigen Bytecode.
3. **Erzeugung von `.class`-Dateien** → Ausgabe des Bytecodes in `.class`-Dateien.
4. **Ausführung durch die JVM** → Die JVM lädt die `.class`-Dateien und interpretiert oder kompiliert den Bytecode in nativen Maschinencode zur Ausführung.

---

### Werkzeuge und Komponenten:

- **Javac**: Der Java-Compiler, der `.java`-Dateien in `.class`-Dateien umwandelt.
- **JVM (Java Virtual Machine)**: Führt den Bytecode aus, der vom Compiler generiert wurde.
- **JIT-Compiler**: Teil der JVM, der den Bytecode zur Laufzeit in nativen Maschinencode kompiliert und optimiert.

### Fazit:
Der Java-Compiler übersetzt den menschenlesbaren Java-Quellcode in einen plattformunabhängigen Bytecode, der dann von der JVM ausgeführt wird. Dieser zweistufige Prozess (Kompilieren und Interpretieren/Kompilieren des Bytecodes) ist der Schlüssel zu Java's Philosophie **"Write Once, Run Anywhere"** (einmal schreiben, überall ausführen), die es ermöglicht, dass Java-Programme auf jeder Plattform mit einer JVM laufen.