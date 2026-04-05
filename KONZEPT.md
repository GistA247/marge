# Konzept: Interaktives Preis-Analyse-Dashboard für Schweißgeräte

**Projekt:** Preis- & Margenanalyse-Tool (Demo → Business-Tool)
**Zielgruppe:** Hersteller (intern: Einkauf, Vertrieb, Controlling)
**Phase:** Demo/Präsentation auf statischem Webserver
**Stand:** April 2026

---

## Inhaltsverzeichnis

1. [Projektziel](#1-projektziel)
2. [Datenmodell](#2-datenmodell)
3. [Technischer Stack](#3-technischer-stack)
4. [Analyse-Framework](#4-analyse-framework)
5. [Features & Funktionalität](#5-features--funktionalität)
6. [UI/UX-Konzept](#6-uiux-konzept)
7. [Datei- & Projektstruktur](#7-datei--projektstruktur)
8. [Roadmap: Demo → Produktivsystem](#8-roadmap-demo--produktivsystem)

---

## 1. Projektziel

Das Dashboard ermöglicht die **tägliche Analyse der Preisentwicklung** von 20 Schweißgeräten über einen Zeitraum von drei Jahren. Im Fokus steht das Verhältnis von Einkaufspreis zu Verkaufspreis — also die **erzielte Marge pro Artikel**.

### Kernfragen, die das Tool beantworten soll:

| # | Fragestellung | Analyse-Typ |
|---|---------------|-------------|
| 1 | Wie hat sich die Marge eines Artikels über die Zeit verändert? | Zeitreihe |
| 2 | Welche Artikel sind aktuell am profitabelsten? | Ranking / Snapshot |
| 3 | Wie wirken sich Einkaufspreisänderungen auf die Marge aus? | Ereignisanalyse |
| 4 | Gibt es saisonale Muster in der Preisentwicklung? | Saisonalität |
| 5 | Welche Artikel zeigen die stärksten Margenschwankungen? | Volatilität |
| 6 | Wie entwickelt sich die Gesamtmarge des Portfolios? | Aggregation |
| 7 | Gibt es Artikel, bei denen Preiserhöhungen die Marge nicht verbessert haben? | Korrelation |

---

## 2. Datenmodell

### 2.1 Artikel-Struktur (20 fiktive Schweißgeräte)

Jeder Artikel enthält folgende Stammdaten:

```json
{
  "id": "SW-001",
  "name": "ProWeld 150 MIG",
  "kategorie": "MIG/MAG",
  "leistung_w": 4500,
  "einkaufspreise": [
    { "gueltig_ab": "2023-01-01", "preis": 210.00 },
    { "gueltig_ab": "2024-06-15", "preis": 228.00 }
  ],
  "verkaufspreise": [
    { "gueltig_ab": "2023-01-01", "preis": 349.00 },
    { "gueltig_ab": "2023-04-01", "preis": 369.00 },
    { "gueltig_ab": "2023-09-15", "preis": 359.00 },
    ...
  ]
}
```

**Regeln:**
- `einkaufspreise`: maximal **2 Einträge** pro Artikel (0 oder 1 Änderung)
- `verkaufspreise`: maximal **9 Einträge** pro Artikel (0 bis 8 Änderungen)
- Alle Preise in **EUR**, zwei Nachkommastellen
- Der Tagespreis wird jeweils aus dem letzten gültigen Eintrag berechnet (Step-Funktion)

### 2.2 Produktkategorien

Die 20 Geräte verteilen sich auf folgende Kategorien:

| Kategorie | Anzahl | Leistungsbereich |
|-----------|--------|-----------------|
| MIG/MAG-Schweißgeräte | 6 | 2.500 – 8.000 W |
| WIG/TIG-Schweißgeräte | 5 | 2.000 – 6.000 W |
| Elektroden-Schweißgeräte | 4 | 3.000 – 9.000 W |
| Plasma-Schneidgeräte | 3 | 1.500 – 5.000 W |
| Multifunktionsgeräte | 2 | 4.000 – 10.000 W |

### 2.3 Berechnete Tagesdaten (abgeleitet aus den Preisstützpunkten)

Aus den Stützpunkten wird zur Laufzeit ein tagesgenaues Daten-Array generiert:

```js
{
  datum: "2023-01-01",
  einkaufspreis: 210.00,
  verkaufspreis: 349.00,
  marge_absolut: 139.00,       // Verkauf - Einkauf
  marge_prozent: 66.19,        // (Marge / Einkauf) * 100
  markup_prozent: 39.83,       // (Marge / Verkauf) * 100  [Handelsspanne]
  preisaenderung_ek: false,    // Flag: EK-Änderung an diesem Tag
  preisaenderung_vk: false     // Flag: VK-Änderung an diesem Tag
}
```

> **Hinweis zu den Margen-Definitionen:**
> - **Marge (auf EK-Basis / Mark-up):** `(VK - EK) / EK × 100` — zeigt wie viel % über dem Einkaufspreis verkauft wird
> - **Handelsspanne (auf VK-Basis / Margin):** `(VK - EK) / VK × 100` — zeigt welcher Anteil des Umsatzes Gewinn ist
> Beide KPIs werden parallel dargestellt, da sie unterschiedliche betriebswirtschaftliche Perspektiven bieten.

---

## 3. Technischer Stack

### 3.1 Begründete Auswahl

| Bereich | Technologie | Begründung |
|---------|-------------|------------|
| **Markup** | HTML5 (semantisch) | Standard, kein Build-Step nötig |
| **Styling** | Tailwind CSS (CDN) | Utility-first, responsiv, kein Setup |
| **Reaktivität** | Alpine.js (CDN) | Leichtgewichtig, kein Build-Step, Vue-ähnlich |
| **Charts** | Apache ECharts (CDN) | Leistungsstärkste OSS-Bibliothek für Zeitreihen, nativ responsiv, interaktiv |
| **Daten** | Statisches JS-Modul (`data.js`) | Einfach, im Browser lauffähig, später austauschbar |
| **Datum/Zeit** | Day.js (CDN) | Leichtgewichtig (2 KB), Moment.js-kompatible API |

### 3.2 Warum Apache ECharts?

ECharts ist für diesen Anwendungsfall besonders geeignet:
- Native Unterstützung für **Zeitreihen** (x-Achse als Datum)
- **DataZoom**-Komponente: interaktives Zoomen & Scrubben auf der Zeitachse
- **Markierungslinien** (markLine) für Preisänderungsereignisse
- **Tooltip** mit mehreren Datenpunkten gleichzeitig
- **Responsive** by default
- Keine Lizenzkosten (Apache 2.0)
- Deutlich performanter als Chart.js bei >1.000 Datenpunkten

### 3.3 Keine Build-Pipeline erforderlich

Alle Abhängigkeiten werden über CDN geladen — die App läuft auf jedem Webserver der statische Dateien ausliefern kann (Apache, Nginx, auch `python -m http.server`).

---

## 4. Analyse-Framework

### 4.1 KPI-Übersicht

```
┌─────────────────────────────────────────────────────────────┐
│                    KPIs pro Artikel/Tag                     │
├────────────────────┬────────────────────────────────────────┤
│ Marge absolut (€)  │ VK - EK                                │
│ Mark-up (%)        │ (VK - EK) / EK × 100                  │
│ Handelsspanne (%)  │ (VK - EK) / VK × 100                  │
├────────────────────┼────────────────────────────────────────┤
│                    KPIs aggregiert (Portfolio/Zeitraum)     │
├────────────────────┬────────────────────────────────────────┤
│ Ø Marge (Zeitraum) │ Arithmetisches Mittel aller Tageswerte │
│ Min/Max Marge      │ Extremwerte im gewählten Zeitraum      │
│ Margenvolatilität  │ Standardabweichung der Tages-Marge     │
│ Margentrend        │ Lineare Regression über den Zeitraum   │
└────────────────────┴────────────────────────────────────────┘
```

### 4.2 Analyseverfahren

#### A) Zeitreihenanalyse (Time Series Analysis)
- Darstellung der Marge (absolut & prozentual) über den gesamten Zeitraum
- Gleitender Durchschnitt (7-Tage, 30-Tage, 90-Tage) zur Trendglättung
- Ereignis-Annotationen: Vertikale Markierungslinien bei EK- und VK-Änderungen

#### B) Ereignisbasierte Analyse (Event Study)
- Analyse der Margenveränderung vor/nach einer Preisänderung
- Berechnung: Ø Marge 30 Tage vor vs. 30 Tage nach jeder Änderung
- Visualisierung als Differenz-Chart

#### C) Ranking & Benchmark-Analyse (Cross-Sectional)
- Aktuelles Margenniveau aller 20 Artikel als Balkendiagramm
- Sortierbar nach Marge absolut, Mark-up %, Handelsspanne %
- Farbkodierung nach Marge-Schwellenwert (konfigurierbar)

#### D) Portfolioanalyse (Aggregation)
- Durchschnittliche Portfoliomarge über alle Artikel und Zeit
- Heatmap: Artikel × Monat → durchschnittliche Monatsmarge
- Verteilung der aktuellen Margen als Histogramm

#### E) Vergleichsanalyse (Comparison)
- Overlay-Chart: bis zu 5 Artikel gleichzeitig vergleichen
- Normalisierte Darstellung (Index = 100 am Startdatum) für Trendvergleich
- Korrelationsmatrix: Zeigt ähnliche Margenverläufe

#### F) Volatilitäts- & Stabilitätsanalyse
- Standardabweichung der Verkaufspreise pro Artikel
- Artikel-Ranking nach Preisstabilität
- Visualisierung: Boxplot pro Artikel für VK-Preis-Verteilung

---

## 5. Features & Funktionalität

### 5.1 Dashboard-Übersicht (Startseite)

- **KPI-Karten** (Snapshot aktueller Tag):
  - Artikel mit höchster / niedrigster Marge
  - Ø Portfolio-Marge
  - Anzahl Preisänderungen im letzten Monat
- **Ranking-Tabelle** aller 20 Artikel mit Sparklines
- **Portfolio-Trendchart** (aggregierte Marge über 3 Jahre)

### 5.2 Artikel-Detailansicht

Für jeden Artikel:
- **Preis-Chart:** EK, VK und Marge (absolut) auf gemeinsamer Zeitachse
- **Marge-%-Chart:** Mark-up und Handelsspanne über Zeit
- **Preisänderungs-Tabelle:** Alle Änderungen mit Datum und Delta
- **Ereignis-Analyse:** Margenveränderung durch jede Preisänderung
- **Statistik-Box:** Min, Max, Ø, Standardabweichung, Trend

### 5.3 Vergleichsansicht

- Artikelauswahl über Checkbox (bis zu 5 gleichzeitig)
- Overlay-Chart der Margenentwicklung
- Normalisierter Vergleich (Index-Darstellung)
- Differenz-Chart (Abweichung vom Portfolio-Durchschnitt)

### 5.4 Filter & Steuerung

| Filter | Typ | Optionen |
|--------|-----|----------|
| Zeitraum | Date-Range-Picker | Frei wählbar, Schnellauswahl (3M, 6M, 1J, 3J) |
| Kategorie | Multi-Select | MIG/MAG, WIG, Elektrode, Plasma, Multi |
| Marge-Schwellenwert | Slider | Filterung auf Artikel unter X % Marge |
| Gleitender Durchschnitt | Toggle + Select | 7 / 30 / 90 Tage |
| Darstellungsart | Radio | Absolut / Prozentual / Normalisiert |

### 5.5 Geplante Features (spätere Phasen)

- CSV/Excel-Export der gefilterten Daten
- PNG-Export der Charts
- Schwellenwert-Alerting (Marge unterschreitet Zielwert)
- Prognose (einfache lineare Extrapolation)
- Anbindung an echte Datenbank (REST API / CSV-Import)

---

## 6. UI/UX-Konzept

### 6.1 Layout-Struktur

```
┌─────────────────────────────────────────────────────┐
│  HEADER: Logo | Navigation | Zeitraum-Filter        │
├──────────┬──────────────────────────────────────────┤
│          │  ┌──────┐ ┌──────┐ ┌──────┐ ┌──────┐   │
│ SIDEBAR  │  │ KPI  │ │ KPI  │ │ KPI  │ │ KPI  │   │
│          │  └──────┘ └──────┘ └──────┘ └──────┘   │
│ Artikel- │  ┌────────────────────────────────────┐  │
│ Liste    │  │   Haupt-Chart (responsiv)           │  │
│          │  │                                    │  │
│ Filter   │  └────────────────────────────────────┘  │
│          │  ┌──────────────┐ ┌────────────────────┐ │
│          │  │ Ranking      │ │ Detail-Tabelle     │ │
│          │  └──────────────┘ └────────────────────┘ │
└──────────┴──────────────────────────────────────────┘
```

**Mobile:** Sidebar wird zu Drawer/Off-canvas, Charts stapeln sich vertikal.

### 6.2 Navigationsstruktur

```
Dashboard (Übersicht)
├── Artikel-Detail (pro Artikel)
├── Vergleichsansicht
├── Portfolio-Analyse
└── Einstellungen (Schwellenwerte, Darstellung)
```

### 6.3 Interaktionsprinzipien

- **Drill-Down:** Klick auf Artikel in Tabelle/Chart → Detailansicht
- **Brush & Zoom:** ECharts DataZoom für Zeitachsen-Zoom per Maus/Touch
- **Tooltip:** Hover über Chart zeigt alle Werte des Tages
- **Markierungen:** EK/VK-Änderungen als vertikale Linien mit Label
- **Responsive Breakpoints:** Mobile (<768px), Tablet (768–1024px), Desktop (>1024px)

### 6.4 Farbsystem (empfohlen)

| Element | Farbe | Bedeutung |
|---------|-------|-----------|
| Verkaufspreis | Blau (#3B82F6) | Neutral/positiv |
| Einkaufspreis | Orange (#F59E0B) | Kosten |
| Marge positiv | Grün (#10B981) | Gut |
| Marge kritisch | Rot (#EF4444) | Unter Schwellenwert |
| EK-Änderung | Orange gestrichelt | Kostenereignis |
| VK-Änderung | Blau gestrichelt | Preisentscheidung |

---

## 7. Datei- & Projektstruktur

```
schweissgeraete-dashboard/
│
├── index.html                  # Einstiegspunkt / Dashboard
├── detail.html                 # Artikel-Detailansicht
├── vergleich.html              # Vergleichsansicht
├── portfolio.html              # Portfolio-Analyse
│
├── js/
│   ├── data.js                 # Statische JSON-Daten (20 Artikel, 3 Jahre)
│   ├── dataEngine.js           # Preisberechnung (Step-Funktion → Tagesdaten)
│   ├── analysis.js             # KPI-Berechnungen, Statistiken
│   ├── charts.js               # ECharts-Konfigurationen
│   ├── filters.js              # Filter-Logik
│   └── app.js                  # Alpine.js App-State & Initialisierung
│
├── css/
│   └── custom.css              # Eigene Styles (ergänzend zu Tailwind)
│
└── KONZEPT.md                  # Dieses Dokument
```

### 7.1 Datenfluss

```
data.js (Stützpunkte)
    │
    ▼
dataEngine.js
    │  generateDailyPrices(artikel, startDate, endDate)
    │  → Array<{ datum, ek, vk, marge_abs, marge_pct, ... }>
    ▼
analysis.js
    │  calcStats(dailyData)     → { min, max, avg, stddev, trend }
    │  calcEventImpact(...)     → Vorher/Nachher-Vergleich
    │  calcPortfolio(...)       → Aggregierte Portfolio-KPIs
    ▼
charts.js
    │  getLineChartConfig(...)  → ECharts-Option-Objekt
    │  getBarChartConfig(...)
    │  getHeatmapConfig(...)
    ▼
Alpine.js (app.js)
    │  Reaktiver State, Event-Handling, DOM-Binding
    ▼
HTML-Templates (index.html, detail.html, ...)
```

---

## 8. Roadmap: Demo → Produktivsystem

### Phase 1 — Demo (aktuell)
- [x] Statische JSON-Daten für 20 Artikel (3 Jahre)
- [ ] Dashboard mit allen Analyse-Views
- [ ] Vollständige Interaktivität (Filter, Zoom, Vergleich)
- [ ] Responsives Design

### Phase 2 — Beta (Übergangssystem)
- [ ] CSV-Import-Funktion (Drag & Drop)
- [ ] LocalStorage für persistente Filter-Einstellungen
- [ ] PNG/CSV-Export
- [ ] Konfigurierbare Marge-Schwellenwerte

### Phase 3 — Produktion
- [ ] REST-API-Anbindung (Backend nach Wahl: Node.js / Python / PHP)
- [ ] Authentifizierung (einfacher Login)
- [ ] Echtzeit-Daten oder täglicher Datenimport
- [ ] Erweiterte Prognose-Funktionen
- [ ] Rollen-basierter Zugriff (Einkauf vs. Vertrieb vs. Controlling)

---

## Anhang A: Technische Entscheidungs-Begründungen

### Warum Alpine.js statt React/Vue?
Für ein Demo-Projekt ohne Build-Pipeline ist Alpine.js ideal: Es wird per CDN geladen, läuft direkt im HTML-Attribut-Kontext, hat keine Abhängigkeiten und ist trivial durch Vue 3 (das eine sehr ähnliche API hat) zu ersetzen, wenn später ein Build-Step eingeführt wird.

### Warum ECharts statt Chart.js oder D3.js?
- **Chart.js:** Einfacher, aber schwächer bei Zeitreihen und DataZoom. Für 1.095 Datenpunkte × 20 Artikel (21.900 Punkte) kann es bei Vergleichsansichten langsam werden.
- **D3.js:** Maximal flexibel, aber erheblicher Entwicklungsaufwand für jede Chart-Variante.
- **ECharts:** Der "Sweet Spot" — reichhaltige Built-in-Komponenten, exzellente Zeitreihen-Unterstützung, performant, gute Dokumentation, aktiv gepflegt von Apache.

### Warum keine Single-Page-Application (SPA)?
Für ein Demo-Projekt mit statischem Server ist eine SPA-Architektur Overkill. Multi-Page mit gemeinsam genutzten JS-Modulen ist einfacher zu debuggen, erklären und präsentieren.

---

## Anhang B: Beispiel-Erkenntnisse aus den Demo-Daten

Die Daten werden so generiert, dass folgende realistische Szenarien sichtbar werden:

1. **Margenkompression durch EK-Erhöhung ohne VK-Anpassung** — ein Artikel, bei dem der EK stieg, der VK aber (zu) spät nachzog
2. **Überreaktion beim VK** — ein Artikel, bei dem VK-Erhöhungen die Marge stark verbesserten, was auf Preissetzungspotenzial hinweist
3. **Saisonales Muster** — ein Artikel mit tendenziell niedrigerem VK im Sommer (fiktive Saisonrabatte)
4. **Stabile Premiumartikel** — Multifunktionsgeräte mit konstant hoher, stabiler Marge
5. **Volatile Niedrigpreisartikel** — häufige VK-Änderungen mit geringen Margen

Diese Szenarien machen die Demo narrativ wertvoll für Präsentationen.
