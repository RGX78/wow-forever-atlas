# Atlas — WoW Forever

Interaktywny atlas stref: **57 map**, **865 pinów** (taxi, quest, vendor, NPC) z bety Forever. Wszystko lokalnie — działa offline, bez zewnętrznych CDN.

**Live:** https://rgx78.github.io/wow-forever-atlas/
**Lokalnie:** otwórz `index.html` (Leaflet i mapy są w repo).

## Co potrafi
- **Lista stref** pogrupowana: Świat (Azeroth, Kalimdor, Eastern Kingdoms) · Kalimdor · Eastern Kingdoms · Pola bitew · Inne.
- **Mapa z zoomem i przesuwaniem** (Leaflet, CRS.Simple) — obraz strefy w pełnej rozdzielczości 1002×668.
- **Piny według typu**: taxi (niebieski), quest (żółty), vendor (zielony), NPC (szary); obwódka = frakcja (Alliance/Horde/obie).
- **Filtry**: klikasz chipy, żeby wyłączyć typ; „frakcja" przełącza All/Horde/Alliance/both; „ukryj piny" chowa wszystko.
- **Szukanie pinu** po nazwie (np. „Thrall", „vendor") — wynik przenosi mapę do pinu i pokazuje tooltip.
- **Siatka stref** — 57 miniatur, klik = otwarcie mapy.
- **Klawiatura**: ← → przełącza strefy. Ostatnia strefa zapamiętana w localStorage.
- Responsywne: na telefonie lista chowa się pod ☰.

## Dane
- Mapy i piny: [warcraftforever.games/maps](https://warcraftforever.games/maps) — build klienta **1.60.1.69893**.
- Piny pochodzą z bety (ForeverLog) — **nie są kompletne**; część stref (np. Darnassus, Alterac Mountains) ma 0 pinów, bo nikt ich nie zeskanował.
- Assety pobrane lokalnie do `maps/` (~8,8 MB) i `thumbs/` (miniaturki).

## Struktura
```
index.html      — aplikacja (dane stref wbudowane w <script>)
maps/           — 57 map stref (.webp)
thumbs/         — miniaturki do siatki
vendor/         — Leaflet 1.9.4 (js + css)
```

## Odświeżanie danych
Skrypty pipeline'u: `F:\HERMES_ORION\.tmp\atlas\`
`build_zone_list.py` → `scrape_atlas.py` → `dl_images.py` → `prepare.py` → `build_app.py`
