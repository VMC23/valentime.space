# Valentime.space - Projekt-Dokumentation

## Projektkontext
- **Typ**: Astro + Vue Blog
- **Standort**: `/Users/valentine/Documents/valentime.space`
- **Startdatum**: März 2026

## Blog-Struktur

### Verzeichnisstruktur
```
blog/
└── entries/          # Markdown-Dateien für Blog-Beiträge
    ├── *.md
src/
├── pages/
│   └── blog/
│       ├── index.astro      # Blog-Übersichtsseite
│       └── [slug].astro     # Dynamische Einzelbeitragsseite
├── layouts/
│   └── MainLayout.astro     # Hauptlayout
└── global.css              # Globale Styles
```

### Datenmodell (Markdown-Frontmatter)
Jeder Beitrag in `blog/entries/` muss folgende Felder im Frontmatter haben:
```yaml
---
title: "Titel des Beitrags"
date: 2026-03-15
excerpt: "Kurze Beschreibung für die Übersicht"
---
```

### Technische Umsetzung
- **Markdown-Parsing**: `front-matter` package (CommonJS, default export verwenden)
- **Markdown zu HTML**: `marked` package
- **Datei-Lesung**: Node.js `fs.readFileSync` + `glob` für Pattern-Matching

## Wichtige Learnings

### CommonJS vs ES Modules
- `front-matter` ist ein CommonJS-Modul
- Es exportiert die Parse-Funktion direkt als `module.exports`
- **Richtig**: `import frontMatter from 'front-matter'; frontMatter(content)`
- **Falsch**: `import { parse } from 'front-matter'`

### Astro Dynamic Routes
- Jede dynamische Route (`[slug].astro`) benötigt eine `getStaticPaths()` Funktion
- Die Funktion muss inline definiert sein (kein Zugriff auf außerhalb definierte Variablen)
- Rückgabewert: Array von Objekten mit `params` und optional `props`

### Pfad-Auflösung in Astro
- `import.meta.dirname` verweist auf das Verzeichnis der aktuellen Astro-Datei
- Relative Pfade müssen entsprechend angepasst werden (z.B. `../../../blog/entries` von `/src/pages/blog/` aus)

## Animationen und Interaktionen

### GSAP (GreenSock Animation Platform)
**Für alle Animationen ist GSAP zu verwenden:**
- Website: https://gsap.com/
- Installation: `npm install gsap`
- Import: `import { gsap } from 'gsap'`

**Verwendungszwecke für GSAP:**
- Page transitions
- Scroll animations
- Hover effects
- Modal/overlay animations
- Any advanced animation beyond CSS capabilities
