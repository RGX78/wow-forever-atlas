# Atlas — WoW Forever

Interaktywny atlas stref: **57 map**, **865 pinów** (taxi, quest, vendor, NPC) z bety Forever. Wszystko lokalnie — działa offline, bez zewnętrznych CDN.

**Live:** https://rgx78.github.io/wow-forever-atlas/
**Lokalnie:** otwórz `index.html` (Leaflet i mapy są w repo).

## Co potrafi
- **Mapy kontynentów jako drzwi do stref**: na Eastern Kingdoms i Kalimdor narysowane są prostokąty stref — klik w strefę (albo w jej etykietę) otwiera mapę tej strefy, breadcrumb „Eastern Kingdoms › Westfall" i **Backspace** wracają do kontynentu.
- **Lista stref** pogrupowana: Świat (Azeroth, Kalimdor, Eastern Kingdoms) · Kalimdor · Eastern Kingdoms · Pola bitew · Inne.
- **Mapa z zoomem i przesuwaniem** (Leaflet, CRS.Simple) — obraz strefy w pełnej rozdzielczości 1002×668.
- **Piny według typu**: taxi (niebieski), quest (żółty), vendor (zielony), NPC (szary); obwódka = frakcja (Alliance/Horde/obie).
- **Filtry**: klikasz chipy, żeby wyłączyć typ; „frakcja" przełącza All/Horde/Alliance/both; „ukryj piny" chowa wszystko.
- **Szukanie pinu** po nazwie (np. „Thrall", „vendor") — wynik przenosi mapę do pinu i pokazuje tooltip.
- **Siatka stref** — 57 miniatur, klik = otwarcie mapy.
- **Klawiatura**: ← → przełącza strefy. Ostatnia strefa zapamiętana w localStorage.
- Responsywne: na telefonie lista chowa się pod ☰.

## Poziomy stref (levelowanie)
Każda strefa ma zakres poziomów widoczny w liście, na etykietach kontynentu i w belce tytułu (`poziom 10–20 · 15 pinów`). Chip **„trasa 1–60"** otwiera listę stref w kolejności levelowania, pogrupowaną co 10 poziomów.

Zakresy dla starych stref = kanoniczne zakresy Classic (1–10 Elwynn, 10–20 Westfall, 15–25 Redridge, 30–45 STV itd.). Nowe strefy Forever bez potwierdzonego zakresu są oznaczone **`~`** (szacunek z poziomów NPC): Zephras Isle, Darkspear Islands, Riverglades, Moonglade. `Shendralas` nie ma żadnych NPC w bazie → `?`.

## Skąd prostokąty stref
`worldmaparea.csv` z repo TheGrayDot/wow-vanilla-world-coords — granice stref w koordynatach świata (WorldMapArea) plus osobne wiersze „Azeroth" (mapID 0) i „Kalimdor" (mapID 1) definiujące zasięg mapy kontynentu. Normalizacja:
`u = (LocLeft_continent − LocLeft_zone) / (LocLeft_continent − LocRight_continent)`, `v = (LocTop_continent − LocTop_zone) / (LocTop_continent − LocBottom_continent)`.
46/49 stref ma prostokąt; nowe strefy Forever (Riverglades, Shendralas, Mount Hyjal) nie mają odpowiednika w vanilla — są tylko na liście.

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
