# Projektrezension: Johann Wolfgang von Goethe — Leben und Werk

## Gesamtbewertung: 8,5 / 10

Ein ambitioniertes, handwerklich solides Projekt, das Goethes Leben und Werk in drei Ausgabeformaten aufbereitet — als immersive Scroll-Website, Beamer-Slideshow und PDF-Handout. Die inhaltliche Tiefe ist bemerkenswert, das visuelle Design hebt sich deutlich von generischen Webprojekten ab.

---

## 1. Inhalt und Texte — 9/10

**Stärken:**
- Die Biographie ist ausführlich, gut recherchiert und stilistisch auf hohem Niveau geschrieben. Die Sprache trifft einen Ton zwischen wissenschaftlicher Genauigkeit und literarischer Eleganz, der dem Gegenstand angemessen ist.
- Familienverhältnisse (Christiane Vulpius, Cornelia, August, Enkel) sind ungewöhnlich detailliert dargestellt — weit über das hinaus, was typische Goethe-Darstellungen bieten.
- Die Werkbeschreibungen (12 Werke) sind prägnant und informativ, mit historischer Einordnung und Wirkungsgeschichte.
- Erlkönig und Zauberlehrling liegen als Volltext vor, mit korrekten Strophen und Sprecherbezeichnungen.
- Zitate sind geschickt über das gesamte Projekt verteilt und strukturieren den Erzählfluss.

**Schwächen:**
- Die Gedichtsektion (Lyrik und Balladen) zeigt nur Auszüge/Beschreibungen der meisten Gedichte. Prometheus, Wandrers Nachtlied und Willkommen und Abschied verdienen ebenfalls den Volltext.
- Die Naturwissenschafts-Sektion ist etwas kurz im Verhältnis zu Goethes tatsächlichem Engagement (Mineralogie, Meteorologie, Osteologie nur in einem Satz erwähnt).
- Es fehlt ein Abschnitt über Goethe als Zeichner und bildender Künstler (über 2.600 Zeichnungen).

---

## 2. index.html — Scroll-Website — 8,5/10

**Stärken:**
- Durchdachtes Farbschema in Weimarer-Klassik-Farben (Dunkelgrün, Gold, Creme, Burgunder) — kohärent und stimmungsvoll, kein generisches Design.
- Exzellente Typographie: Playfair Display, Cormorant Garamond und EB Garamond ergeben eine harmonische Serif-Kombination, die zum Thema passt.
- CSS-Variablen konsequent eingesetzt (33 Variablen in `:root`), was Theming und Wartbarkeit erleichtert.
- Scroll-triggered Reveal-Animationen via IntersectionObserver — performant und dezent.
- 3D-Buch-Animation mit Mausinteraktion (CSS 3D Transforms + requestAnimationFrame) ist ein gelungenes interaktives Element.
- Schwebende Textelemente (Werktitel) im Hero-Bereich erzeugen Tiefe.
- Rotierende Farbenlehre-Visualisierung als reines CSS — clever und thematisch passend.
- Dark/Light Theme mit localStorage-Persistenz funktioniert zuverlässig.
- Ladebildschirm mit animiertem Ornament statt generischem Spinner.

**Schwächen:**
- 93 KB in einer einzigen HTML-Datei. Für eine Einzelseite akzeptabel, aber die Wartbarkeit leidet (2.484 Zeilen).
- Noise-Overlay (`body::after` mit SVG feTurbulence) bei z-index 9999 kann auf schwächerer Hardware Rendering-Probleme verursachen. Dasselbe Overlay wurde in der Slideshow bereits entfernt — sollte hier ebenfalls evaluiert werden.
- Die Navigation (`nav .nav-links`) verschwindet auf kleinen Bildschirmen nicht hinter einem Hamburger-Menü — auf Mobilgeräten unter 768px werden die Links abgeschnitten oder überlappen.
- Keine `<meta name="description">` oder Open-Graph-Tags für SEO/Social-Media-Sharing.
- Kein `lang`-Attribut auf Abschnittsebene, aber `html lang="de"` ist korrekt gesetzt.
- `font-display: swap` fehlt bei den Google-Fonts-Importen (implizit durch `&display=swap` im URL gelöst — korrekt).

**Code-Qualität:**
- CSS ist sauber strukturiert mit Abschnitts-Kommentaren (`═══ SECTION NAME ═══`).
- JavaScript ist in einem IIFE gekapselt, `'use strict'` gesetzt — gute Praxis.
- Passive Event-Listener für Scroll-Events korrekt eingesetzt.
- Keine externen Abhängigkeiten außer Google Fonts — gute Entscheidung für Langlebigkeit.

---

## 3. slideshow.html — Präsentations-Slideshow — 9/10

**Stärken:**
- 29 Folien, sauber strukturiert mit `data-index`-Attributen und semantischen CSS-Klassen.
- Hervorragende Navigationsoptionen: Tastatur (Pfeiltasten, Leertaste, Home/End), Maus (Klick-Zonen, Mausrad), Touch (Swipe), Vollbild (F-Taste).
- Seitenleiste mit allen 29 Folien, Typ-Labels und aktiver Folie — erscheint bei Mausbewegung zum linken Rand. Durchdacht implementiert mit mouseenter/mouseleave und Timeouts.
- Text-to-Speech mit rollendifferenzierten Stimmen ist das Highlight des Projekts:
  - Erlkönig mit vier distinkt konfigurierten Stimmen (Erzähler, Vater, Sohn, Erlkönig) — unterschiedliche Pitch- und Rate-Werte erzeugen tatsächlich unterscheidbare Charaktere.
  - Zauberlehrling mit progressiver Panik (Tempo und Tonhöhe steigen mit fortschreitender Strophe) — ein cleveres Detail.
  - Automatisches Highlighting und Scrollen der aktiven Strophe.
  - Meister-Stimme tief und autoritär als Kontrast.
- Scrollbare Biographie-Folien (`getScrollableArea()`) lösen das Problem langer Texte auf fixierten Slides elegant.
- Custom Cursor (Gold-Ring) passend zum Gesamtdesign.
- Progress-Bar am unteren Rand zeigt den Fortschritt innerhalb der Präsentation.
- Clean Slide-Backgrounds nach Entfernung der problematischen Noise-Textur.

**Schwächen:**
- Die `slideMeta`-Array-Einträge (Zeile 2050–2079) müssen manuell mit den HTML-Slides synchron gehalten werden. Ein Refactoring, das die Metadaten aus den Slide-Elementen selbst extrahiert, wäre robuster.
- `cursor: none` auf `html, body` versteckt den System-Cursor zugunsten des Custom-Cursors — auf Touchscreens und bei deaktiviertem JavaScript sieht der Nutzer gar keinen Cursor.
- Die Funktion `getScrollableArea()` prüft `scrollHeight > clientHeight + 5` — der Magic-Number-Schwellwert von 5px ist fragil.
- Monkey-Patching von `updateUI` (Zeile 2162: `const origUpdateUI = updateUI; updateUI = function() {...}`) statt einer sauberen Event-basierten Architektur.
- Einige Click-Handler verwenden `e.stopPropagation()` statt gezielter Event-Delegation.

**Code-Qualität:**
- Gut strukturierter JavaScript-Code mit klaren Abschnitts-Kommentaren.
- Voice-Discovery-Logik ist robust und fällt auf verfügbare Stimmen zurück.
- Stagger-Animationen über CSS-Klassen (`stagger-1` bis `stagger-5`) sind eine elegante Lösung.

---

## 4. handout.md / handout.pdf — 7/10

**Stärken:**
- Vollständiger Inhalt: alle Biographie-Kapitel, Werkübersicht, beide Gedichte im Volltext, Lebensstationen-Tabelle.
- Goethe-Portrait mit `minipage`-Layout im PDF (1/3 Breite neben Text) — optisch ansprechend.
- Gedichte korrekt formatiert mit Zeilenumbrüchen und Sprecherbezeichnungen in Fettdruck.

**Schwächen:**
- Das `minipage`-LaTeX im Markdown bricht die Portabilität: Die Datei rendert nur mit pandoc + xelatex korrekt, nicht in GitHub, VS Code Preview oder anderen Markdown-Renderern. Der LaTeX-Block erscheint dort als Rohtext.
- Abhängigkeit von externer `header.tex` (für `\usepackage{graphicx}`) ist ein versteckter Build-Parameter, der leicht vergessen wird.
- Die Lebensstationen-Tabelle ist eine einfache Markdown-Tabelle — im PDF funktioniert sie, aber bei sehr vielen Einträgen könnte sie über Seitenumbrüche brechen.
- Kein Inhaltsverzeichnis (`--toc` fehlt im pandoc-Befehl) — bei 460 Zeilen wäre eines hilfreich.

---

## 5. Projektstruktur und Dokumentation — 8/10

**Stärken:**
- README.md ist umfassend: Dateibeschreibungen, Feature-Listen, Tastatur-Shortcuts, pandoc-Befehl, Technologie-Stack.
- CLAUDE.md enthält nützliche Entwickler-Hinweise (Re-Indexing-Script, Konventionen, Dateigrößen).
- Keine Build-Tools, keine node_modules, keine Abhängigkeiten — das Projekt funktioniert durch einfaches Öffnen der HTML-Dateien. Diese Einfachheit ist eine bewusste und gute Architekturentscheidung.

**Schwächen:**
- Kein `.gitignore` (z.B. für `.DS_Store`, `*.pdf` falls gewünscht, Backup-Dateien).
- `header.tex` ist eine isolierte Hilfsdatei ohne Kontext — sollte im README oder CLAUDE.md dokumentiert sein.
- Kein Lizenzhinweis für das Goethe-Portrait (zwar gemeinfrei, aber eine explizite Angabe im Repository wäre sauberer).

---

## 6. Design und Ästhetik — 9/10

Das visuelle Design ist der größte Pluspunkt des Projekts. Die Weimarer-Klassik-Farbpalette, die sorgfältige Typographie und die dezenten Animationen erzeugen eine Atmosphäre, die an eine Museumsausstellung erinnert — genau das, was für einen Goethe-Tribute angemessen ist.

**Besonders gelungen:**
- Die Farbvariablen-Namen (`--cream`, `--gold`, `--green-deep`, `--burgundy`, `--ink`) lesen sich fast poetisch und machen die Designintention transparent.
- Dark Theme der Slideshow ist für Beamer-Projektion optimiert — eine praktische Entscheidung.
- Die Transition zwischen Light und Dark Theme ist sanft (0.5s ease) und nicht abrupt.

**Verbesserungspotenzial:**
- In der Slideshow ist der Light-Theme-Override (`!important` auf allen Slides) ein grober Keil. Besser wäre es, die CSS-Variablen sauber zu invertieren, wie es in index.html gemacht wird.
- Die Gedicht-Folien (Erlkönig, Zauberlehrling) sind die visuell stärksten Slides — die reinen Biographie-Folien könnten von ähnlichem visuellen Einsatz profitieren (dezente Hintergrund-Illustrationen, Jahreszahlen als große Typographie-Elemente).

---

## 7. Technische Bewertung

| Kategorie | Note | Kommentar |
|-----------|------|-----------|
| HTML-Semantik | 7/10 | Grundstruktur korrekt, aber kaum `<article>`, `<aside>`, `<figure>` — überwiegend `<div>` und `<section>` |
| CSS-Architektur | 8/10 | Variablen-System, kein Framework, saubere Kaskade — aber Spezifitäts-Eskalation (`!important`) an einigen Stellen |
| JavaScript | 8/10 | IIFE, strict mode, passive listeners, IntersectionObserver — modern und performant |
| Barrierefreiheit | 5/10 | Kein `aria-label` auf interaktiven Elementen, `cursor: none` problematisch, kein `prefers-reduced-motion`, keine Skip-Links, Kontraste im Light Theme teilweise grenzwertig |
| Performance | 8/10 | Keine externen JS-Bibliotheken, CSS-Animationen statt JS wo möglich, passive Scroll-Listener. Aber: unkomprimierte 93KB HTML, kein Lazy-Loading für das Portrait-Bild |
| Responsive Design | 6/10 | `clamp()` für Schriftgrößen, aber keine echten Breakpoints für die Navigation, Werke-Grid und Gedichte-Grid auf kleinen Bildschirmen |
| Browser-Kompatibilität | 8/10 | Getestet in Chrome, Safari, Firefox. Webkit-Prefixes vorhanden. Web Speech API hat variierende Unterstützung |

---

## 8. Empfehlungen

### Kurzfristig (Quick Wins)
1. `.gitignore` hinzufügen
2. `prefers-reduced-motion` Media Query einbauen, um Animationen für empfindliche Nutzer zu deaktivieren
3. `aria-label` auf Theme-Toggle, Slideshow-Navigation und Play-Buttons
4. Pandoc-Befehl mit `-H header.tex` in README dokumentieren
5. Responsive Navigation (Hamburger-Menü) für Mobilgeräte in index.html

### Mittelfristig
6. Slide-Metadaten aus `data-*`-Attributen der HTML-Elemente generieren statt manueller Array-Pflege
7. `minipage`-LaTeX im Markdown durch pandoc-native Bildeinbettung ersetzen (Portabilität)
8. Inhaltsverzeichnis im PDF-Handout aktivieren (`--toc`)
9. Weitere Gedichte im Volltext ergänzen (Prometheus, Wandrers Nachtlied)

### Langfristig
10. CSS-Module oder Scoped Styles evaluieren, falls das Projekt wächst
11. Lighthouse-Audit durchführen und Score optimieren
12. Print-Stylesheet für index.html erstellen

---

## Fazit

Ein beeindruckendes Einzelprojekt, das zeigt, was mit reinem HTML/CSS/JavaScript ohne Build-Tools und Frameworks möglich ist. Die inhaltliche Qualität der Goethe-Biographie übertrifft viele Wikipedia-Artikel, das visuelle Design hat Charakter und Wiedererkennungswert, und die TTS-Vorlesung mit rollenspezifischen Stimmen ist ein originelles Feature, das den Text lebendig macht.

Die Hauptschwächen liegen in der Barrierefreiheit und im responsiven Design — beides Bereiche, die mit vertretbarem Aufwand deutlich verbessert werden könnten. Die Entscheidung gegen externe Abhängigkeiten zahlt sich in Langlebigkeit und Einfachheit aus: Das Projekt wird in zehn Jahren noch genauso funktionieren wie heute.

*»Was man nicht versteht, besitzt man nicht.«* — Dieses Projekt zeigt, dass der Autor seinen Gegenstand versteht.