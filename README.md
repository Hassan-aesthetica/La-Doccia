# La Doccia — Website Quellpaket

Dies ist die bearbeitbare Version der Website. Sie ist bewusst **schlank**:
Die HTML-Datei ist nur ~100 KB, alle Bilder/Videos liegen als echte Dateien
im Ordner `assets/`. So bleibt das Projekt in einem Code-Chat oder Editor
handhabbar (die alte „alles-in-einem" HTML war 3,7 MB und dafür ungeeignet).

## Struktur

```
la-doccia-source/
├── index.html            ← die Website (bearbeite HAUPTSÄCHLICH diese Datei)
├── assets/               ← alle Bilder, Videos, Poster
│   ├── manifest.json     ← Zuordnung: interner Name → Dateiname
│   ├── *.webp            ← Produkt- und Sektionsbilder
│   ├── hero.mp4 / .webm  ← Hero-Video (als video / videowebm)
│   └── poster.webp        ← Standbild des Videos
├── logo_paths.json       ← Vektorpfade der Wortmarke „LA DOCCIA" (im HTML eingebettet genutzt)
├── ral.json              ← Daten der Farbwelt-Sektion
└── README.md
```

## Lokal ansehen

Wegen der externen Dateien braucht es einen kleinen lokalen Server
(direktes Öffnen per Doppelklick blockiert das Laden der Assets):

```bash
cd la-doccia-source
python3 -m http.server 8000
# dann im Browser: http://localhost:8000
```

## Wie die Bilder eingebunden sind

Im `<script>` steht `const A = { ... }` — ein Objekt, das jeden Bildnamen
auf seinen Dateipfad mappt (z. B. `"towelStack": "assets/towelStack.webp"`).
Im Code wird `src('towelStack')` benutzt, um das Bild zu laden.
Neues Bild hinzufügen: Datei in `assets/` legen und in `A` eine Zeile ergänzen.

## Produkte bearbeiten

Die Produktliste ist das Array `const P = [ ... ]` im `<script>`.
Die Kategorien stehen darüber in `const CATS = [ ... ]`.
Jedes Produkt hat: id, cat (Kategorie), sc (Unterkategorie), n (Name),
p (Preis), optional old (Streichpreis), img + img2 (zwei Bilder für Hover-Wechsel),
r (Bewertung), rv (Anzahl), badge, d (Beschreibung).

## Deployment (z. B. Vercel, Netlify)

Den ganzen Ordner `la-doccia-source/` hochladen — `index.html` ist der Einstieg.
Kein Build-Schritt nötig, es ist reines HTML/CSS/JS.

## Noch offen (vom Kunden zu liefern)

- Echte Preise der neuen Produkte (aktuell plausibel geschätzt)
- Rechtstexte: Telefon, E-Mail, UID/Kleinunternehmer-Angabe in Impressum/Datenschutz/AGB/Widerruf
  (im Code als gelb markierte Platzhalter)
- Vor Live-Gang: Impressum/AGB über WKO-Generator, Shop-Teil über IT-Recht Kanzlei prüfen lassen
