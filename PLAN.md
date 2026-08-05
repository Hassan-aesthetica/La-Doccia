# PLAN — Shop-Upgrade La Doccia

## Ist-Zustand (Phase 1: Bestandsaufnahme)

- **Stack:** Eine statische `index.html`, Vanilla JS, kein Framework, kein Build-Tool, kein Backend. Views (`v-home`, `v-shop`, Rechtsseiten …) werden per JS umgeschaltet.
- **Produkte:** Hardcoded im Array `P` (22 Produkte), Kategorien in `CATS` (6 Stück: Bad & Frottee, Haarpflege, Körperpflege, Duft & Parfüm, Taschen & Accessoires, Armaturen).
- **Datenmodell pro Produkt (vorher):** `id, cat, sc, n, p, old?, img, img2, r, rv, badge?, d, x, colors?`
- **Warenkorb:** In-Memory-Array `CART`, Drawer, Mengenrabatt (2 → 10 %, 3 → 15 %), Versandfrei ab 79 €. Kein Checkout (Demo-Toast), keine Persistenz.
- **Styling:** Design-Tokens als CSS-Variablen in `:root`, kein externes CSS-System.
- **Payment/E-Mail:** Nicht vorhanden. Demo-Seite.

## Abwägung: Was aus dem Auftrag übernommen wird — und was nicht

Der Auftrag ist für einen Bademode-Shop mit Framework-Stack und Backend geschrieben.
Dieses Projekt ist eine statische Demo-Site mit anderem Sortiment. Entscheidungen:

### Umgesetzt (hoher Conversion-Hebel, hier sauber machbar)
| Maßnahme | Begründung |
|---|---|
| Zentrale Promo-Config (`PROMO`) | Alle Rabatt-/Versandregeln an einer Stelle, Stapel-Logik definiert (höherer Rabatt gewinnt, Gratisversand stapelt immer) |
| Warenkorb-Persistenz (localStorage) | Standard; Abbrecher verlieren den Korb nicht |
| Gutscheinfeld (einklappbar) + funktionierender Code DOCCIA10 | Rabatt wird real gerechnet; eingeklappt, damit niemand zum Code-Googeln rausgeht |
| Cross-Sells im Warenkorb (max. 3, ≤ 30 % des Korbwerts) | Stärkster AOV-Hebel |
| Gratisversand-Bestätigung bei Erreichen | Belohnungsmoment |
| Staffel-Hinweis auf der Produktseite (Preis/Stück-Tabelle) | Mengenrabatt wirkt nur, wenn man ihn vor dem Warenkorb sieht |
| Grundpreis (€/100 ml bzw. /100 g) auf Karte + PDP | **Gesetzliche Pflicht** bei Pflegeprodukten (PAngV) |
| Streichpreis-Referenz „niedrigster Preis der letzten 30 Tage" | **Gesetzliche Pflicht** (PAngV §11) |
| Größenwahl (Bademäntel) als Buttons, Warenkorb variantenfähig | Pflicht für Textil-Bestellbarkeit |
| Konkrete Lieferzeit („Lieferung Do, 6. – Mo, 10. August") | Konkretheit konvertiert besser als „schnell" |
| „Wird oft zusammen gekauft" (Bundle, echte Mengenrabatt-Rechnung) | AOV-Hebel, transparent gerechnet — keine Fake-Ersparnis |
| Wunschliste (Herz, localStorage, eigene Ansicht) | Standard-Widget, Rückkehr-Anker |
| „Zuletzt angesehen" (Shop-Seite unten) | Discovery ohne Homepage vollzustellen |
| Kategorie-Kacheln als Shop-Einstieg | Abteilungs-Einstieg wie gefordert — mit den 6 echten Kategorien |
| Suche: Synonyme, Tippfehlertoleranz, Autosuggest mit Bildern, Kein-Treffer-Seite | Suchende kaufen überdurchschnittlich oft |
| Shop-Dropdown im Header (Desktop) + Kategorien im Mobilmenü | Max. 2 Klicks zu jeder Kategorie |
| Accordion auf PDP (Details/Material, Versand & Rückgabe) | Material = Textilkennzeichnungspflicht |
| Sticky Kaufleiste im Produkt-Modal (mobil) | Mobile Conversion |
| `track()`-Stub mit GA4-Event-Namen | Vorbereitet, feuert nur in `dataLayer` — kein Tracking ohne Consent-System |
| Popup erst nach 22 s | Auftrag: 20–30 s; bleibt max. 1× pro Besucher (Vorgabe des Kunden) |

### Bewusst NICHT umgesetzt (mit Grund)
| Punkt aus dem Auftrag | Grund |
|---|---|
| Damen/Herren/Kinder-Abteilungen | Sortiment ist Bad-Interieur + Accessoires, keine Bademode. Die 6 echten Kategorien SIND die Abteilungen. Fantasie-Abteilungen wären leer. |
| Mega-Menü mit Bildspalten | Bei 6 Kategorien Overkill; schlankes Dropdown reicht und lädt schneller |
| Größen-Lagerbestand, „Benachrichtigen wenn wieder da", Restbestands-Badges | Keine echten Bestandsdaten vorhanden — Auftrag verbietet erfundene Knappheit ausdrücklich |
| Double-Opt-In, Warenkorbabbruch-Mail, E-Mail-Dienst | Braucht Backend/E-Mail-Provider → `OFFEN.md` |
| Echter Checkout/Payment | Kein Backend → `OFFEN.md` |
| Cookie-Banner | Es lädt kein einziges Tracking-/Drittskript (nur Google Fonts). Ein Banner ohne Gegenstand wäre Consent-Theater. Nötig, sobald echtes Tracking kommt → `OFFEN.md` |
| Filter-Zustand in der URL, paginierte SEO-URLs | Single-Page-Demo ohne Router; bei 22 Produkten keine Pagination nötig |
| Bewertungs-Fotos, Sterne-Filter | Keine echten Bewertungsdaten einzelner Käufe vorhanden |
| Produktfinder-Quiz, Shop-the-Look, Journal | Contentaufwand steht bei 22 Produkten nicht im Verhältnis; Kandidat für später |
| Skeleton-Loader | Daten sind lokal, Rendering ist synchron — es gibt nichts zu überbrücken |
| Du-Form | Bestehende Site ist durchgehend Sie-Form; Konsistenz schlägt Vorgabe |

## Neue Produktfelder
`ml` (Füllmenge), `g` (Gewicht Kerze), `sizes[]` (Bademäntel), `mat` (Material, Textilpflicht), `rel[]` (redaktionelle Empfehlungen). Grundpreis wird berechnet, nicht gepflegt. EdP ist vom Grundpreis ausgenommen (klassisches Parfüm), Sets ebenfalls (verschiedene Produkte).

## Annahmen
- AOV unbekannt → Gratisversand-Schwelle bleibt bei 79 € (bestehende Kommunikation), Staffel 2/3 Artikel bleibt.
- `old`-Preise werden als „niedrigster Gesamtpreis der letzten 30 Tage" interpretiert und so ausgezeichnet. Echte Preishistorie: `OFFEN.md`.
- Bestseller-Badges sind redaktionell (keine Verkaufsdaten) — als solche ok, keine erfundenen Zahlen daneben.
