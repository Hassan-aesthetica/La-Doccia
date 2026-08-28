# UEBERGABE — Shop-Upgrade La Doccia

Alles Folgende lebt in `index.html` (eine Datei, Vanilla JS, kein Build nötig).
Lokal ansehen: `python3 -m http.server` im Projektordner.

## Was gebaut wurde

**Navigation & Discovery**
- Shop-Dropdown im Header (Desktop, Hover) und Kategorie-Punkte im Mobilmenü — jede Kategorie in max. 2 Klicks
- Kategorie-Kacheln mit Bild und Artikelzahl als Shop-Einstieg
- „Zuletzt angesehen" (localStorage, max. 8) unten auf der Shop-Seite
- Wunschliste: Herz auf jeder Karte und Header-Icon mit Zähler, eigene Seite, persistent

**Suche**
- Live-Filterung + Autosuggest ab 2 Zeichen (Produkte mit Bild und Preis, Kategorie-Chips)
- Deutsche Synonyme (`SYN`-Liste im Script) und Tippfehlertoleranz (Levenshtein)
- Kein-Treffer-Seite mit Hinweis + „Beliebt bei unseren Kunden"
- Jede Suche ≥ 3 Zeichen landet als `search`-Event im dataLayer

**Produktseite (Modal)**
- Grundpreis (automatisch aus `ml`/`g`), 30-Tage-Bestpreis-Hinweis am Streichpreis
- Konkrete Lieferzeit (2–4 Werktage, Wochenenden übersprungen), Versandkosten-Link
- Größen-Buttons (Bademäntel) mit Pflicht-Auswahl; Größe läuft bis in den Warenkorb
- Mengenrabatt-Staffel als Preis-pro-Stück-Tabelle (rechtskonform, keine „statt"-Preise)
- „Wird oft zusammen gekauft": 3er-Bundle, Ersparnis = echter 15-%-Mengenrabatt, transparent beschriftet
- Accordions „Details & Material" (Textilkennzeichnung) und „Versand & Rückgabe"
- Sticky Kaufleiste am unteren Rand (mobil)
- „Passt dazu": redaktionelle Empfehlungen (`rel`) zuerst, dann gleiche Kategorie — nie leer

**Warenkorb**
- Persistiert über Reloads (localStorage `ld_cart`)
- Bis zu 3 Cross-Sells („Passt zu Ihrer Bestellung"), je ≤ 30 % des Korbwerts, Ein-Klick-Add
- Einklappbares Gutscheinfeld; DOCCIA10 rechnet real
- Rabattlogik: Neukundencode und Mengenrabatt stapeln sich nicht — der höhere gewinnt, mit sichtbarem Hinweis; Gratisversand stapelt immer
- „Gratisversand erreicht ✓"-Bestätigung, Fortschrittstexte mit konkretem Restbetrag

**Sonstiges**
- `track()`-Stub: GA4-Eventnamen (`view_item`, `add_to_cart`, `begin_checkout`, `search`, …) in `window.dataLayer` — ohne externes Skript
- Newsletter-Popup: frühestens nach 22 s, maximal 1× pro Besucher

## Wo wird was konfiguriert?

| Was | Wo in `index.html` |
|---|---|
| Versandschwelle, Versandkosten, Staffeln, Gutscheincode | `const PROMO = {...}` (eine Stelle, alles andere leitet sich ab — auch Drawer-Beschriftungen) |
| Produkte | Array `const P = [...]` |
| Kategorien | Array `const CATS = [...]` |
| Such-Synonyme | `const SYN = [...]` |
| Kuratierte Kollektionen (Sale, Neuheiten, Sommer, Sets, Farben) | `const COLL = {...}` — Titel, Bild, Filter je Kachel; Sale-Prozentsatz wird aus echten Preisen berechnet (`maxSale()`) |
| Logo-Farbpaletten | `const SQPAL = [...]` |
| Startseiten-Produkte | `const FEATURED = [...]` |

## Neues Produkt korrekt anlegen

Pflichtfelder: `id, cat, sc, n, p, img, img2, r, rv, d`
- **Pflegeprodukt?** → `ml:` (oder `g:`) setzen — der Grundpreis erscheint dann automatisch auf Karte und Produktseite. Ausnahmen (EdP, Sets aus verschiedenen Produkten): Feld einfach weglassen.
- **Streichpreis `old`?** → muss der **niedrigste Gesamtpreis der letzten 30 Tage** sein, nichts anderes.
- **Textil?** → `mat:` mit Materialzusammensetzung (Pflicht).
- **Mit Größen?** → `sizes:['S','M','L','XL']` — Karte zeigt dann „Größe wählen", Modal erzwingt die Auswahl.
- **Empfehlungen:** `rel:['id1','id2','id3']` — steuert „Passt dazu", Bundle und Warenkorb-Cross-Sells.
- `x:` „Gut zu wissen"-Text (Pflege/Anwendung/Saison).

## Produktkatalog (Stand August 2026)
Das Sortiment (60 Produkte `p01`–`p60` + 10 Sets `S1`–`S10`) kommt aus dem Google-Drive-Katalog
(Ordner `produkte/` und `sets/`). Dateikonvention: `<nr>_<produkt>_<perspektive>.webp` —
`_a` Packshot (Grid/Warenkorb), `_b` Detail (Galerie), `_c` Szene (Galerie/Kategorie-Header).
Die Bilder liegen unter `assets/p/` und `assets/s/`; Produkte referenzieren sie direkt als Pfad
(`src()` hat einen Fallback: unbekannte Keys werden als Pfad durchgereicht).
Preise, Bewertungen und Texte sind plausible Platzhalter — vor Livegang mit echten Daten abgleichen.

## Hinweis zu den Bildern
Vier Asset-Dateien tragen vertauschte Namen (Taschen liegen in `shampoo.webp`, Kerzen in `bagsSet.webp`, Handtücher in `candles3.webp`, ein Pflege-Set in `towelStack.webp`). Das ist im Bild-Mapping `A` am Anfang des Scripts korrigiert — beim Ersetzen der Platzhalter-Bilder vor dem Livegang am besten die Dateien richtig benennen und die vier Korrekturzeilen entfernen.

## Was bewusst nicht umgesetzt wurde
Siehe `PLAN.md` (Abwägungstabelle) und `OFFEN.md` (Lücken inkl. dessen, was der Kunde liefern muss).
