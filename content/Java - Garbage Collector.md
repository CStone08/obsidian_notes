---
title: Java - Garbage Collector
draft: false
tags:
  - Java
---
**Java Garbage Collection (GC)** ist ein automatischer Speicherverwaltungsprozess, der in Java verwendet wird, um den Speicher von Objekten freizugeben, die nicht mehr verwendet werden. Dieser Prozess hilft, Speicherlecks zu vermeiden und sicherzustellen, dass Programme nicht den Speicher ausgehen. So funktioniert es:

---
### Grundlegende Konzepte

1. **Heap-Speicher**: Der Bereich im Arbeitsspeicher, aus dem Java Objekte erstellt. Der Java-Heap ist in verschiedene **Generationen** unterteilt, um die Leistung der Garbage Collection zu verbessern:
    
    - **Young Generation (Junge Generation)**: Hier werden neue Objekte erstellt und starten ihren Lebenszyklus.
    - **Old Generation (Alte Generation)**: Hierhin werden Objekte verschoben, die längere Zeit überlebt haben.
    - **Permanent Generation (PermGen)** (ab Java 8: **Metaspace**): Speichert Metadaten zu Klassen und Methoden.
2. **Objektlebenszyklus**: Objekte werden in der Young Generation erstellt. Wenn sie mehrere GC-Zyklen überleben, werden sie in die Old Generation verschoben.
---
### Generationsbasierte Garbage Collection

Java teilt den Heap-Speicher in Generationen auf, weil Objekte unterschiedlich lange leben:

- **Young Generation**: Hier werden die meisten Objekte erstellt und schnell wieder entfernt (z. B. temporäre Variablen).
- **Old Generation**: Speichert langlebige Objekte (z. B. globale Objekte, die während der gesamten Programmausführung bestehen).
- **Metaspace**: Speichert Metadaten zu Klassen, nicht die Objektdaten selbst.
---
#### Typen von Garbage Collectors

1. **Minor GC**: Sammelt den Speicher von der Young Generation. Dies geschieht häufig und entfernt kurzlebige Objekte.
    
    - **Eden Space**: Die meisten Objekte werden hier erstellt. Wenn der Speicher voll ist, wird ein Minor GC ausgelöst.
    - **Survivor Spaces**: Zwei kleinere Speicherbereiche (S0 und S1), in denen Objekte gespeichert werden, die Minor GC überleben. Nach mehreren GC-Zyklen werden diese in die Old Generation verschoben.
2. **Major (Full) GC**: Sammelt Speicher von der Old Generation. Dieser Vorgang ist aufwändiger, da die Old Generation größer ist und länger lebende Objekte enthält. Ein Full GC kann auch eine Minor GC umfassen.
---
### Grundlegende Schritte der Garbage Collection

1. **Markieren**: Der GC identifiziert (oder "markiert") alle lebenden Objekte, die noch von anderen Objekten oder Wurzeln (wie lokale Variablen oder Thread-Stacks) referenziert werden.
    
2. **Bereinigen/Kompaktieren**: Nachdem der GC die lebenden Objekte identifiziert hat, gibt er den Speicher unreferenzierter Objekte frei. Es gibt zwei Ansätze:
    
    - **Bereinigen (Sweep)**: Der GC gibt nur den Speicherplatz ungenutzter Objekte frei, wodurch Lücken im Speicher entstehen.
    - **Kompaktieren**: Um Fragmentierung zu vermeiden, verschiebt der GC Objekte im Speicher, um zusammenhängende freie Bereiche zu schaffen.
---
### Garbage Collection-Algorithmen

Java bietet mehrere GC-Algorithmen, die je nach Bedarf konfiguriert werden können:

1. **Serial GC**: Ein einfacher, einthreadiger Garbage Collector. Geeignet für kleine Anwendungen, bei denen die GC-Pausenzeit nicht kritisch ist.
    
2. **Parallel GC**: Mehrere Threads werden verwendet, um den GC-Prozess zu beschleunigen. Ideal für mehrthreadige Anwendungen. Der Minor GC läuft parallel.
    
3. **CMS (Concurrent Mark-Sweep) GC**: Reduziert die GC-Pausen, indem der größte Teil der Arbeit parallel zur Anwendung durchgeführt wird. Es reduziert lange Pausen während eines Full GCs, kann jedoch zur Fragmentierung führen.
    
4. **G1 (Garbage First) GC**: Für Anwendungen entwickelt, die niedrige Pausenzeiten erfordern. G1 teilt den Heap in Regionen und führt den GC in kleineren Abschnitten durch, sowohl für Minor als auch für Major Collections. G1 kann den Speicher auch komprimieren und Fragmentierung vermeiden.
    
5. **ZGC und Shenandoah GC**: Dies sind Niedrig-Latenz-Garbage-Collector, die die Auswirkungen des GC auf die Anwendungsleistung minimieren, indem der Großteil der Arbeit parallel durchgeführt wird.
    
---
### Phasen des GC im G1 (Garbage First) Collector

1. **Initial Mark**: Identifiziert alle lebenden Objekte, die direkt von den Wurzeln referenziert werden.
2. **Concurrent Mark**: Verfolgt lebende Objekte im gesamten Heap parallel, ohne die Anwendung zu pausieren.
3. **Remark**: Finalisiert das Markieren und stellt sicher, dass alle während der parallelen Phase verpassten Objekte erfasst werden.
4. **Cleanup**: Identifiziert Bereiche des Heaps, die wiederverwendet werden können, und komprimiert den Speicher bei Bedarf.
---
### Zusammenfassung

- **Automatische Speicherverwaltung**: Java verwaltet den Speicher automatisch mit dem GC und entlastet den Entwickler von der manuellen Speicherverwaltung.
- **Generationsbasierte GC**: Objekte werden basierend auf ihrer Lebensdauer kategorisiert, wobei kurzlebige Objekte häufiger gesammelt werden.
- **Mark-and-Sweep/Kompaktierung**: GC-Algorithmen verwenden Markieren, um lebende Objekte zu finden, und geben den Speicher ungenutzter Objekte frei, manchmal mit Kompaktierung, um Fragmentierung zu vermeiden.
- **Konfigurierbar**: Unterschiedliche GC-Algorithmen können verwendet werden, um die Leistung je nach den spezifischen Anforderungen der Anwendung zu optimieren (z. B. Minimierung der Pausenzeiten oder Maximierung des Durchsatzes).

Der GC von Java sorgt dafür, dass der Speicher effizient verwaltet wird und Anwendungen reibungslos laufen, ohne dass manuell in die Speicherverwaltung eingegriffen werden muss.