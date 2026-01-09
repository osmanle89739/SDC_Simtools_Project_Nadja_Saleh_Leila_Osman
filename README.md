# Krankenhaus-Bettenbelegungssimulation (COVID-19 Nürnberg)

Dieses Projekt simuliert die Auslastung und Wartezeiten in Krankenhäusern (Intensiv- und Normalstationen) in Nürnberg unter Verwendung der **Discrete Event Simulation (DES)**. Ziel ist es, die Auswirkungen unterschiedlicher Patientenaufkommen auf die Wartezeiten und die Systemstabilität zu analysieren.

##  Übersicht

Die Simulation nutzt die Bibliothek `SimPy`, um den Prozess der Patientenaufnahme, die Verweildauer (Length of Stay) und die Ressourcenknappheit (Bettenkapazität) abzubilden. Es werden zwei Szenarien verglichen: der Normalbetrieb und ein Stress-Test bei hoher Belastung.

### Kernfeatures:

* **Monte-Carlo-Simulation:** Durchführung von  unabhängigen Replikationen zur Unsicherheitsquantifizierung.
* **Warm-up Phase:** Vorbelegung der Betten (75% Startkapazität), um einen realistischen "Steady-State" zu erreichen.
* **Stochastische Prozesse:** Modellierung der Ankünfte und Behandlungsdauer mittels Exponentialverteilungen.
* **Statistische Auswertung:** Berechnung von Mittelwerten, Standardfehlern, Konfidenzintervallen und 95%-Quantilen der Wartezeiten.

---

### Ordnerstruktur 

project/
├── notebooks/
│   └── MonteCarlosimulationFInal.ipynb  # Hauptanalyse und finale Ergebnisse
├── src/
│   └── simulation_logic.py              # Kernlogik der DES (SimPy) und MC-Schleifen
├── tests/
│   └── infunferschrittern.ipynb         # Erweiterte Szenarien (5er-Schritte) zur Kipppunkt-Suche
├── requirements.txt                     # Benötigte Python-Bibliotheken
└── README.md                            # Projektbeschreibung 

---
## Technologien

* **Python 3.x**
* **SimPy:** Framework für die ereignisorientierte Simulation.
* **NumPy:** Mathematische Berechnungen und Zufallszahlengenerierung.
* **Pandas:** Strukturierung und tabellarische Darstellung der Ergebnisse.

---

## Parameter & Konfiguration

Die Kapazitäten orientieren sich an realen Werten für den Standort Nürnberg:

| Parameter | Wert | Beschreibung |
| --- | --- | --- |
| `ICU_BEDS` | 47 | Verfügbare Intensivbetten |
| `NORM_BEDS` | 400 | Verfügbare Normalbetten |
| `MEAN_LOS` | 14.0 Tage | Durchschnittliche Liegedauer (Mean Length of Stay) |
| `SIM_DURATION` | 150 Tage | Gesamter Simulationszeitraum |
| `R` | 20 | Anzahl der Simulationsläufe (Replikationen) |

---

##  Durchführung der Simulation

### Funktionsweise des Modells

1. **Initialisierung:** Das Krankenhaus wird zu 75% mit "Preload"-Patienten gefüllt, um Einschwingeffekte zu minimieren.
2. **Ankunftsprozess:** Patienten treffen basierend auf einem Poisson-Prozess (Exponentialverteilung der Zwischenankunftszeiten) ein.
3. **Behandlung:** Falls ein Bett frei ist, wird es belegt. Die Behandlungsdauer ist stochastisch (). Wenn kein Bett frei ist, entsteht eine Wartezeit.
4. **Auswertung:** Nach 150 Tagen werden die Statistiken für das jeweilige Replikations-Szenario aggregiert.

### Starten der Simulation

Stelle sicher, dass alle Abhängigkeiten installiert sind:

```bash
pip install simpy numpy pandas

```

Führe das Skript aus:

```bash
python simulation_script.py

```

---

##  Ergebnisse (Szenarien-Vergleich)

Das Modell vergleicht zwei Hauptszenarien:

1. **Normal (35 Pat./Woche):** Repräsentiert den regulären Betrieb.
2. **Stress-Test (235 Pat./Woche):** Testet das System am theoretischen Kapazitätslimit.

Die Ergebnisse werden in einer Tabelle ausgegeben, die die **theoretische Auslastung ()** der mittleren **Wartezeit** und dem **Konfidenzintervall** gegenüberstellt.

---

##  Lizenz

Dieses Projekt wurde für akademische Zwecke zur Simulation von Krankenhauskapazitäten entwickelt.

