# 🧗 Kletterschuh-Navigator

**Interaktive Vergleichs-App für 109 Kletterschuhe von 10 Herstellern** – als Single-File-HTML-App, ohne Build-Prozess, ohne Dependencies.

---

## Demo

Einfach `index.html` im Browser öffnen – keine Installation nötig. Mit GitHub Pages direkt hostbar (Settings → Pages → Branch `main` → Root).

## Features

| Feature | Beschreibung |
|---|---|
| **10 Marken, 109 Modelle** | La Sportiva, Scarpa, Tenaya, evolv, Five Ten, Mad Rock, Boreal, Ocún, Red Chili, UnParallel |
| **7 Vergleichsdimensionen** | Performance/Einsatz, Härte (1–5), Downturn (1–5), Asymmetrie (1–5), Leisten/Fit, Verschluss, Sohlengummi, Niveau |
| **Kalibrierte Skalen** | Werte sind *herstellerübergreifend* vergleichbar – ein „Downturn 4" bedeutet bei jeder Marke dasselbe |
| **Farbcodierung** | Grün (weich/flach/symmetrisch) → Rot (steif/aggressiv/spitz) für Erfassung auf einen Blick |
| **Multi-Select-Filter** | Marke (Chips), Niveau, Härte, Downturn, Asymmetrie, Leisten-Breite, Gummi-Familie – innerhalb einer Gruppe ODER-verknüpft, gruppenübergreifend UND (z. B. „Härte 3+4, Leisten breit, XS Edge") |
| **Freitextsuche** | Über Modellname, Einsatzbeschreibung, Verschluss, Fit |
| **Sortierung** | Klick auf Spaltenkopf, numerisch/alphabetisch/nach Niveau-Rang, Richtung umschaltbar |
| **Direktvergleich** | Bis zu 5 Schuhe (markenübergreifend) per Checkbox markieren → Gegenüberstellung im Modal, Attribute als Zeilen |
| **Äquivalenz-Matrix** | Welche Modelle der 10 Marken in dieselbe Kategorie fallen (Comp-Slipper, aggressiv Bouldern, Kante, Allround, Trad, Einsteiger) |
| **12 Gummi-Familien** | Vibram XS Grip2/Grip/Edge/Vision, FriXion, Stealth, TRAX, Science Friction, Zenith, Ocún CAT, Red Chili RX, UP RH |

## Tech

- **Eine einzige HTML-Datei** (~115 KB): HTML + CSS + Vanilla JS, keine Frameworks, keine Build-Tools
- Daten als `data-*`-Attribute direkt an den Tabellenzeilen → Filter/Sortierung/Vergleich arbeiten auf dem DOM, keine separate Datenhaltung
- Custom Multi-Select-Dropdowns, Sticky-Filterleiste, Vergleichs-Tray + Modal ohne Libraries
- Fonts: Fraunces + Archivo (Google Fonts, einziger externer Request)
- Responsive (horizontales Scrollen der Tabellen auf Mobile)

## Datenmodell

Jeder Schuh ist eine `<tr>` mit maschinenlesbaren Attributen:

```html
<tr data-shoe data-brand="scarpa" data-niv="fort"
    data-h="4" data-d="3" data-a="4"
    data-width="mittel" data-rubbercat="xsedge">
```

| Attribut | Werte |
|---|---|
| `data-brand` | `lasportiva` `scarpa` `tenaya` `evolv` `fiveten` `madrock` `boreal` `ocun` `redchili` `unparallel` |
| `data-niv` | `ein` (Einsteiger) · `int` (Intermediate) · `fort` (Fortgeschritten) · `pro` (Profi/Elite) |
| `data-h` / `data-d` / `data-a` | Härte / Downturn / Asymmetrie, jeweils `1`–`5` |
| `data-width` | `schmal` · `mittel` · `breit` (aus Leisten/LV/HV abgeleitet) |
| `data-rubbercat` | `xsgrip2` `xsgrip` `xsedge` `vision` `frixion` `stealth` `trax` `sciencefriction` `zenith` `cat` `rx` `uprh` |

Neue Modelle lassen sich durch Kopieren einer Zeile ergänzen – Filter, Sortierung und Vergleich greifen automatisch.

## Datenqualität & Grenzen

- Härte/Downturn/Asymmetrie sind **redaktionell kalibrierte Einschätzungen** auf Basis von Herstellerangaben und Testberichten – keine Messwerte.
- Gummizuordnung = übliche Standardausstattung; Sondereditionen und Resohlungen können abweichen.
- Sortiment = aktuell relevante Performance-/Komfortmodelle; Kinder-, Verleih- und Auslaufmodelle sind bewusst nicht vollständig.
- **Passform ersetzt keine Anprobe.** Die Leisten-Spalte bildet nur Volumen/Form grob ab.
- Stand der Daten: Mitte 2026.


## Projektstruktur

```
kletterschuh-navigator/
├── index.html    # Die komplette App (HTML + CSS + JS)
└── README.md     # Diese Datei
```

## Lizenz & Hinweise

Privates Referenzprojekt. Alle Marken- und Modellnamen gehören den jeweiligen Herstellern. Die Bewertungen sind redaktionelle Einschätzungen ohne Gewähr und keine Kaufberatung – Passform immer anprobieren.