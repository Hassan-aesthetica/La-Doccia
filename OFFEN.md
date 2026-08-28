# OFFEN — was noch fehlt und warum

Diese Punkte sind mit der aktuellen statischen Seite (kein Backend, kein E-Mail-Dienst,
keine Bestandsdaten) nicht sauber umsetzbar und wurden bewusst NICHT als Attrappe gebaut.

## Braucht ein Backend / einen Dienst
- **Echter Checkout & Payment** (Stripe/PayPal/Shop-System). Der „Zur Kasse"-Button ist als Demo gekennzeichnet und feuert `begin_checkout` in den dataLayer.
- **Newsletter Double-Opt-In**: Aktuell wird der Code DOCCIA10 direkt angezeigt. Rechtlich sauber ist: E-Mail → neutrale Bestätigungsmail → erst nach Klick der Code. Braucht Brevo/Klaviyo/Mailchimp + Protokollierung (Zeitpunkt, IP). Das Gutscheinfeld im Warenkorb akzeptiert den Code bereits und rechnet ihn korrekt — die „einmal pro Kunde"-Durchsetzung geht erst serverseitig.
- **Warenkorbabbruch-Mail**: erst nach E-Mail-Anbindung.
- **Suchbegriff-Logging**: Events liegen im `dataLayer` (`search`), brauchen ein Analytics-Ziel.

## Braucht echte Daten
- **Bestand je Größe / „Benachrichtigen, wenn wieder da"**: keine Lagerdaten vorhanden. Keine Fake-Knappheit eingebaut (Vorgabe).
- **Preishistorie**: `old` wird derzeit als „niedrigster Gesamtpreis der letzten 30 Tage" ausgezeichnet und muss vom Betreiber genau so gepflegt werden. Sobald Preise sich ändern, echte Historie führen (Feld `preis_historie` + `getReferenzpreis()`).
- **Bestseller-Badges**: redaktionell. Bei echten Verkaufsdaten datenbasiert vergeben.
- **Bewertungen**: aggregierte Werte sind redaktionelle Demo-Daten; einzelne Kundenbewertungen mit Fotos brauchen ein Review-System.
- **Produktangaben prüfen**: Duftöl-Anteile, Materialangaben, Füllmengen und Grundpreise sind plausible Platzhalter — vor Livegang mit echten Produktdaten abgleichen (Textilkennzeichnung & PAngV sind Pflicht!).

## Bewusst zurückgestellt
- **Cookie-Banner**: Die Seite lädt außer Google Fonts nichts von Dritten und setzt kein Tracking. Sobald GA4/Meta-Pixel o. ä. eingebunden wird: Consent-Tool davor schalten, `track()` erst nach Einwilligung an das Ziel weiterreichen. (Google Fonts idealerweise lokal hosten — dann ist auch das erledigt.)
- **Filter-Zustand in der URL**: Single-Page ohne Router. Bei Umzug auf ein Framework/Shop-System nachziehen.
- **Produktfinder-Quiz, Shop-the-Look, Journal/SEO-Artikel**: lohnt ab größerem Sortiment bzw. wenn Content produziert wird.

## Aus dem Gespräch mit Oleg — wartet auf Zulieferung
- **Telefonnummer**: Im Header, Mobilmenü und Beratungsformular steht der Platzhalter „01 555 01 00" (`tel:+4315550100`) — durch die echte Nummer ersetzen (3 Stellen in `index.html` suchen: „5550100").
- **Glas-Lieferanten-Link** (kommt per WhatsApp): daraus 5 echte Farbtöne für den Dusch-Farbwähler wählen — aktuell Weiß & Creme, Blassgrün, Taubenblau, Pastellviolett, Braunrot (`LINECOLORS` im Script, mit ral-Beispielbildern hinterlegt).
- **Rahmen-Foto für die Quadrate** (kommt per WhatsApp): Rahmen-Variante des Logos testen.
- **Thermochrome Quadrate** (Farbe wechselt mit Temperatur): als Produkt-Story/USP-Modul einbauen, sobald es real ist — nichts versprechen, was noch nicht existiert.
- **Kinder-Kategorie**: In jeder Abteilung steht „Kinder — bald" (Vorgabe Notizbuch: Damen/Herren/Kinder je Abteilung). Sobald Produkte `who:'kinder'` bekommen, wird der Link aktiviert — aktuell gibt es keine Kinderprodukte, daher bewusst kein klickbarer leerer Bereich.
- **Job/Karriere**: Steht in Olegs Notizbuch, wurde aber in einem früheren Feedback explizit entfernt („Karriere kann raus"). Aktuell draußen — bitte klären, ob eine Karriere-Seite doch gewünscht ist.
- **Bunte Buchstaben im Logo**: Die Skizze zeigt auch mehrfarbige Buchstaben (L blau, D grün, O orange …). Umgesetzt sind bislang nur die Rahmen-Quadrate — die Wortmarke blieb bewusst einfarbig (wirkt edler). Auf Wunsch ist die bunte Variante schnell gebaut.
- **Viele Farben pro Produkt** (Lacoste-Prinzip, 10–25 Farben): braucht echte Varianten-Daten + Bilder je Farbe.

## Bildkatalog — Rest-Synchronisation
Vom Drive-Katalog sind alle 70 Artikel mit mindestens einem Vollformat-Bild eingebunden.
Noch offen: Bei 8 Produkten (01, 07, 15, 17, 21, 24, 49, 51) fehlt der `_a`-Packshot lokal
(aktuell zeigt das Grid dort `_b`/`_c`), und bei vielen Produkten fehlen die `_b`/`_c`-Galeriebilder.
Die Dateien liegen im Drive (`produkte/`-Ordner) — bei Gelegenheit nachladen nach `assets/p/`
und im `P`-Array `img`/`gal` ergänzen (Konvention siehe UEBERGABE.md).

## KI-Kampagnenbilder (assets/e/)
Die Editorial-Bilder mit Menschen (Hero, Gucci-Kacheln, Abteilungen, Kollektionen) sind
KI-generiert — die abgebildeten Personen existieren nicht. Vor Livegang durch echte
Kampagnen-Shootings ersetzen oder als KI-Bild kennzeichnen (je nach Rechtslage/Markenauftritt).

## Vom Kunden zu liefern
- Telefonnummer + E-Mail (gelbe Markierungen in Impressum/Datenschutz/Widerruf/Kontakt)
- UID-Nummer bzw. Kleinunternehmer-Hinweis, USt.-Ausweis der Preise
- Je Produkt mind. 4 echte Bilder für eine volle Galerie (aktuell 2)
- Maßtabelle Bademäntel (Größenberater), echte Materialzusammensetzungen
