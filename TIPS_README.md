# Tips & Activities invullen (tips.html)

`tips.html` toont een Leaflet-kaart met POI's (points of interest) rond Los Carmenes,
gegroepeerd per categorie in de zijbalk. Alle content komt uit één bestand:
[`tips.json`](tips.json). Er is geen build-stap nodig — bewerk het bestand en commit.

Op dit moment staat er **voorbeelddata** in (duidelijk gelabeld `(ejemplo)`), plus een
gele waarschuwingsbalk in de sidebar ("Datos de ejemplo..."). Vervang de inhoud van
`tips.json` door echte locaties en verwijder daarna die waarschuwing (zie onderaan).

## Formaat

`tips.json` is een platte lijst van objecten:

```json
{
  "label": "Naam van de locatie",
  "cat": "nature",
  "icon": "🏖️",
  "color": "#3498db",
  "lat": 36.71495,
  "lng": -4.30050
}
```

| Veld    | Betekenis                                                              |
|---------|--------------------------------------------------------------------------|
| `label` | Naam zoals die in de sidebar en de popup op de kaart verschijnt. Eigennamen blijven ongewijzigd, ongeacht de gekozen taal (ES/EN/NL/CA). |
| `cat`   | Categorie-sleutel — bepaalt groepering, kleur in de legenda en vertaalde titel. Zie tabel hieronder. |
| `icon`  | Eén emoji, getoond op de kaartmarker en naast de naam in de lijst.      |
| `color` | Hex-kleur van de marker/bolletje. Vrij te kiezen, maar houd 'm consistent per categorie. |
| `lat` / `lng` | Coördinaten (WGS84, gewoon decimaal — geen WKT of andere notatie). |

## Beschikbare categorieën (`cat`)

Deze acht zijn al vertaald in `tips.html` (ES/EN/NL/CA) — gebruik bij voorkeur alleen deze:

| `cat` waarde | NL label          | Typisch voor                          |
|--------------|--------------------|-----------------------------------------|
| `nature`     | Natuur & Stranden  | Stranden, wandelpaden, natuurgebied     |
| `restaurant` | Eten & Drinken     | Restaurants, bars, cafés                |
| `activity`   | Activiteiten       | Sport, watersport, attracties           |
| `shop`       | Winkels            | Supermarkt, bakker, etc.                |
| `practical`  | Praktisch          | Parkeren, tankstation                   |
| `stay`       | Verblijf           | Hotels/accommodaties in de buurt        |
| `culture`    | Cultuur            | Musea, bezienswaardigheden              |
| `poi`        | Overig             | Vangnet voor alles wat niet past        |

Wil je een nieuwe categorie toevoegen (bv. `nightlife`)? Voeg dan ook een regel toe aan
`CAT_LABELS` in `tips.html` (zoek naar `const CAT_LABELS = {`) met de ES/EN/NL/CA-tekst,
anders verschijnt de rauwe sleutel als label.

## Coördinaten opzoeken

- Rechtsklik op de locatie in [openstreetmap.org](https://www.openstreetmap.org) →
  "Show address" geeft lat/lng direct in de URL.
  Of gebruik Google Maps: rechtsklik op de locatie → de coördinaten staan bovenaan het menu.
- De kaart in `tips.html` is gecentreerd op `[36.714516, -4.300670]` (Los Carmenes zelf) —
  dat hoef je niet aan te passen tenzij het huis verhuist.

## Na het invullen van echte data

Verwijder de placeholder-waarschuwing zodra `tips.json` echte locaties bevat:

1. In `tips.html`, verwijder de regel
   `<div class="placeholder-note" id="placeholder-note">...</div>` (rond de sidebar-top), of
2. Verwijder gewoon de `note`-teksten uit het `UI`-object in `tips.html` en de regel
   `document.getElementById('placeholder-note').textContent = t.note;` in `showLang()`.

Geen andere code-aanpassingen nodig — de kaart, legenda en sidebar-lijst renderen
automatisch op basis van wat er in `tips.json` staat.
