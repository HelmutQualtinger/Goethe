# Johann Wolfgang von Goethe — Leben und Werk

Interaktive Biographie und Werkübersicht zu Johann Wolfgang von Goethe (1749–1832), umgesetzt als immersive Webseite und Projektions-Slideshow.

## Dateien

| Datei | Beschreibung |
|---|---|
| `index.html` | Scroll-Website — vollständige Biographie, Werkübersicht, Gedichte (Volltexte), Zitate, 3D-Animationen |
| `slideshow.html` | Präsentations-Slideshow — 26 Folien, optimiert für Beamer-Projektion |

## index.html — Scroll-Website

Einzel-HTML-Datei mit eingebettetem CSS und JavaScript. Museumsstil-Design in Weimarer-Klassik-Farben (Dunkelgrün, Gold, Creme, Burgunder).

**Inhalte:**
- 6 Biographie-Kapitel (Kindheit, Studium, Sturm und Drang, Weimar/Italien, Klassik/Spätwerk, Tod)
- 12 Werke mit Beschreibungen (Werther, Faust I & II, Wilhelm Meister, Divan, Iphigenie, Tasso, u.a.)
- 6 Gedichte mit Auszügen (Erlkönig, Zauberlehrling, Prometheus, Wandrers Nachtlied, u.a.)
- **Erlkönig** und **Der Zauberlehrling** als Volltext mit Sprecherbezeichnungen
- Zitate durchgehend eingestreut
- Naturwissenschaft-Sektion (Farbenlehre, Morphologie)

**Features:**
- 3D-Buch-Animation (CSS 3D Transforms, Mausinteraktion)
- Parallax-Effekte
- Scroll-triggered Reveal-Animationen
- Schreibfeder-Typewriter-Animation
- Schwebende Textelemente
- Rotierende Farbenlehre-Visualisierung
- Responsive Design

## slideshow.html — Präsentations-Slideshow

26 Folien, optimiert für Fernlesbarkeit bei Projektion.

**Navigation:**
- `←` `→` — Folien wechseln
- `Leertaste` — Nächste Folie (auf Gedicht-Folien: Vorlesung starten/stoppen)
- `↑` `↓` — Gedicht-Text scrollen
- `Mausrad` — Folien wechseln / Gedichte scrollen
- `Klick` — Linkes Drittel = zurück, Rest = weiter
- `Swipe` — Touch-Navigation
- `F` — Vollbild
- `Tab` — Seitenleiste ein/aus
- `Esc` — Vorlesung stoppen
- `Home` / `End` — Erste / letzte Folie

**Seitenleiste:**
- Erscheint wenn die Maus an den linken Bildschirmrand fährt
- Alle 26 Folien mit Titel und Typ-Label
- Direkte Navigation per Klick
- Aktive Folie hervorgehoben

**Vorlesung (Text-to-Speech):**
- Erlkönig mit verschiedenen Stimmen:
  - *Erzähler* — weiblich, ruhig
  - *Vater* — männlich, tief, beruhigend
  - *Sohn* — weiblich/hoch, ängstlich
  - *Erlkönig* — männlich, sehr tief, langsam, unheimlich
- Zauberlehrling mit steigender Panik (Tempo und Tonhöhe erhöhen sich)
- Meister-Stimme tief und autoritär
- Automatisches Highlighting und Scrollen der aktiven Strophe
- Dramatische Pausen zwischen Strophen
- Nutzt die auf dem System verfügbaren deutschen Stimmen (macOS: Anna, Markus, etc.)

## Technologie

- Reines HTML/CSS/JavaScript — keine Build-Tools, keine Abhängigkeiten
- Google Fonts: Playfair Display, Cormorant Garamond, EB Garamond
- CSS 3D Transforms, CSS Animationen, IntersectionObserver
- Web Speech API für Vorlesung
- Getestet in Chrome, Safari, Firefox

## Nutzung

Einfach `index.html` oder `slideshow.html` im Browser öffnen:

```
open index.html
open slideshow.html
```

Für die Slideshow-Projektion empfohlen: `F` für Vollbild drücken.