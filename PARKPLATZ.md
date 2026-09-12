# PARKPLATZ — geparkte Produkte

Diese Artikel wurden aus dem Shop genommen, sind aber vollständig vorbereitet:
Bilder liegen weiter unter `assets/`, die Produktzeilen stehen hier zum
Wieder-Einfügen (in `index.html` vor `];` des `P`-Arrays einsetzen, `rel`-IDs
ggf. anpassen). Reihenfolge = Zeitpunkt der Entfernung, Neueste zuletzt.

## Kosmetik & Duft
| Produkt | frühere ID | Bilder | Anmerkung |
|---|---|---|---|
| Raumduft-Diffuser, 100 ml | p08 | 08_raumduft-diffuser_a/_c.webp | |
| Sonnencreme SPF 50, 150 ml | p18 | 18_sonnencreme_*.webp | Saisonartikel — Sommer |
| Haaröl, 100 ml | p23 | 23_haaroel_*.webp | |
| Zahnputzbecher | p27 | 27_zahnputzbecher_*.webp | |
| Flüssigseife, 300 ml | p36 | 36_fluessigseife_*.webp | |
| EdP „Sea Breeze" | p01 | 01_eau-de-parfum-damen_*.webp | Standard-Flakon |
| EdP „Giardino" | p90 | 90_a/90_b.jpg | Verlaufs-Flakon türkis |
| EdP „Tramonto" | p91 | 91_a/91_b.jpg | Verlaufs-Flakon violett-orange |
| EdP „Notte" | p97 | 97_a/97_b.jpg | schwarzes Glas, Gold |
| EdP „Marmo" | p98 | 98_a/98_b.jpg | Marmor-Optik („altmodisch" — Oleg) |
| EdP „Prisma" | p99 | 99_a/99_b.jpg | Klarglas |
| Parfüm-Puzzle, 4 × 2 ml | p04 | 04_puzzle.jpg | Mini-Flakons als Puzzleteile |
| EdP „Blocco" | p127 | 127_a.jpg (+ Varianten assets/e/flakon-blocco-*.jpg) | Klarglas-Block, Farbverlauf innen |
| Shampoo, 250 ml | p19 | 19_shampoo-250_*.webp | Basis-Shampoo („Volume"/„Repair" sind im Shop) |
| Shampoo, 500 ml | p20 | 20_shampoo-500_*.webp | |

## Sets (komplett geparkt)
| Produkt | frühere ID | Bilder |
|---|---|---|
| Willkommensset | S1 | assets/s/S1_* |
| Duschset komplett | S2 | assets/s/S2_* |
| Duft-Geschenkbox | S3 | assets/s/S3_* |
| Haarpflege-Set | S4 | assets/s/S4_* |
| Handtaschen-Set | S5 | assets/s/S5_* |
| Reiseset | S6 | assets/s/S6_* |
| Zahnpflege-Set | S7 | assets/s/S7_* |
| Handtuch-Set, 3-teilig | S8 | assets/s/S8_* |
| Duschpflege-Set | S9 | assets/s/S9_* |
| Neukundenset | S10 | assets/s/S10_* |

## Mode & Accessoires
| Produkt | frühere ID | Bilder | Anmerkung |
|---|---|---|---|
| Kartenetui | p53 | 53_kartenetui_*.webp | |
| Schlüsselanhänger | p54 | 54_schluesselanhaenger_*.webp | Olegs Skizze existiert auch |
| Trinkflasche, 500 ml | p55 | 55_trinkflasche_*.webp | Sport-Flasche „Idra" (p109) ist noch im Shop |
| Windbreaker „Vento" | p70 | 70_a/70_b.jpg | Colorblock orange-violett |
| Biker-Shorts „Sprint" | p104 | 104_a/104_b.jpg | „wirkt billig" — Oleg |
| Leggings „Motion" (violett) | p102 | 102_a–d.jpg | |
| Sport-Bra „Support" (grün) | p103 | 103_a/103_b.jpg | |
| Sport-Shorts „Pace" (grün) | p107 | 107_a/107_b.jpg | |
| Herren-T-Shirt „Essenziale" | p118 | 118_a/118_b.jpg + 118_video.mp4 | Redesign mit Quadrate-Print |
| Herren-Hoodie „Comodo" | p119 | 119_a/119_b.jpg | Creme mit Quadrate-Tape |
| Herren-Jogginghose „Rilassato" | p121 | 121_a/121_b.jpg | |
| Loafer-Socken 3er | p123 | 123_a.jpg | Schwarz/Königsblau/Braun |

## Zubehör (Duschwelt — geparkt mit den Duschkonzepten)
| Produkt | frühere ID | Bilder |
|---|---|---|
| Seifenschale | p56 | 56_seifenschale_*.webp |
| Seifenspender-Set, 2-teilig | p57 | 57_seifenspender-set_*.webp |
| Glasabzieher | p58 | 58_glasabzieher_*.webp |
| Duschregal | p59 | 59_duschregal_*.webp |

Noch im Shop aus Zubehör: nur die Antirutschmatte (p60).

## Wieder einbauen — so geht's
1. Produktzeile aus der Git-History holen (`git log -p -S "id:'pXX'" -- index.html`)
   oder neu anlegen nach dem Schema in UEBERGABE.md.
2. Vor `];` des `P`-Arrays einfügen, `rel`-Verweise auf aktuelle IDs prüfen.
3. Bilder liegen unverändert unter `assets/p/` bzw. `assets/s/`.
