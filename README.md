# 🧗 Kletterschuh-Navigator

**Interaktive Vergleichs-App für 133 Kletterschuhe von 12 Herstellern** – als Single-File-HTML-App, ohne Build-Prozess, ohne Dependencies.

---

## Demo

Einfach `index.html` im Browser öffnen – keine Installation nötig. Mit GitHub Pages direkt hostbar (Settings → Pages → Branch `main` → Root).

## Features

| Feature | Beschreibung |
|---|---|
| **12 Marken, 133 Modelle** | La Sportiva, Scarpa, Tenaya, evolv, Five Ten, Mad Rock, Boreal, Ocún, Red Chili, UnParallel, Black Diamond, Simond |
| **7 Vergleichsdimensionen** | Performance/Einsatz, Härte (1–5), Downturn (1–5), Asymmetrie (1–5), Leisten/Fit, Verschluss, Sohlengummi, Niveau |
| **Kalibrierte Skalen** | Werte sind *herstellerübergreifend* vergleichbar – ein „Downturn 4" bedeutet bei jeder Marke dasselbe |
| **Farbcodierung** | Grün (weich/flach/symmetrisch) → Rot (steif/aggressiv/spitz) für Erfassung auf einen Blick |
| **Filter** | Kompakte Leiste mit Suche, Marken-Chips (wischbar auf dem Handy) und Neuheiten-Schalter; weitere Filter (Niveau, Härte/Downturn/Asymmetrie als 1–5-Leiste, Leisten, Gummi) in einem Filter-Fenster (mobil von unten). Innerhalb einer Gruppe ODER, gruppenübergreifend UND. Aktive Filter erscheinen als entfernbare Kärtchen, dazu Trefferzahl „x von 133“ und „Alle Filter löschen“ |
| **Freitextsuche** | Über Modellname, Einsatzbeschreibung, Verschluss, Fit |
| **Sortierung** | Klick auf Spaltenkopf, numerisch/alphabetisch/nach Niveau-Rang, Richtung umschaltbar |
| **Direktvergleich** | Bis zu 5 Schuhe (markenübergreifend) per Checkbox markieren → Gegenüberstellung im Modal, Attribute als Zeilen, inkl. Link zur Herstellerquelle |
| **Neuheiten** | Badge „neu“ (Modelljahr 2026, neu oder überarbeitet) bzw. „angekündigt“ (offiziell angekündigt, noch nicht erhältlich) + Filter „Nur Neuheiten“ |
| **Teilbare Links** | Suche, Filter und Sortierung stehen im URL-Hash (z. B. `#b=scarpa&h=3,4&new=1`) und werden beim Öffnen wiederhergestellt |
| **Äquivalenz-Matrix** | Welche Modelle der 12 Marken in dieselbe Kategorie fallen (Comp-Slipper, aggressiv Bouldern, Kante, Allround, Trad, Einsteiger) |
| **15 Gummi-Filter** | Vibram XS Grip2/Grip/Edge/Vision, FriXion, Stealth, TRAX, Science Friction, Xtreme Friction, Zenith, Ocún CAT, Red Chili RX, UnParallel RH/RA, Black Diamond, Sonstige/k. A. |

## Tech

- **Eine einzige HTML-Datei** (~145 KB): HTML + CSS + Vanilla JS, keine Frameworks, keine Build-Tools
- Daten als `data-*`-Attribute direkt an den Tabellenzeilen → Filter/Sortierung/Vergleich arbeiten auf dem DOM, keine separate Datenhaltung
- Sticky-Filterleiste, Filter-Sheet (Dialog mit Esc/Hintergrund-Klick), Vergleichs-Tray + Modal ohne Libraries
- Farblogik: ausgewählt = helles Creme, Orange nur für die Hauptaktion und Links, Gold für Neuheiten, Grün→Rot ausschließlich für die 1–5-Skalen
- Fonts: Fraunces + Archivo (Google Fonts, einziger externer Request)
- Responsive (horizontales Scrollen der Tabellen auf Mobile)

## Datenmodell

Jeder Schuh ist eine `<tr>` mit maschinenlesbaren Attributen:

```html
<tr data-shoe data-brand="scarpa" data-niv="fort"
    data-h="4" data-d="3" data-a="4"
    data-width="mittel" data-rubbercat="xsedge"
    data-new="neu" data-src="https://…">
```

| Attribut | Werte |
|---|---|
| `data-brand` | `lasportiva` `scarpa` `tenaya` `evolv` `fiveten` `madrock` `boreal` `ocun` `redchili` `unparallel` `blackdiamond` `simond` |
| `data-niv` | `ein` (Einsteiger) · `int` (Intermediate) · `fort` (Fortgeschritten) · `pro` (Profi/Elite) |
| `data-h` / `data-d` / `data-a` | Härte / Downturn / Asymmetrie, jeweils `1`–`5` |
| `data-width` | `schmal` · `mittel` · `breit` (aus Leisten/LV/HV abgeleitet) |
| `data-rubbercat` | `xsgrip2` `xsgrip` `xsedge` `vision` `frixion` `stealth` `trax` `sciencefriction` `xtremefriction` `zenith` `cat` `rx` `uprh` `bd` `andere` (Sonstige bzw. keine Herstellerangabe) |
| `data-new` *(optional)* | `neu` (Modelljahr 2026, neu/überarbeitet) · `angekuendigt` (offiziell angekündigt, noch nicht erhältlich) |
| `data-src` *(optional)* | URL der Herstellerseite bzw. Pressemitteilung (nur `http(s)`), erscheint im Vergleichs-Modal |

Neue Modelle lassen sich durch Kopieren einer Zeile ergänzen – Filter, Sortierung und Vergleich greifen automatisch.

## Datenqualität & Grenzen

- Härte/Downturn/Asymmetrie sind **redaktionell kalibrierte Einschätzungen** auf Basis von Herstellerangaben und Testberichten – keine Messwerte.
- Gummizuordnung = übliche Standardausstattung; Sondereditionen und Resohlungen können abweichen.
- Sortiment = aktuell relevante Performance-/Komfortmodelle; Kinder-, Verleih- und Auslaufmodelle sind bewusst nicht vollständig.
- **Passform ersetzt keine Anprobe.** Die Leisten-Spalte bildet nur Volumen/Form grob ab.
- „k. A.“ = keine Herstellerangabe gefunden; solche Felder wurden bewusst nicht geschätzt.
- Five Ten, UnParallel und Simond konnten nicht direkt beim Hersteller geprüft werden (siehe Hinweise in den jeweiligen Sektionen).
- Stand der Daten: November 2026.

## Changelog

### 11/2026
Sortiment, Verschluss und Gummi aller Marken gegen die Herstellerkataloge geprüft (La Sportiva USA, Scarpa, Tenaya, Mad Rock, Black Diamond: Shop-Produktdaten; Boreal: Shop-API; Red Chili: Produktdatenblätter; Ocún, evolv: Katalogseiten; Pressemitteilungen von La Sportiva, Edelrid und Ocún).

- **Neue Marken:** Black Diamond (6 Modelle), Simond (3 Modelle)
- **Neu/überarbeitet 2026:** Scarpa Blackbird, Furia Air · Tenaya Aruma · evolv Zenist · Mad Rock Villain, Remora Pro · Red Chili Voltage 3, Magnet Lace · Ocún Jett · La Sportiva Skwama Lite, HyperEZ
- **Angekündigt:** La Sportiva Solution / Solution Comp (Frühjahr 2027)
- **Ergänzt:** u. a. La Sportiva Kubo, Mandala, Mantra · Scarpa Chimera, Vapor S, Reflex VS · evolv Phantom Pro LV, Rave, Yosemite Bum LV · Mad Rock Drone 2, D2.ONE, Shark 3, Talaria, RedLine Strap · Boreal Synergy 2.0, Indo, Ballet · Ocún Sigma, Iris, Jett Crack · Red Chili Voltage Lace/X, Magnet, Ventic Air, Sausalito
- **Entfernt (nicht mehr im Herstellerkatalog bzw. nicht belegbar):** La Sportiva Aragon · Scarpa Furia S, Maestro · evolv Oracle, Agro, Defy · Mad Rock Haywire, Drifter, Flash 2.0 (Shark 2.0/Drone HV → Nachfolger) · Boreal Diabolo, Kintaro · Ocún Oxi · Red Chili Atomyc 2, Amp (Voltage 2 → Voltage 3)
- **Korrigiert:** u. a. La Sportiva Genius (Schnürung), Solution (1 Klettriemen), Finale (XS Edge), Skwama Lite (FriXion Black), HyperEZ (FriXion XF 2.0) · Mad Rock Phoenix (Leder-Schnürschuh, kein Aggressiv-Klett), Rover (Einsteiger), Drone CS (Xtreme Friction) · Red Chili Mystix (Schnürung), Fusion/Charger (RX-1), Spirit (3 Klettriemen), Sensor (aggressiv) · Boreal Crux (technischer Allrounder statt Einsteiger) · UnParallel Newtro VCS (steif & aggressiv)
- **Fußnoten bereinigt:** nicht belegbare Modellnamen entfernt (u. a. Mad Rock Lyra/Agama/M5/Weaver, Boreal Marduk, Red Chili Matador, evolv Supra/Eldo)


## Projektstruktur

```
kletterschuh-navigator/
├── index.html    # Die komplette App (HTML + CSS + JS)
└── README.md     # Diese Datei
```

## Lizenz & Hinweise

Privates Referenzprojekt. Alle Marken- und Modellnamen gehören den jeweiligen Herstellern. Die Bewertungen sind redaktionelle Einschätzungen ohne Gewähr und keine Kaufberatung – Passform immer anprobieren.