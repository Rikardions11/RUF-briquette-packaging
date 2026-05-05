# Brikešu pakošanas līnijas simulācija

## Projekta apraksts

2D vizuāla simulācija automātiskās kantaino brikešu pakošanas iekārtas
darbībai. Simulācija balstīta uz reālu inženiertehnisko risinājumu, kas
izstrādāts bakalaura darbā SIA „Avoti SWF" Lizuma brikešu cehā.

Mērķis nav fizikāli precīza diskrēto elementu metode, bet gan **vizuāli
ticams iekārtas darbības atspoguļojums**, kas demonstrē sistēmas plūsmu —
no preses cikla līdz gatavai pakai pēc plēvošanas.

## Tehniskā steka prasības

- **Tikai vanilla HTML + CSS + JavaScript** ar Canvas 2D API
- **Bez ārējām bibliotēkām** (bez React, bez p5.js, bez jQuery)
- **Bez build sistēmas** (faili atveras tieši pārlūkā ar dubultklikšķi)
- Animācijas cilpa ar `requestAnimationFrame` un Δt-balstītu pozīciju aprēķinu
- Kods rakstīts ES6+ moduļos (`type="module"`), kad sākam refaktorēt

## Reālās iekārtas tehniskie parametri

### Brikešu preses
- **Konfigurācija:** 4 RUF tipa hidrauliskās preses, katra divpusēja → 8 izeju punkti
- **Vienas preses produktivitāte:** 1 brikete uz 7,2 sekundēm (atbilst 500 kg/h)
- **Ražotne:** maksimālais īpatnējais presēšanas spiediens uz briketes plakni ~1700 kg/cm²
- Cikls: hidrauliskā cilindra gājiens vienlaicīgi presē vienā kambarā un
  izgrūž briketi no otrā — viens cikls = viena izgūta brikete

### Brikete (gabarīti)
- Izmēri: **150 × 65 × 100 mm**
- Masa: ~1 kg
- Standarts: EN ISO 17225-3
- Skatā no augšas (top-down) brikete redzama kā taisnstūris ar lielāko plakni
  150 × 100 mm

### Konveijeru sistēma
Trīs taisnie ķēdes konveijeri + viens pagrieziena konveijers ar 90° pagriezienu.

| Konveijers | Plūsma uz vienu ķēdi | Apkalpo |
|------------|---------------------|---------|
| Konveijers 3 (tālākais) | 1 brikete / 3,6 s | Preses 3 un 4 |
| Konveijers 2 | 1 brikete / 2,4 s | + Prese 2 |
| Konveijers 1 (tuvākais grupēšanai) | 1 brikete / 1,8 s | + Prese 1 |
| Konveijers 0 (90°) | tāda pati izejas plūsma | Pagrieziens uz grupēšanu |

Katram **taisnam konveijeram ir divas paralēlas neatkarīgas ķēdes**, kas
darbojas sinhroni, bet briketes pa tām pārvietojas neatkarīgi.

### Brikešu padeves moduļi
Uz katra taisna konveijera, blakus preses izejai, atrodas pneimatisks
brikešu padeves modulis, kura uzdevums ir nogādāt briketi vai nu uz
**tuvāko**, vai **tālāko** konveijera ķēdi:
- **Tuvākās ķēdes modulis:** pneimatiskais cilindrs novietots virs rullīšiem;
  virzulim izvirzoties — brikete tiek nostumta uz tuvākās ķēdes
- **Tālākās ķēdes modulis:** pneimatiskais cilindrs apgriezts un novietots
  zem rullīšiem; virzulim ievelkoties — briketei pazūd pamats un tā nokrīt
  uz tālākās ķēdes

Šī risinājuma loģiskais princips: divu paralēlu plūsmu apvienošana vienā
konveijera materiālu plūsmā bez brikešu telpiskās orientācijas zaudēšanas.

### Pagrieziena konveijers (90°)
Briketes pārvietojas pa 90° loka trajektoriju, saglabājot savu telpisko
orientāciju (neapgāžas). Simulācijā realizēt ar polāro koordinātu
interpolāciju ap pagrieziena centra punktu.

### Grupēšanas mehānisms
- **Mērķa konfigurācija:** 12 briketes 6 × 2 izkārtojumā uz mazākās plaknes
- **Cikla laiks:** ne vairāk kā 21 sekunde uz vienu paku
- **Darbības princips:** brikešu pāri (no abām paralēlajām ķēdēm) tiek
  pakāpeniski stumti pa X-asi sešas reizes pēc kārtas
- **Stabilitātes nodrošinājums:** Y-ass virziena piespiedējmehānisms novērš
  kārtojuma sagāšanos stumšanas brīdī
- **Pēc grupēšanas:** paka pārvietojas pa X-asi uz etiķetes uzlikšanas
  pozīciju, pēc tam pa Z-asi cauri termosaraušanās plēves iekārtai
- **Drošība:** atbilst standartam EN ISO 13850 (avārijas apturēšana)

### Pakošanas plūsma (kopskats)
```
Prese (×4) → Padeves modulis → Taisnais konveijers (2 ķēdes)
   → Pagriezta konveijera 90° loks → Grupēšanas mezgls (6×2)
   → Etiķete → Plēvošana → Termotunelis → Paletizācija
```

## Vizuālais stils

- **Skats:** ortogonāla projekcija no augšas (top-down)
- **Fons:** tumši pelēks (industrial HMI / SCADA estētika)
- **Preses:** tumši pelēks taisnstūris ar metāliska izskata noformējumu
- **Briketes:** brūni-dzelteni taisnstūri (koksnes brikešu krāsa)
- **Konveijeru ķēdes:** tumšas līnijas ar periodisku zobu raksta animāciju
- **Pneimatiskie cilindri:** zila / oranža indikācija, kad aktīvi
- **UI panelis:** sānā vai apakšā, ar slaideriem un skaitītājiem

## Mērogs

Visa simulācija balstīta uz vienkāršu mēroga koeficientu starp reālajiem
milimetriem un pikseļiem. Definējama vienā konstantē `MM_PER_PX`
(piemēram, 5 mm/px), un visi izmēri (briketes 150×100 mm, konveijeru
garumi, padeves moduļu pozīcijas) iegūstami pārrēķinot.

## Kodēšanas konvencijas

- **Komentāri latviešu valodā** ar mehānisko inženierterminu lietojumu
- **Funkciju un mainīgo nosaukumi angļu valodā** (`Press`, `Conveyor`,
  `Briquette`, `FeederModule`, `GroupingUnit`)
- **Viena klase = viens fails**, kad sākam refaktorēt no `index.html` uz
  moduļiem
- **Konstantes augšā** katrā failā (cikla laiki, ātrumi, izmēri)
- **Δt visās fizikas funkcijās** — nekad neatkarīgu animāciju no kadru ātruma

## Uzbūves plāns

Skat. `PLAN.md` failu. Sekot fāzēm secīgi — sākam no vienas preses ar
vienu konveijera ķēdi un pakāpeniski augam līdz pilnai sistēmai.

## Ierobežojumi (out of scope)

- **PLC vadības loģika** — bakalaura darbā izslēgta, tāpēc simulācijā tā
  arī netiek detalizēti modelēta. Saglabājam tikai vienkāršus stāvokļus
  (gaida / strādā / bloķēts).
- **Inženiertehniskie aprēķini** — netiek iegūti no simulācijas. Simulācija
  ir tikai vizuāls instruments.
- **Realistisks fizisks brikešu sadursmes modelis** — pietiek ar
  cietas-ķermeņa pārvietošanas modeli ar atdurēm.
