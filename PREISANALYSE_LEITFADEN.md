# Preis- und Margenanalyse — Ein Leitfaden für Einsteiger

> Dieses Dokument erklärt die wichtigsten Begriffe, Konzepte und Analysemethoden rund um Preise und Margen im Handel — am Beispiel des Schweißgeräte-Dashboards. Alle Zahlen und Szenarien stammen direkt aus dem Tool.

---

## Inhaltsverzeichnis

1. [Warum Preisanalyse?](#1-warum-preisanalyse)
2. [Die vier Grundbegriffe](#2-die-vier-grundbegriffe)
3. [Mark-up vs. Handelsspanne — der wichtigste Unterschied](#3-mark-up-vs-handelsspanne)
4. [Wie entsteht ein Verkaufspreis?](#4-wie-entsteht-ein-verkaufspreis)
5. [Was ist Margenanalyse?](#5-was-ist-margenanalyse)
6. [Zeitreihenanalyse — Preise im Zeitverlauf](#6-zeitreihenanalyse)
7. [Portfolioanalyse — das Sortiment als Ganzes](#7-portfolioanalyse)
8. [Fünf typische Szenarien aus der Praxis](#8-fünf-typische-szenarien)
9. [Verkaufszahlen, Umsatz und Rohertrag](#9-verkaufszahlen-umsatz-und-rohertrag)
10. [Lagerbestand und sein Einfluss auf die Marge](#10-lagerbestand)
11. [Was ist eine „gute" Marge?](#11-was-ist-eine-gute-marge)
12. [Häufige Fehler und Fallen](#12-häufige-fehler-und-fallen)
13. [Glossar aller Fachbegriffe](#13-glossar)

---

## 1. Warum Preisanalyse?

Stellen Sie sich vor, Sie betreiben einen Online-Shop für Schweißgeräte. Sie kaufen Geräte beim Hersteller ein und verkaufen sie weiter. Irgendwann stellen Sie fest: Der Umsatz steigt, aber das Konto wird nicht voller. Was läuft falsch?

Antwort: Die **Marge** — also der Anteil des Preises, den Sie als Händler einbehalten — ist zu niedrig oder sinkt schleichend. Das passiert häufiger als man denkt, weil:

- **Einkaufspreise steigen** (Rohstoffe, Energie, Lieferketten), aber der Händler erhöht den Verkaufspreis nicht rechtzeitig
- **Wettbewerb drückt den Verkaufspreis**, während der Einkaufspreis stabil bleibt
- **Rabattaktionen** werden zu oft und zu tief gewährt
- **Einzelne Artikel** ruinieren die Gesamtmarge, ohne dass es auffällt

Preisanalyse bedeutet: Sie beobachten systematisch, wie sich Einkaufs- und Verkaufspreise über Zeit entwickeln, welche Artikel margenstark oder -schwach sind, und wann Handlungsbedarf besteht — bevor es zu spät ist.

---

## 2. Die vier Grundbegriffe

### 2.1 Einkaufspreis (EK)

Der **Einkaufspreis** ist der Betrag, den Sie als Händler an Ihren Lieferanten zahlen — netto, also ohne Mehrwertsteuer.

**Beispiel aus dem Tool:**  
Der *ProWeld 150 MIG* (SW-001) kostet ab Januar 2023 **210,00 €** im Einkauf.

Der EK ist Ihr Kostensockel. Alles, was Sie über den EK hinaus verlangen, ist Ihr potenzieller Gewinn.

> **Wichtig:** Der EK ist nicht unveränderlich. Lieferanten erhöhen ihre Preise — durch Rohstoffkosten, Energiepreise, Wechselkurse oder einfach Verhandlungsmacht. Diese Erhöhungen kommen oft kurzfristig und müssen im Verkaufspreis nachgezogen werden.

---

### 2.2 Verkaufspreis (VK)

Der **Verkaufspreis** ist der Betrag, den Ihr Kunde zahlt — ebenfalls netto.

**Beispiel:**  
Der *ProWeld 150 MIG* wird ab Januar 2023 für **349,00 €** verkauft.

Der VK hat zwei Aufgaben:
1. Er muss den EK plus alle weiteren Kosten (Lager, Versand, Personal, Overhead) decken
2. Er soll einen Gewinn übrig lassen

---

### 2.3 Absolute Marge (Marge abs.)

Die **absolute Marge** ist die einfachste Kennzahl: Was bleibt pro verkauftem Stück in Euro übrig?

```
Marge absolut = VK − EK
```

**Beispiel:**
```
ProWeld 150 MIG:  349 € − 210 € = 139 € pro Stück
```

Die absolute Marge sagt Ihnen, wie viel Euro-Rohertrag ein einzelner Verkauf bringt. Sie ist besonders wichtig, wenn Sie berechnen wollen, wie viele Stück Sie verkaufen müssen, um Fixkosten zu decken.

> **Falle:** Ein Artikel mit 139 € Marge klingt besser als einer mit 50 € Marge. Aber wenn der erste Artikel 400 € kostet und der zweite 60 €, ist die relative Betrachtung eine ganz andere Geschichte (→ Mark-up, nächster Abschnitt).

---

### 2.4 Rohertrag

Der **Rohertrag** ist die absolute Marge multipliziert mit der Verkaufsmenge:

```
Rohertrag = Marge absolut × verkaufte Stück
```

Das Dashboard zeigt den Rohertrag für den gewählten Zeitraum in der Statistik-Box der Artikel-Detail-Ansicht. Der Rohertrag ist das, was Ihnen nach dem Wareneinkauf bleibt — bevor weitere Kosten wie Miete, Personal oder Marketing abgezogen werden.

---

## 3. Mark-up vs. Handelsspanne

Das ist der Punkt, an dem viele Einsteiger stolpern: Es gibt **zwei verschiedene Prozentsätze** für dieselbe Situation — und beide sind korrekt, messen aber unterschiedliche Dinge.

### 3.1 Mark-up (Aufschlag auf EK)

Der **Mark-up** beschreibt, um wie viel Prozent Sie den Einkaufspreis aufgeschlagen haben:

```
Mark-up = (VK − EK) / EK × 100
```

**Rechenbeispiel** mit dem ProWeld 150 MIG:
```
Mark-up = (349 − 210) / 210 × 100 = 139 / 210 × 100 = 66,2 %
```

Das bedeutet: Der VK liegt **66,2 % über** dem EK. Sie haben den Einkaufspreis um zwei Drittel aufgeschlagen.

**Wann denkt man in Mark-up?**  
Händler und Einkäufer denken typischerweise in Mark-up, weil sie vom Einkaufspreis ausgehend kalkulieren: „Was muss ich draufschlagen, damit sich der Artikel lohnt?"

---

### 3.2 Handelsspanne (Anteil am VK)

Die **Handelsspanne** beschreibt denselben Gewinn — aber als Anteil am Verkaufspreis:

```
Handelsspanne = (VK − EK) / VK × 100
```

**Rechenbeispiel:**
```
Handelsspanne = (349 − 210) / 349 × 100 = 139 / 349 × 100 = 39,8 %
```

Das bedeutet: Von jedem Euro Umsatz bleiben **39,8 Cent** als Rohertrag übrig — der Rest geht an den Lieferanten.

**Wann denkt man in Handelsspanne?**  
Finanz- und Controlling-Abteilungen rechnen gerne in Handelsspanne, weil sie vom Umsatz ausgehend denken: „Welcher Anteil unseres Umsatzes bleibt uns?"

---

### 3.3 Die entscheidende Beziehung

Mark-up und Handelsspanne messen dieselbe Marge — nur von verschiedenen Seiten. Daher gilt immer:

```
Handelsspanne < Mark-up  (solange die Marge positiv ist)
```

Das liegt daran, dass der VK (Nenner der Handelsspanne) größer ist als der EK (Nenner des Mark-up). Dividiert man dieselbe Zahl durch eine größere Zahl, erhält man einen kleineren Prozentwert.

| Artikel | EK | VK | Marge abs. | Mark-up | Handelsspanne |
|---|---|---|---|---|---|
| ProWeld 150 MIG (SW-001) | 210 € | 349 € | 139 € | **66,2 %** | **39,8 %** |
| EcoWeld 130 MIG (SW-004) | 155 € | 235 € | 80 € | **51,6 %** | **34,0 %** |
| MultiPro 5in1 (SW-020) | 680 € | 1.299 € | 619 € | **91,0 %** | **47,7 %** |

> **Merkhilfe:** Wenn jemand sagt „wir haben 40 % Marge", fragen Sie immer: Meint er Mark-up oder Handelsspanne? Das ist kein Kleinkram — bei einem Artikel für 1.000 € VK ist der Unterschied zwischen 40 % Mark-up (286 € Marge) und 40 % Handelsspanne (400 € Marge) erheblich.

---

## 4. Wie entsteht ein Verkaufspreis?

Es gibt drei grundlegende Strategien, einen VK festzusetzen:

### 4.1 Kostenorientierte Preisbildung (Cost-Plus)

Der klassische Ansatz im Handel: Sie nehmen den EK und schlagen einen festen Prozentsatz auf.

```
VK = EK × (1 + Aufschlagsatz)
```

**Beispiel:** EK = 210 €, gewünschter Mark-up = 70 %  
→ VK = 210 × 1,70 = **357 €**

**Vorteil:** Einfach, sicher, jeder Artikel trägt zur Kostendeckung bei.  
**Nachteil:** Ignoriert, was Kunden bereit sind zu zahlen, und was Wettbewerber verlangen.

---

### 4.2 Wettbewerbsorientierte Preisbildung

Sie schauen, was vergleichbare Produkte am Markt kosten, und positionieren sich bewusst darunter, darüber oder gleichauf.

**Typische Positionen:**
- **Niedrigpreis:** 5–15 % unter Wettbewerb → hohe Stückzahlen, niedrige Marge
- **Marktpreis:** auf Wettbewerbsniveau → mittlere Marge
- **Premium:** 10–30 % über Wettbewerb → niedrige Stückzahl, hohe Marge pro Stück

**Problem:** Wenn alle Wettbewerber ähnlich kalkulieren und einer anfängt zu unterbieten, gerät die Branche in einen Preiskampf, bei dem alle verlieren.

---

### 4.3 Wertbasierte Preisbildung

Der VK orientiert sich daran, was der Artikel dem Kunden **wert** ist — unabhängig vom EK.

Beispiel: Ein Schweißgerät, das die Produktivität verdoppelt, kann mehr kosten als ein günstiges Modell, selbst wenn der Unterschied im EK klein ist. Der Kunde zahlt für den Nutzen, nicht für die Materialkosten.

**Im Dashboard sichtbar:** Die MultiWeld- und MultiPro-Geräte (SW-019, SW-020) haben einen Mark-up über 90 % — weit mehr als günstigere Modelle. Das ist kein Zufall, sondern eine bewusste Positionierung als Premium-Produkt.

---

### 4.4 In der Praxis: Mischung aus allen dreien

Kein Händler folgt nur einer Strategie. Typisch ist:
1. **Mindest-VK** per Cost-Plus sicherstellen (unter diesem Preis wird nie verkauft)
2. **Marktpreis** beobachten und VK in einem vertretbaren Korridor halten
3. **Wert-Argumente** kommunizieren, um eine Prämie zu rechtfertigen

---

## 5. Was ist Margenanalyse?

Margenanalyse bedeutet, die Marge nicht als statische Zahl zu betrachten, sondern als **dynamische Größe, die sich ständig verändert** — durch EK-Änderungen, VK-Anpassungen, Marktdruck und strategische Entscheidungen.

Konkret fragt man:

- **Zeitlich:** Wie entwickelt sich die Marge eines Artikels über Monate und Jahre?
- **Quer:** Welche Artikel sind margenstarker als andere — und warum?
- **Kausal:** Was hat eine Margenveränderung ausgelöst? EK-Erhöhung? VK-Senkung? Aktion?
- **Prognostisch:** Wo droht die Marge in Zukunft unter die Zielschwelle zu fallen?

Das Dashboard deckt die ersten drei Dimensionen ab.

---

## 6. Zeitreihenanalyse

Die wichtigste Analyseart: Wie verändert sich EK, VK und Marge **über die Zeit**?

### 6.1 Was man im Preisverlauf sieht

Öffnen Sie im Dashboard einen Artikel (z.B. *ProWeld 200 MIG*, SW-002) in der Artikel-Detail-Ansicht. Der **Preisentwicklungs-Chart** zeigt drei Linien:

- **Gelb (EK):** Einkaufspreisstufen — oft Treppenform (bleibt monatelang gleich, springt dann)
- **Blau (VK):** Verkaufspreisstufen — ebenfalls Treppen, idealerweise nach jeder EK-Erhöhung
- **Grün (Marge abs.):** Die Differenz zwischen VK und EK — die entscheidende Linie

**Was man erkennen sollte:**

| Muster | Bedeutung |
|---|---|
| EK steigt, VK folgt sofort | Gesunde Preisführerschaft |
| EK steigt, VK folgt verzögert | Temporäre Margenkompression — wie lange? |
| EK steigt, VK steigt gar nicht | Kritisch — Marge bricht ein |
| VK sinkt, EK stabil | Bewusste Aktion oder Wettbewerbsdruck |
| Beide steigen proportional | Stabile Marge trotz Preissteigerung |

---

### 6.2 Markierungslinien verstehen

Im Preisverlauf-Chart zeigt das Dashboard **vertikale Markierungslinien** an jeder Preisänderung:

- **Gelbe gestrichelte Linie:** EK hat sich geändert
- **Blaue gestrichelte Linie:** VK hat sich geändert

Diese Linien helfen, Ursache und Wirkung zu trennen. Wenn nach einer gelben Linie die grüne Margenlinie einbricht, wissen Sie: Der Lieferant hat den EK erhöht, ohne dass der VK nachgezogen wurde.

---

### 6.3 Gleitender Durchschnitt (Moving Average)

Die täglichen Margenlinien können durch Sondereffekte „zackig" wirken. Der **gleitende Durchschnitt** (MA) glättet diese Schwankungen:

- **7-Tage-MA:** Zeigt Wochentrends, noch relativ volatil
- **30-Tage-MA:** Der Standard — zeigt monatliche Entwicklung, gut lesbar
- **90-Tage-MA:** Zeigt den Langfristtrend, ignoriert kurzfristige Ausreißer

**Wann welcher MA?**  
Für eine strategische Beurteilung (sinkt die Marge strukturell?) → 90-Tage-MA.  
Für operative Steuerung (wann wurde die letzte Preisanpassung spürbar?) → 30-Tage-MA.

---

### 6.4 Ereignis-Analyse

Das Dashboard zeigt für jede Preisänderung: Wie war die Marge **30 Tage vorher** vs. **30 Tage nachher**?

**Interpretation:**

```
Grüner Balken nach blauer Markierung (VK-Erhöhung):
→ Die VK-Erhöhung hat die Marge verbessert. Gut.

Roter Balken nach gelber Markierung (EK-Erhöhung):
→ Der höhere EK hat die Marge gedrückt. Handlungsbedarf.

Kleiner Unterschied nach großer EK-Erhöhung:
→ Der VK wurde zwar angepasst, aber nicht genug.
```

**Praxisbeispiel** (SW-002, ProWeld 200 MIG):

- Juli 2024: EK springt von 285 € auf 340 € (+19,3 %)
- Januar 2024: VK wurde bereits auf 489 € erhöht — aber zu wenig
- Mark-up fiel von 64,6 % auf unter 44 %
- Erst Oktober 2024: VK auf 559 € → Mark-up erholt sich auf 64,4 %

Das ist ein klassisches Beispiel für **verzögerte Preisanpassung** — der Händler hat 15 Monate mit zu niedriger Marge gearbeitet.

---

## 7. Portfolioanalyse

Während die Zeitreihenanalyse einen Artikel betrachtet, zeigt die Portfolioanalyse das **gesamte Sortiment** auf einmal.

### 7.1 Margenverteilung (Histogramm)

Das Histogramm im Portfolio-View beantwortet: Wie ist die Marge über das Sortiment verteilt?

**Typische Muster:**

```
Gesundes Portfolio:      Hauptmasse bei 40–70 % Mark-up, wenige Ausreißer nach unten
Preiskampf-Portfolio:    Häufung bei < 30 % — viele Artikel sind knapp kalkuliert
Premiumlastiges Portfolio: Hauptmasse bei > 70 % — wenige Artikel, hohe Marge
```

**Was tun bei vielen Artikeln < 30 %?**
→ Jeden Artikel einzeln prüfen: Ist der niedrige Mark-up strategisch gewollt (Lockartikel, Pflichtartikel)? Oder ist er durch EK-Steigerungen entstanden, die nicht nachgezogen wurden?

---

### 7.2 Kategorievergleich

Verschiedene Produktkategorien haben typischerweise strukturell unterschiedliche Margen:

- **Premium-Kategorien** (Multi-Geräte, Plasma-Profis) → höhere Margen möglich, da weniger Preisvergleich
- **Einstiegskategorien** (MIG/MAG-Basisgeräte) → stärkerer Wettbewerb, engere Margen
- **Zubehör und Sets** → oft höhere prozentuale Marge als Hauptgeräte, da Preisvergleich schwieriger

Im Dashboard-Kategorienvergleich sehen Sie den Ø Mark-up und die Ø Handelsspanne je Kategorie nebeneinander. Eine Kategorie deutlich unter den anderen → Preisstruktur überprüfen.

---

### 7.3 Monats-Heatmap

Die Heatmap ist eines der mächtigsten Werkzeuge: Sie zeigt **alle Artikel × alle Monate** in einer einzigen Ansicht.

**Was leuchtet wie?**
- **Dunkle Felder:** Niedrige Marge in diesem Monat (z.B. EK-Anstieg oder Sommer-Aktion)
- **Helle/grüne Felder:** Hohe Marge
- **Dunkle Spalte (ganzer Monat):** Viele Artikel hatten in diesem Monat niedrige Margen → systemisches Ereignis (Lieferantenerhöhung? Marktpreisdruck?)
- **Dunkle Zeile (ganzer Artikel):** Dieser Artikel hat strukturell niedrige Marge

**Saisonale Muster** sehen Sie als regelmäßig wiederkehrende Helligkeit/Dunkelheit in bestimmten Monaten — z.B. Sommer-Aktionen, die jedes Jahr die Marge drücken.

---

### 7.4 Volatilitäts-Ranking

Die **Volatilität** (Standardabweichung der Marge) misst, wie stark die Marge um ihren Durchschnittswert schwankt.

```
Niedrige Volatilität (< 2 Prozentpunkte): Stabile, planbare Marge
Mittlere Volatilität (2–5 pp):            Moderate Schwankungen, beobachten
Hohe Volatilität (> 5 pp):               Marge schwankt stark — Ursache analysieren
```

**Woher kommt hohe Volatilität?**
- Häufige Preisänderungen (VK oder EK)
- Saisonale Rabattaktionen
- Wettbewerbsdruck mit temporären Gegenmaßnahmen
- Unstrukturierte Preispolitik (kein klares Kalkulationsschema)

Volatile Artikel erfordern mehr Management-Aufmerksamkeit — und sind ein Indiz für fehlende Preisdisziplin.

---

## 8. Fünf typische Szenarien

Das Dashboard enthält fünf Preis-Szenarien, die in der Praxis häufig vorkommen. Hier eine ausführliche Erklärung mit den konkreten Zahlen:

---

### Szenario 1: Margenkompression (SW-002)

**Was passiert:**  
Der Lieferant erhöht den EK — aber der Händler passt den VK nicht sofort oder nicht ausreichend an. Die Marge „komprimiert" sich.

**Zahlen:**
```
Jan 2023: EK = 285 €, VK = 469 €  → Mark-up = 64,6 %
Jul 2024: EK steigt auf 340 €      → Mark-up fällt auf 43,8 %  (!)
Okt 2024: VK steigt auf 559 €      → Mark-up erholt sich auf 64,4 %
```

**Warum passiert das?**
- EK-Erhöhungen kommen oft als unangenehme Überraschung
- Der Händler hofft, die Erhöhung sei temporär
- Kundenbindung: Preiserhöhungen beim Kunden sind schwer kommunizierbar
- Interne Prozesse: Preisanpassungen brauchen Zeit und Freigaben

**Konsequenz bei 15 Monaten Margenverlust:**  
Bei 2 verkauften Stück/Monat und 100 € Margenverlust pro Stück: 15 × 2 × 100 = **3.000 € entgangener Rohertrag** — für einen einzigen Artikel.

**Was tun?**  
Sofortige VK-Anpassung bei EK-Änderungen. Oder zumindest: klare Regel, ab wieviel Prozent EK-Erhöhung der VK automatisch nachgezogen wird.

---

### Szenario 2: Überreaktion VK (SW-007)

**Was passiert:**  
Der VK wird stark erhöht, obwohl der EK stabil bleibt. Die Marge steigt stark an.

**Warum kann das ein Problem sein?**

Hohe Marge klingt gut — und oft ist es das auch. Aber eine übermäßige VK-Erhöhung ohne EK-Begründung kann:
- Kunden vergraulen (besonders bei preissensiblen Einstiegsgeräten)
- Den Artikel aus dem Wettbewerbskorridor heraus katapultieren
- Auf Dauer zu sinkenden Verkaufszahlen führen, die die höhere Marge pro Stück überkompensieren

**Wann ist hohe Marge unproblematisch?**  
Bei Premium-Artikeln, bei denen Kunden nicht stark auf den Preis schauen, oder bei Spezialgeräten ohne direkten Wettbewerb.

---

### Szenario 3: Saisonales Muster (SW-003, SW-016)

**Was passiert:**  
Der VK wird regelmäßig im Sommer gesenkt und im Winter wieder erhöht — eine bewusste saisonale Preisstrategie.

**Zahlen (WeldMaster 170 MIG, SW-003):**
```
Winter (Nov–Apr): VK = 339–349 €  → Mark-up ≈ 74 %
Sommer (Mai–Okt): VK = 319–329 €  → Mark-up ≈ 64 %
EK bleibt stabil bei 195 €
```

**Warum macht man das?**  
Schweißgeräte verkaufen sich im Sommer schlechter (Handwerker haben weniger Innenaufträge, Privatkunden sind im Urlaub). Ein günstigerer Preis stimuliert die Nachfrage in der Schwachsaison.

**Die Abwägung:**  
- Mehr Verkäufe im Sommer (positiv)
- Niedrigere Marge pro Stück (negativ)
- Netto: Sinnvoll, wenn die Mehrabsätze den Margenrückgang überkompensieren

**Im Dashboard erkennbar:**  
Heatmap zeigt regelmäßig im Mai/Juni einen dunkleren Streifen bei saisonalen Artikeln. Das Volatilitäts-Ranking stuft diese Artikel als „moderat volatil" ein.

---

### Szenario 4: Stabile Premium-Marge (SW-019, SW-020)

**Was passiert:**  
EK und VK steigen gemeinsam und proportional. Die Marge bleibt konstant hoch.

**Zahlen (MultiWeld 3in1, SW-019):**
```
Jan 2023: EK = 425 €, VK = 749 €   → Mark-up = 76,2 %
Jan 2024: EK = 435 €, VK = 779 €   → Mark-up = 79,1 %
Jan 2025: EK = 445 €, VK = 809 €   → Mark-up = 81,8 %
```

**Warum funktioniert das?**
- Premium-Kunden kaufen aufgrund von Qualität und Marke, nicht nur wegen des Preises
- Kein starker Wettbewerb in diesem Segment
- Der Händler hat Preismacht und kann Erhöhungen weitergeben

**Was lernt man daraus?**  
Nicht alle Artikel müssen günstig sein. Ein Portfolio braucht „Anker-Artikel" mit stabiler hoher Marge, die schwankende Artikel quersubventionieren können.

---

### Szenario 5: Volatile Niedrigmarge (SW-004, SW-015)

**Was passiert:**  
Der VK wird häufig geändert (Aktionen, Wettbewerbsreaktionen), während der EK ebenfalls steigt. Das Ergebnis: eine Marge, die selten stabil ist und strukturell unter Druck bleibt.

**Zahlen (EcoWeld 130 MIG, SW-004):**
```
Jan 2023: EK = 155 €, VK = 235 €  → Mark-up = 51,6 %
Apr 2023: VK auf 225 € gesenkt      → Mark-up = 45,2 %
Aug 2023: VK auf 239 € erhöht       → Mark-up = 54,2 %
Jan 2024: VK auf 229 € gesenkt      → Mark-up = 47,7 %
Sep 2024: EK steigt auf 168 €,
          VK auf 255 € erhöht       → Mark-up = 51,8 %
```

**Das Problem:**  
Keine klare Preisstrategie → hoher Verwaltungsaufwand für häufige Preisänderungen, unzuverlässige Margenplanung, Kunden gewöhnen sich ans Warten auf Rabatte.

**Was tun?**  
Klare Preis-Leitplanken definieren: Mindest-VK (immer), Standard-VK (Normallage), Aktions-VK (max. X-mal pro Jahr, max. Y % Rabatt).

---

## 9. Verkaufszahlen, Umsatz und Rohertrag

Marge allein sagt nicht alles. Ein Artikel mit 80 % Mark-up, der 2x pro Jahr verkauft wird, ist weniger wertvoll als ein Artikel mit 50 % Mark-up, der täglich abgeht.

### 9.1 Die drei Verkaufs-KPIs

| Kennzahl | Formel | Was sie zeigt |
|---|---|---|
| **Verkaufte Einheiten** | Σ Stück im Zeitraum | Wie oft wurde der Artikel verkauft? |
| **Umsatz** | Σ (Stück × VK) | Wie viel hat der Artikel zum Gesamtumsatz beigetragen? |
| **Rohertrag** | Σ (Stück × Marge abs.) | Wie viel hat der Artikel zum Gesamtgewinn beigetragen? |

### 9.2 Umsatz vs. Rohertrag — ein kritischer Unterschied

Ein häufiger Fehler: Entscheidungen nach Umsatz treffen, obwohl der Rohertrag zählt.

**Beispiel:**

| Artikel | Stück/Monat | VK | Marge abs. | Umsatz/Monat | Rohertrag/Monat |
|---|---|---|---|---|---|
| Artikel A | 50 | 100 € | 15 € | **5.000 €** | 750 € |
| Artikel B | 5 | 500 € | 150 € | 2.500 € | **750 €** |

Artikel A macht doppelt so viel Umsatz — aber **denselben Rohertrag** wie Artikel B. Wer nur auf Umsatz schaut, bevorzugt Artikel A. Wer auf Rohertrag schaut, sind beide gleichwertig.

Im schlimmsten Fall: Artikel A macht viel Umsatz, aber nach Abzug von Versandkosten, Retourenquote und Handling-Aufwand ist er tatsächlich **schlechter** als sein Umsatz suggeriert.

**Faustregel:** Optimieren Sie auf Rohertrag, nicht auf Umsatz.

---

## 10. Lagerbestand

Ein oft unterschätzter Faktor in der Margenanalyse: Wenn ein Artikel nicht verfügbar ist, macht er keinen Umsatz — und damit auch keinen Rohertrag.

### 10.1 Lagerausfallquote

```
Lagerausfallquote = Tage ohne Bestand / Gesamttage × 100
```

Im Dashboard beträgt die simulierte Lagerausfallquote im Schnitt ca. **20 %** — ein Artikel ist also jeden fünften Tag nicht lieferbar.

**Was das bedeutet:**  
Ein Artikel mit 1.000 € theoretischem Monatsumsatz und 20 % Lagerausfallquote macht real nur **800 € Umsatz**. Der entgangene Rohertrag ist dauerhaft verloren — er kann nicht nachgeholt werden.

### 10.2 Ursachen für Lagerausfälle

- Falsche Bestandsplanung (zu geringe Sicherheitsbestände)
- Lieferverzögerungen beim Lieferanten
- Unerwartete Nachfragepeaks
- Saisonale Nachfragemuster, die nicht berücksichtigt wurden

### 10.3 Die Verbindung zur Marge

Lagerausfälle und Marge beeinflussen sich gegenseitig:
- Artikel mit **hoher Marge** sollten nie ausverkauft sein — der entgangene Rohertrag ist zu groß
- Artikel mit **niedriger Marge** können entspannter gesteuert werden
- Nach einem Lagerausfall steigt oft die Nachfrage kurzfristig — was die Statistiken verzerrt

**Tipp:** Im Dashboard sehen Sie in der Statistik-Box der Artikel-Detail-Ansicht, welche Artikel hohe Lagerausfallquoten haben. Prüfen Sie, ob gerade margenstarke Artikel davon betroffen sind.

---

## 11. Was ist eine „gute" Marge?

Die Frage klingt einfach, ist aber stark branchenabhängig. Hier Orientierungswerte für den **technischen Fachhandel** (Schweißgeräte, Elektrowerkzeuge, ähnliche Artikel):

### 11.1 Mark-up-Richtwerte im Fachhandel

| Mark-up | Bewertung | Typisch für |
|---|---|---|
| < 20 % | Kritisch — kaum Kostendeckung möglich | Commodity-Artikel, starker Online-Wettbewerb |
| 20–40 % | Knapp — nur tragbar bei niedrigen Fixkosten | Einstiegsgeräte, Preiskampf-Segmente |
| 40–70 % | Gut — normale Fachhandelsspanne | Mittelklasse-Geräte, Standardsortiment |
| 70–100 % | Sehr gut — starke Marktposition | Spezialgeräte, wenig Wettbewerb |
| > 100 % | Exzellent — Premium oder Nische | Hochpreisige Spezialgeräte, Eigenmarken |

> **Achtung:** Diese Werte gelten für den **Rohertrag** vor weiteren Kosten. Wenn Ihr Unternehmen z.B. 30 % Fixkosten auf den Umsatz hat, brauchen Sie eine Handelsspanne von mindestens 30 % — was einem Mark-up von ca. 43 % entspricht — nur um die Kosten zu decken. Gewinn kommt erst danach.

### 11.2 Der Break-even-Mark-up

Der **Break-even-Mark-up** ist der Mindest-Mark-up, bei dem Sie gerade noch kostendeckend arbeiten:

```
Break-even-Mark-up ≈ Fixkosten-Anteil am Umsatz / (1 − Fixkosten-Anteil)
```

**Beispiel:**  
Fixkosten = 35 % des Umsatzes (Miete, Personal, Overhead)  
→ Break-even-Mark-up = 0,35 / 0,65 = **53,8 %**

Jeder Artikel unter diesem Mark-up **kostet Sie Geld** (übernimmt keine anteiligen Fixkosten). Jeder Artikel darüber erwirtschaftet Gewinn.

---

## 12. Häufige Fehler und Fallen

### Fehler 1: EK-Erhöhungen zu spät weitergeben

**Symptom:** Marge sinkt nach EK-Erhöhung, erholt sich langsam oder gar nicht.  
**Lösung:** Automatische VK-Anpassungsregel: „Bei EK-Erhöhung > X % wird der VK sofort angepasst."

---

### Fehler 2: Zu viele Artikel mit Niedrigmarge

**Symptom:** Umsatz wächst, Rohertrag stagniert.  
**Lösung:** ABC-Analyse: Welche Artikel machen wie viel Rohertrag? Fokus auf A-Artikel (20 % der Artikel, 80 % des Rohertrags).

---

### Fehler 3: Rabatte ohne Mengenplanung

**Symptom:** Sommer-Aktion bringt Mehrabsatz, aber der Rohertrag ist trotzdem niedriger als im Vorjahr.  
**Lösung:** Vor jeder Aktion berechnen: Wie viele Mehrstücke müssen verkauft werden, damit der Rohertrag konstant bleibt?

```
Break-even-Mehrabsatz = ursprünglicher Rohertrag / neuer Rohertrag pro Stück − 1
```

**Beispiel:**  
Normaler VK = 339 €, EK = 195 €, Marge = 144 €  
Aktions-VK = 319 €, Marge = 124 €  
→ Break-even: 144 / 124 − 1 = **16,1 % Mehrabsatz nötig**

Wenn die Aktion nicht mindestens 16 % mehr Stück verkauft, war sie schlechter als kein Angebot.

---

### Fehler 4: Marge mit Gewinn verwechseln

**Symptom:** Mark-up ist 60 %, aber das Unternehmen macht kaum Gewinn.  
**Ursache:** Rohertrag (nach EK) ≠ Gewinn. Dazwischen liegen: Miete, Personal, Marketing, Logistik, Retouren, Abschreibungen.

**Lösung:** Vollkostenrechnung statt reiner Margenbetrachtung.

---

### Fehler 5: SET-Artikel unkritisch kalkuliert

**Symptom:** SET-Artikel haben schlechtere Marge als Einzelgeräte.  
**Ursache:** Der SET-Preis wurde pauschal aus Einzelkomponenten addiert, ohne Aufschlag für Bundling, Verpackung und Handling.

**Im Dashboard sichtbar:** Der SET-Artikel SW-035 (EcoTIG 140 Vollausstattung) hat laut Szenario-Label explizit: „EK-Kompression drückt Set-Marge unter Einzelartikel." Ein Warnsignal.

---

## 13. Glossar

| Begriff | Kurzformel | Erklärung |
|---|---|---|
| **EK** | — | Einkaufspreis (Netto, was der Händler zahlt) |
| **VK** | — | Verkaufspreis (Netto, was der Kunde zahlt) |
| **Marge abs.** | VK − EK | Rohertrag pro Stück in Euro |
| **Mark-up** | (VK−EK)/EK × 100 | Aufschlag auf den EK in Prozent |
| **Handelsspanne** | (VK−EK)/VK × 100 | Rohertraganteil am VK in Prozent |
| **Rohertrag** | Menge × Marge abs. | Gesamter Rohertrag im Zeitraum |
| **Umsatz** | Menge × VK | Gesamtumsatz im Zeitraum |
| **Lagerausfallquote** | Ausfallstage/Gesamt × 100 | Anteil der Tage ohne Lagerbestand |
| **Gleitender Ø (MA)** | Ø der letzten N Tage | Geglätteter Trend einer Zeitreihe |
| **Volatilität / Stddev** | Standardabweichung | Maß für Schwankungsbreite der Marge |
| **Margenkompression** | — | EK steigt, VK folgt nicht → Marge sinkt |
| **Break-even-Mark-up** | Fixkosten / (1−Fixkosten) | Mindest-Mark-up zur Kostendeckung |
| **SET-Artikel** | — | Gebündeltes Paket aus Hauptgerät + Zubehör |
| **Sparkline** | — | Miniaturgraph der letzten 365 Tage |
| **DataZoom** | — | Zoom-Funktion in Charts (Mausrad oder Schieberegler) |
| **KPI** | — | Key Performance Indicator — wichtige Kennzahl |
| **Portfolioanalyse** | — | Analyse des gesamten Sortiments im Vergleich |
| **Zeitreihenanalyse** | — | Analyse der Entwicklung über Zeit |
| **Cost-Plus-Pricing** | VK = EK × (1+Aufschlag) | Preisfindung ausgehend vom Einkaufspreis |
| **Deckungsbeitrag I** | = Marge abs. | Erlös minus variable Kosten (vereinfacht: EK) |

---

*Erstellt auf Basis des Schweißgeräte Preis- & Margenanalyse-Dashboards · Stand April 2026*
