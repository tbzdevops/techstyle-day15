# Tag 15 Projekt — Container Teil 1

> **Projektauftrag TechStyle Online Shop.** Dieses Repository ist dein
> Startpunkt fuer Tag 15 und enthaelt den Stand nach Tag 14.

## Ausgangslage

Die monolithische Architektur des Shops macht Updates schwerfaellig und
fehleranfaellig. In einem zweitaegigen Intensivprojekt beginnt das Team mit
der Containerisierung der Applikation als ersten Microservice: Docker-
Grundlagen, Container-Images und eine Container-Registry zur Verwaltung
dieser Images.

## Vorbereitung

Installiere Docker und Docker Compose auf deiner Entwicklungsmaschine.

## Aufgaben

### Auftrag 1 — Monolith analysieren und Komponenten herausbrechen

- Analysiere die bestehende Shop-Anwendung.
- Identifiziere die Komponenten, die in einzelne Container aufgesplittet
  werden koennten.
- Erstelle ein Diagramm der Architektur vor und nach der Containerisierung.

### Auftrag 2 — Applikation containerisieren

- Entwickle ein `Dockerfile`, das die Applikation in einem Container
  betreibt.
- Entwickle eine Docker-Compose-Datei, die den Applikationscontainer und die
  Datenbank startet.
- Baue und teste das Container-Image lokal.
- Implementiere eine CI/CD-Pipeline fuer automatisches Image-Building.

**Ziel:** unter `https://github.com/USERNAME?tab=packages` liegt ein Docker
Image mit der containerisierten Applikation.

> Der Workflow-Dateiname muss mit `container`, `build` oder `docker` beginnen
> (z. B. `container-build.yml`), damit die automatische Pruefung ihn findet.

## Abnahmekriterien

Diese Kriterien prueft die Pipeline bei jedem Push automatisch. **Die Haken
setzt die Pipeline selbst:** ein erfuelltes Kriterium wird abgehakt, und
sobald eine Aenderung es wieder bricht, verschwindet der Haken. Du musst hier
nichts von Hand pflegen — beim naechsten Push wird die Liste ueberschrieben.

<!-- c50:progress -->
**Fortschritt: 0 / 3 Kriterien erfüllt** ⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜ — Stand: 2026-08-24 21:16 UTC.
<!-- /c50:progress -->

- [ ] ⬜ Container/Build-Workflow existiert
- [ ] ⬜ Docker Image Build im Workflow
- [ ] ⬜ Registry-Push oder Image Scanning vorhanden

Zusaetzlich manuell abgenommen (nicht automatisch geprueft):

- Monolith analysiert und Komponenten identifiziert
- Architekturdiagramm vor/nach der Containerisierung
- Microservice-Stack mit Docker Compose erstellt

## Abnahmekriterien selber pruefen

**Lokal** — jederzeit, ohne Push:

```bash
bash .github/classroom/grade.sh
```

Das Skript liest die Tagesnummer aus `.classroom50.yaml`. Du kannst sie auch
erzwingen:

```bash
CLASSROOM_DAY=15 bash .github/classroom/grade.sh
```

Die Ausgabe listet jedes Kriterium mit ✅ oder ❌ und nennt bei jedem ❌ den
konkreten Loesungshinweis. Sobald ein Kriterium fehlt, endet das Skript mit
Exit-Code 1.

**In GitHub** — bei jedem Push:

Der Workflow **🎓 Classroom Autograding** laeuft automatisch und hakt die
erfuellten Kriterien oben im README ab. Ergebnis im Tab
**Actions** → letzter Run → Job *Abnahmekriterien pruefen*.

Die Punktzahl ist **anteilig**: jedes erfuellte Abnahmekriterium zaehlt einen
Punkt (z. B. `Points 8/13`). Gruen wird der Lauf erst, wenn alle Kriterien
erfuellt sind — Teilpunkte gibt es aber ab dem ersten.

## Anwendung lokal starten

```bash
./run_dev.sh
```

Legt ein venv an, installiert die Abhaengigkeiten, seedet die Datenbank und
startet den Dev-Server auf http://localhost:5000. Admin-Panel unter `/admin`.

Hinweise zur Anwendung:

- Die Datenbank liegt unter `/tmp/techstyle.db`.
- `python seed_data.py` (im aktivierten venv) setzt die Produkte zurueck.
- Das Admin-Panel hat noch kein Login — das ist zum jetzigen Zeitpunkt so gewollt.
