# GitHub Pages Deployment – Anleitung

Diese Anleitung beschreibt, wie ein statisches Website-Projekt (z.B. mit Astro) automatisch
über GitHub Actions auf GitHub Pages deployed wird. Basis ist das funktionierende Setup
des Plantoclean-Projekts.

---

## Voraussetzungen

- GitHub-Account (hier: GistA247)
- Lokales Projekt mit `npm run build` → erzeugt einen `dist/`-Ordner
- Git ist eingerichtet und das Projekt in einem GitHub-Repository

---

## 1. GitHub Repository anlegen

1. Auf github.com → **New repository**
2. Name wählen, z.B. `mein-projekt`
3. Sichtbarkeit: **Public** (GitHub Pages ist bei privaten Repos kostenpflichtig)
4. Repository erstellen (ohne README etc., falls lokal schon Dateien vorhanden)

---

## 2. GitHub Pages aktivieren

Im Repository auf GitHub:

1. **Settings** → **Pages**
2. Source: **GitHub Actions** auswählen
3. Speichern

---

## 3. GitHub Actions Workflow anlegen

Datei anlegen: `.github/workflows/deploy.yml`

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [main]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: pages
  cancel-in-progress: false

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup Node
        uses: actions/setup-node@v4
        with:
          node-version: 22

      - name: Install dependencies
        run: npm ci

      - name: Build Astro
        run: npm run build

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./dist

  deploy:
    needs: build
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

> Für andere Frameworks: `npm run build` anpassen und den korrekten Output-Ordner
> bei `path:` eintragen (z.B. `./out` bei Next.js, `./public` bei Hugo).

---

## 4. Astro-spezifisch: Base-URL konfigurieren

Da GitHub Pages die Seite unter einem **Unterordner** ausliefert
(`https://nutzername.github.io/repo-name/`), muss Astro das wissen:

**`astro.config.mjs`:**
```js
export default defineConfig({
  site: 'https://GITHUB-NUTZERNAME.github.io',
  base: '/REPO-NAME',
  // weitere Konfiguration ...
});
```

Alle internen Links im Code müssen die `BASE_URL` verwenden:
```js
const base = import.meta.env.BASE_URL.replace(/\/$/, "");
// Verwendung: href={`${base}/kontakt/`}
```

> Wenn die Seite später auf einer **eigenen Domain** ohne Unterordner läuft,
> einfach `base` entfernen und `site` auf die eigene Domain setzen.

---

## 5. Pushen und deployen

```bash
git add .
git commit -m "Initial deploy setup"
git push origin main
```

GitHub Actions startet automatisch. Status unter:
**Repository → Actions → Deploy to GitHub Pages**

---

## 6. Seite aufrufen

Nach erfolgreichem Deployment:
```
https://GITHUB-NUTZERNAME.github.io/REPO-NAME/
```

Beispiel Plantoclean:
```
https://gista247.github.io/plantoclean/
```

---

## Häufige Probleme

| Problem | Lösung |
|--------|--------|
| Seite lädt, CSS/Bilder fehlen | `base` in `astro.config.mjs` fehlt oder falsch |
| 404 auf allen Seiten | GitHub Pages Source nicht auf "GitHub Actions" gesetzt |
| Build schlägt fehl | Fehler im Actions-Log prüfen (Repository → Actions) |
| Deployment startet nicht | Branch heisst nicht `main` → in `deploy.yml` anpassen |
| `npm ci` schlägt fehl | `package-lock.json` fehlt im Repository |
