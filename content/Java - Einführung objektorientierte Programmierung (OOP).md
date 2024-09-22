---
title: Java - Einführung objektorientierte Programmierung (OOP)
draft: false
tags:
  - Java
---
Objektorientierte Programmierung (OOP) befasst sich mit **Klassen** und **Objekten**. Hier sind die wichtigsten Konzepte, begleitet von Beispielen in Java:

---

1. **Daten in der Programmierung**: Programme verwalten verschiedene Datentypen (z.B. Strings, Zahlen, Booleans). Für einfache Informationen sind diese Datentypen ausreichend, aber um komplexe Objekte wie "Schüler" abzubilden, benötigen wir etwas Flexibleres.

2. **Benutzerdefinierte Datentypen**: In Java gibt es keinen eingebauten "Schüler"-Datentyp. Mit OOP können wir **benutzerdefinierte Datentypen** durch **Klassen** erstellen.

---

### Beispiel: Definition einer `Schueler`-Klasse in Java

```java
public class Schueler {
    // Attribute der Klasse
    private String name;
    private double gpa;
    private int jahr;
    private boolean hatStipendium;

    // Konstruktor zum Erstellen eines Schueler-Objekts
    public Schueler(String name, double gpa, int jahr) {
        this.name = name;
        this.gpa = gpa;
        this.jahr = jahr;
        this.hatStipendium = false; // Standardmäßig kein Stipendium
    }

    // Methode, um zu prüfen, ob der Schüler Ehrungen hat
    public boolean hatEhrungen() {
        return this.gpa %3E 3.5;
    }

    // Methode, um ein Stipendium zu vergeben
    public void vergebeStipendium() {
        this.hatStipendium = true;
    }

    // Getter-Methoden für die Attribute
    public String getName() {
        return name;
    }

    public double getGpa() {
        return gpa;
    }

    public int getJahr() {
        return jahr;
    }

    public boolean hatStipendium() {
        return hatStipendium;
    }
}
```

---

3. **Objekte in Java**: Ein **Objekt** ist eine Instanz einer Klasse. Nachdem wir die Klasse `Schueler` definiert haben, können wir nun Objekte (Schüler) erstellen und mit ihnen arbeiten.

---

### Beispiel: Erstellen von Schueler-Objekten

```java
public class Main {
    public static void main(String[] args) {
        // Erstellen von Schueler-Objekten
        Schueler schueler1 = new Schueler("Max", 3.8, 2023);
        Schueler schueler2 = new Schueler("Anna", 3.2, 2022);

        // Prüfen, ob die Schüler Ehrungen haben
        if (schueler1.hatEhrungen()) {
            System.out.println(schueler1.getName() + " hat Ehrungen.");
        } else {
            System.out.println(schueler1.getName() + " hat keine Ehrungen.");
        }

        // Vergeben eines Stipendiums an Anna
        schueler2.vergebeStipendium();
        System.out.println(schueler2.getName() + " hat Stipendium: " + schueler2.hatStipendium());
    }
}
```

**Ergebnisse**:
```
Max hat Ehrungen.
Anna hat Stipendium: true
```

---

4. **Flexibilität von OOP**: Sobald wir eine Klasse definiert haben, können wir beliebig viele Objekte dieser Klasse erstellen. So können wir viele Schüler in unserem Programm anlegen und deren Attribute und Methoden verwenden.

---
### Fazit:
- **Klassen** definieren neue Datentypen, die Attribute und Methoden enthalten.
- **Objekte** sind Instanzen dieser Klassen und repräsentieren reale Entitäten.
- Mit OOP können komplexe Programme flexibel aufgebaut werden, die reale Weltmodelle abbilden, wie z.B. Schüler, Tiere oder Geräte.>)