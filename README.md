# Tag 15 Projekt — DevSecOps: Security-Pipeline für TechStyle

> **Projektauftrag TechStyle Online Shop.** Dieses Repository ist eure Abgabe
> für Tag 15. Es enthält den Stand von
> [`day_14_solution`](https://github.com/tbzdevops/techstyle/tree/day_14_solution):
> den containerisierten Shop mit Deployment auf AWS.

## Story

Ein Konkurrent von TechStyle wurde gehackt, Kundendaten sind im Netz
aufgetaucht. Der Shop-Betreiber will wissen, ob ihm das auch passieren kann.
Euer Team baut heute eine Security-Pipeline, die jede Änderung am Shop
automatisch prüft und unsichere Änderungen stoppt. Zum Schluss müsst ihr den
Betreiber in einem kurzen Pitch davon überzeugen, dass sich das lohnt.

## Ausgangsstand

- **Eigenes Projekt nach Tag 14:** Übernehmt euren Stand wie an Tag 14 (Weg A):

  ```bash
  git remote add team <URL eures Team-Repos>
  git fetch team
  git rm -r -q .                                   # Stand von day_14_solution entfernen
  git checkout team/<euer-Branch> -- .             # euren Projektstand übernehmen
  git checkout HEAD -- README.md .github/classroom .github/workflows/classroom.yml
  git commit -m "Eigenen Projektstand nach Tag 14 übernommen"
  git push
  ```

- **`day_14_solution`:** Ihr müsst nichts tun, dieses Repository enthält genau
  diesen Stand.

## Aufgaben

**Zeit:** 50 Min | **Format:** Gruppen à 3–4 | **Pitch:** um 11:05 Uhr

Die Vorlagen für beide Workflows stehen in der Tagesplanung von Tag 15,
Abschnitt **Projekt**.

| Zeit | Was |
|------|-----|
| 5 Min | Rollen verteilen, `SNYK_TOKEN` als Repository-Secret anlegen |
| 30 Min | Rolle 1 und Rolle 2 parallel umsetzen, die übrigen Gruppenmitglieder unterstützen und bereiten den Pitch vor |
| 5 Min | Gemeinsam: Gate-Beweis mit einem roten Pull-Request |
| 10 Min | Pitch fertigstellen und einmal laut durchspielen |

**Vorbereitung:** **Settings** → **Secrets and variables** → **Actions** →
**New repository secret** → Name `SNYK_TOKEN`, Wert: euer Snyk-Token. In der
Snyk-Organisation muss **Snyk Code** aktiviert sein.

1. **Rolle 1 – Gate:** `.github/workflows/security.yml` führt bei jedem Push
   auf `main` und bei jedem Pull-Request `snyk test` (SCA) und
   `snyk code test` (SAST) aus, scheitert nur bei High und Critical
   (`--severity-threshold=high`) und lädt die Ergebnisse als SARIF in den
   Security-Tab.
2. **Rolle 2 – Container:** `.github/workflows/container-scan.yml` baut das
   Image und scannt es mit `snyk container test`. Aktualisiert danach die
   `FROM`-Zeile im `Dockerfile` nach der Empfehlung von Snyk und prüft mit
   `docker compose up --build`, dass der Shop weiterhin läuft.
3. **Gemeinsam – Gate-Beweis:** Öffnet einen Pull-Request, der in
   `requirements.txt` die Zeile `PyYAML==5.3` ergänzt. Der Security-Workflow
   muss rot werden. Nicht mergen. Den Link zum roten Lauf tragt ihr in
   `PITCH.md` unter «Beweis» ein.
4. **Alle – Pitch:** `PITCH.md` mit den vier Teilen Risiko, Lösung, Beweis und
   Nutzen, 2–3 Minuten, ohne Fachjargon. Bereitet euch auf Kundenfragen vor.

> ⚠️ Code Scanning steht in **privaten** Repositories nur mit der Lizenz
> «GitHub Code Security» zur Verfügung. Schlägt der SARIF-Upload deshalb fehl,
> ladet die SARIF-Dateien stattdessen mit `actions/upload-artifact@v4` hoch.

## Abnahmekriterien

Diese Kriterien prüft die Pipeline bei jedem Push automatisch. **Die Haken
setzt die Pipeline selbst:** Ein erfülltes Kriterium wird abgehakt, und
sobald eine Änderung es wieder bricht, verschwindet der Haken. Du musst hier
nichts von Hand pflegen, beim nächsten Push wird die Liste überschrieben.

<!-- c50:progress -->
**Fortschritt: 0 / 13 Kriterien erfüllt** ⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜ — Stand: 2026-11-17 21:17 UTC.
<!-- /c50:progress -->

- [ ] ⬜ Rolle 1: Security-Workflow vorhanden (.github/workflows/security.yml)
- [ ] ⬜ Rolle 1: Läuft bei jedem Push auf main und bei jedem Pull-Request
- [ ] ⬜ Rolle 1: SNYK_TOKEN wird als GitHub Secret gelesen
- [ ] ⬜ Rolle 1: SCA mit snyk test
- [ ] ⬜ Rolle 1: SAST mit snyk code test
- [ ] ⬜ Rolle 1: Build scheitert nur bei High und Critical (--severity-threshold=high)
- [ ] ⬜ Rolle 1: Findings als SARIF im Security-Tab oder als Artefakt
- [ ] ⬜ Rolle 2: Container-Workflow vorhanden (.github/workflows/container-scan.yml)
- [ ] ⬜ Rolle 2: Image wird im Workflow gebaut und mit snyk container test gescannt
- [ ] ⬜ Rolle 2: Base-Image im Dockerfile ist aktualisiert (nicht mehr python:3.11-slim)
- [ ] ⬜ Pitch: PITCH.md vorhanden
- [ ] ⬜ Pitch: PITCH.md enthält Risiko, Lösung, Beweis und Nutzen
- [ ] ⬜ Gate-Beweis: PITCH.md verlinkt den roten Pull-Request oder Lauf

Zusätzlich manuell abgenommen (nicht automatisch geprüft):

- Der Security-Workflow läuft im Tab **Actions**, die Findings erscheinen unter
  **Security** → **Code scanning** (oder als Artefakt)
- Der Pull-Request mit `PyYAML==5.3` ist rot und wurde nicht gemergt
- Der Shop läuft mit dem neuen Base-Image (`docker compose up --build`)
- Kunden-Pitch, falls eure Gruppe um 11:05 Uhr ausgelost wird

## Abnahmekriterien selber prüfen

**Lokal**, jederzeit und ohne Push:

```bash
bash .github/classroom/grade.sh
```

Das Skript liest die Tagesnummer aus `.classroom50.yaml`. Du kannst sie auch
erzwingen:

```bash
CLASSROOM_DAY=15 bash .github/classroom/grade.sh
```

Die Ausgabe listet jedes Kriterium mit ✅ oder ❌ und nennt bei jedem ❌ den
konkreten Lösungshinweis. Sobald ein Kriterium fehlt, endet das Skript mit
Exit-Code 1.

**In GitHub**, bei jedem Push:

Der Workflow **🎓 Classroom Autograding** läuft automatisch und hakt die
erfüllten Kriterien oben im README ab. Ergebnis im Tab
**Actions** → letzter Run → Job *Abnahmekriterien prüfen*. Er committet die
Haken auf `main`: Holt sie vor jedem Push mit `git pull --rebase`.

Die Punktzahl ist **anteilig**: Jedes erfüllte Abnahmekriterium zählt einen
Punkt (z. B. `Points 8/13`). Grün wird der Lauf erst, wenn alle Kriterien
erfüllt sind, Teilpunkte gibt es aber ab dem ersten.

## Anwendung lokal starten

Wie an Tag 13 mit Docker Compose:

```bash
cp .env.container.example .env.container   # Werte eintragen, siehe Kommentar in der Datei
docker compose --env-file .env.container up --build -d --wait
```

Der Shop läuft danach auf http://localhost:5001, das Admin-Panel unter `/admin`.

## Musterlösung

Nach dem Unterricht findest du die Musterlösung im Repository
[`tbzdevops/techstyle`](https://github.com/tbzdevops/techstyle/tree/day_15_solution)
auf dem Branch `day_15_solution`.
