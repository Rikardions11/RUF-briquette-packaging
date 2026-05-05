# Brikešu pakošanas līnijas simulācija

2D vizuāla simulācija automātiskās kantaino brikešu pakošanas iekārtas
darbībai. Iekārta ir bakalaura darba „Automātiskā kantaino brikešu
pakošanas iekārta" praktiskā realizācija SIA „Avoti SWF" Lizuma
brikešu cehā.

## Sistēmas konfigurācija

- 4 RUF tipa hidrauliskās preses (8 izejas punkti)
- 3 taisnie ķēdes konveijeri ar paralēlām ķēdēm
- 1 pagrieziena konveijers (90°)
- Pneimatiskais grupēšanas mehānisms 6×2 izvietojumam
- Etiķetēšana, plēvošana un termotuneļa atspoguļojums

## Palaišana

Atver `index.html` pārlūkprogrammā. Nav nepieciešama instalēšana,
build sistēma vai serveris.

```bash
# macOS
open index.html

# Windows
start index.html

# Linux
xdg-open index.html
```

## Izstrāde ar Claude Code

Visa konteksta informācija ir failā `CLAUDE.md` — Claude Code agents
to automātiski ielasa katras sesijas sākumā.

Izstrādes plāns un fāzes — `PLAN.md`.

## Tehnoloģiju steks

Vanilla HTML + CSS + JavaScript ar Canvas 2D API. Bez ārējām
bibliotēkām, bez build sistēmas.

## Autors

Rihards Salmiņš, LBTU Inženierzinājņu un informācijas tehnoloģiju
fakultāte, Mašīnu projektēšanas un ražošanas studiju programma, 2026.
