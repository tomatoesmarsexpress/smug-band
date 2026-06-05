# Empfohlene Projektstruktur für Astro-Websites

Diese Struktur legt den Fokus auf **Wartbarkeit**, **Skalierbarkeit** und **klare Trennung der Verantwortlichkeiten**.

## Übersicht

```
smug_website/
├── public/                    # Statische Assets (unverändert im Build)
│   ├── favicon.svg
│   ├── favicon.ico
│   ├── images/                # Bilder, die direkt referenziert werden
│   │   ├── logo.svg
│   │   └── og-image.jpg       # Open Graph / Social Sharing
│   └── fonts/                 # Webfonts (falls selbst gehostet)
│
├── src/
│   ├── assets/                # Assets, die vom Build verarbeitet werden
│   │   └── images/            # Optimierte Bilder (Astro Image)
│   │
│   ├── components/            # Wiederverwendbare UI-Komponenten
│   │   ├── ui/                # Generische UI-Bausteine
│   │   │   ├── Button.astro
│   │   │   ├── Card.astro
│   │   │   └── Header.astro
│   │   ├── layout/            # Layout-spezifische Komponenten
│   │   │   ├── Navigation.astro
│   │   │   ├── Footer.astro
│   │   │   └── Sidebar.astro
│   │   └── sections/          # Größere Seitenabschnitte
│   │       ├── Hero.astro
│   │       └── ContactForm.astro
│   │
│   ├── content/               # Content Collections (Astro)
│   │   ├── blog/
│   │   │   ├── config.ts      # Schema für Blog-Posts
│   │   │   └── *.md
│   │   └── pages/             # CMS-ähnliche Seiten (optional)
│   │       └── *.md
│   │
│   ├── layouts/
│   │   ├── BaseLayout.astro   # Minimales HTML-Grundgerüst
│   │   ├── PageLayout.astro   # Standard-Seitenlayout
│   │   └── BlogLayout.astro   # Layout für Blog/Artikel
│   │
│   ├── pages/                 # Dateibasiertes Routing
│   │   ├── index.astro
│   │   ├── about.astro
│   │   ├── contact.astro
│   │   └── blog/
│   │       ├── index.astro    # Blog-Übersicht
│   │       └── [...slug].astro # Dynamische Blog-Artikel
│   │
│   ├── styles/
│   │   ├── global.css         # Globale Styles, Tailwind-Imports
│   │   ├── variables.css      # CSS Custom Properties
│   │   └── utilities.css      # Projekt-spezifische Utilities
│   │
│   ├── lib/                   # Hilfsfunktionen, Utilities
│   │   ├── utils.ts           # Allgemeine Hilfsfunktionen
│   │   └── constants.ts       # Konstanten, Konfiguration
│   │
│   ├── data/                  # Statische Daten (JSON, TS)
│   │   ├── navigation.ts
│   │   └── team.ts
│   │
│   └── env.d.ts               # TypeScript-Umgebungsdefinitionen
│
├── astro.config.mjs
├── package.json
├── tsconfig.json
└── .env.example               # Beispiel für Umgebungsvariablen
```

---

## Erläuterungen

### `public/` vs. `src/assets/`
- **public/**: Dateien werden 1:1 kopiert. Ideal für Favicons, robots.txt, statische Bilder.
- **src/assets/**: Astro kann Bilder optimieren (z.B. mit `<Image>`). Ideal für Fotos, die in Komponenten eingebunden werden.

### Komponenten-Hierarchie
| Ordner | Zweck |
|--------|-------|
| `ui/` | Kleine, wiederverwendbare Bausteine (Buttons, Inputs, Cards) |
| `layout/` | Navigation, Footer, Sidebar – strukturieren die Seite |
| `sections/` | Größere Blöcke wie Hero-Bereiche, Formulare |

### Content Collections
Für Blog, Dokumentation oder CMS-ähnliche Inhalte. Ermöglicht:
- Type-Safety durch definierte Schemas
- Einfaches Hinzufügen neuer Inhalte per Markdown/MDX
- Automatische Generierung von Übersichtsseiten

### `lib/` und `data/`
- **lib/**: Pure Functions, keine UI. Gut testbar.
- **data/**: Strukturierte Daten getrennt vom Code. Einfach zu pflegen.

---

## Konventionen für Wartbarkeit

1. **Ein Komponente = Eine Datei** – Keine zu großen Monolithen
2. **Konsistente Benennung** – PascalCase für Komponenten, kebab-case für Dateien
3. **Props dokumentieren** – JSDoc oder TypeScript-Interfaces für Komponenten
4. **Keine Magie** – Konstanten in `constants.ts`, nicht hardcoded
5. **Content Collections** – Für wiederkehrende Inhalte statt manueller Seiten

---

## Minimale Startstruktur (für dieses Projekt)

Falls du schrittweise vorgehen möchtest, hier die **minimalen Ergänzungen** zur aktuellen Struktur:

```
src/
├── components/
│   ├── ui/          # Neu: für generische Komponenten
│   └── layout/      # Neu: Navigation, Footer hier
├── lib/
│   └── constants.ts # Neu: z.B. Site-Metadaten
├── data/
│   └── navigation.ts # Neu: Menü-Struktur zentral
└── ... (Rest wie bisher)
```

Diese Struktur lässt sich bei Bedarf erweitern, ohne später umbauen zu müssen.
