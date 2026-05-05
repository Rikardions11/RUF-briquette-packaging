# Izstrādes plāns — fāzēs

Šis fails kalpo kā ceļa karte Claude Code agentam, kā arī manai paša
orientācijai. Katrā fāzē ir definēts skaidrs **iznākums** — kas pēc tās
pabeigšanas redzams ekrānā — un **pieņemšanas kritērijs**.

Strādājam pa fāzēm secīgi. Nepāreju uz nākamo fāzi, kamēr iepriekšējā
nav vizuāli pārbaudīta pārlūkprogrammā.

---

## 0. fāze — sagatavošana ✅

**Iznākums:** projekta mape ar `CLAUDE.md`, `README.md`, `PLAN.md`,
sākotnējo `index.html` un `.gitignore`. Git repozitorijs inicializēts.

```bash
git init
git add .
git commit -m "Sākotnējā projekta struktūra"
```

---

## 1. fāze — viena prese, viena konveijera ķēde

**Iznākums:** Canvas elementā redzama viena prese, kas izgrūž briketes
uz vienas konveijera ķēdes ar adjustējamu cikla laiku.

**Tehniskie uzdevumi:**
- [ ] Animācijas cilpa ar `requestAnimationFrame` un Δt aprēķinu
- [ ] `Press` klase ar cikla taimeri (1,8 – 7,2 s diapazons)
- [ ] `Briquette` objekts ar pozīciju, ātruma vektoru un stāvokli
- [ ] `Conveyor` klase ar vienu ķēdi, ķēdes ātrums kā parametrs
- [ ] HTML range slaideris preses cikla laika regulēšanai
- [ ] Brikešu skaitītājs (kopējais izgūto brikešu skaits)

**Pieņemšanas kritērijs:** maina slaideri → mainās brikešu izgrūšanas
ritms; briketes vienmērīgi pārvietojas pa konveijera ķēdi no preses uz
ekrāna labo malu.

---

## 2. fāze — divpusēja prese ar diviem padeves moduļiem

**Iznākums:** prese izgrūž briketes pārmaiņus uz tuvāko un tālāko ķēdi
caur pneimatisku padeves moduli.

**Tehniskie uzdevumi:**
- [ ] Konveijeram pievienot otru paralēlu ķēdi (`chain[0]`, `chain[1]`)
- [ ] `FeederModule` klase ar diviem stāvokļiem: `near` / `far`
- [ ] Pneimatiskā cilindra animācija (izstiepts / ievilkts) ar
      `ease-in-out` interpolāciju
- [ ] Preses izeja → modulis → noteiktā ķēde
- [ ] Vizuāla cilindra stāvokļa indikācija (krāsas maiņa)

**Pieņemšanas kritērijs:** briketes pārmaiņus parādās uz augšējās un
apakšējās ķēdes; pneimatiskā cilindra kustība redzama vizuāli.

---

## 3. fāze — visas četras preses un trīs taisnie konveijeri

**Iznākums:** pilns brikešu savākšanas sistēmas atspoguļojums no augšas.

**Tehniskie uzdevumi:**
- [ ] 4 preses, katra ar 2 izejām (kopā 8 padeves punkti)
- [ ] 3 secīgi taisnie konveijeri ar 2 paralēlām ķēdēm katrs
- [ ] Brikešu plūsmas summēšanās: konveijers 3 → 2 → 1
- [ ] Pārejas zonas starp konveijeriem (briketes nemaina orientāciju)
- [ ] Slaideri katras preses cikla laikam (kopā 4 slaideri)

**Pieņemšanas kritērijs:** plūsmas ātrumi atbilst CLAUDE.md tabulai
(konveijers 1 saņem brikeshes ar augstāko intensitāti — 1 brikete uz
1,8 s uz vienu ķēdi).

---

## 4. fāze — pagrieziena konveijers (90°)

**Iznākums:** briketes pagriežas 90° lokā, saglabājot orientāciju.

**Tehniskie uzdevumi:**
- [ ] `TurningConveyor` klase ar polāro koordinātu interpolāciju
- [ ] Pagrieziena centrs un rādiuss kā konfigurējami parametri
- [ ] Briketes telpiskā orientācija saglabāta (rotē kopā ar trajektoriju
      tā, lai brikete saglabātu orientāciju attiecībā pret kustības virzienu)
- [ ] Vizuāla loka indikācija konveijera kontūrai

**Pieņemšanas kritērijs:** brikete ieiet 90° lokā un izejošajā galā
turpina kustību perpendikulāri ieejas virzienam.

---

## 5. fāze — grupēšanas mehānisms

**Iznākums:** 12 briketes savācas 6×2 matricā, kā prasīts tehniskajās
prasībās.

**Tehniskie uzdevumi:**
- [ ] Ieejas zonas sensori — reģistrē divu paralēlo brikešu pienākšanu
- [ ] Brikešu pāra reģistrs (līdz 6 pāriem)
- [ ] Pirmais pneimatiskais cilindrs — pakāpeniski stumj pārus pa X-asi
      6 reizes pēc kārtas
- [ ] Y-ass piespiedējmehānisms (vizuāla statīvu animācija)
- [ ] Cikla laika ierobežojums: viena paka ne vairāk kā 21 s
- [ ] Cikla skaitītājs (cik pakas saformētas)

**Pieņemšanas kritērijs:** 12 briketes salasās matricā, pneimatisko
cilindru kustība atbilst secīgajai stumšanai.

---

## 6. fāze — etiķete, plēvošana un izeja

**Iznākums:** gatavā paka iziet cauri plēvošanas iekārtai un nonāk uz
izejas konveijera.

**Tehniskie uzdevumi:**
- [ ] Otrais cilindrs — pārvieto paku uz etiķetes pozīciju
- [ ] Etiķetes uzlikšanas vizuāla indikācija (uzliesmojums vai krāsas maiņa)
- [ ] Z-ass kustība cauri plēvošanas iekārtai
- [ ] Plēves "savilkšanās" animācija (paka kļūst nedaudz mazāka un spīdīga)
- [ ] Termotuneļa attēlojums

**Pieņemšanas kritērijs:** paka pilnā ciklā iziet no grupēšanas mezgla
līdz izejas pozīcijai bez pārtraukumiem.

---

## 7. fāze — vadības panelis un statistika

**Iznākums:** profesionāla HMI saskarne ar reāllaika rādītājiem.

**Tehniskie uzdevumi:**
- [ ] Globāls laika paātrinājuma multiplikators (1× / 2× / 5× / 10×)
- [ ] Pause / Play / Reset pogas
- [ ] Statistikas panelis: brikešu kopskaits, pakas/h, sistēmas noslodze
      katrā konveijerā
- [ ] Avārijas apturēšanas poga (vizuāla, sarkana, iztur EN ISO 13850
      semantiku)
- [ ] Krāsainā shēma matchosies ar SIA „Avoti" estētiku

**Pieņemšanas kritērijs:** simulācija izskatās un izjūtas kā reāla
ražošanas vadības saskarne.

---

## Refaktorēšanas slieksnis

Kad `index.html` pārsniedz **400 rindas**, sadalām moduļos:

```
brikesu-sim/
├── index.html
├── style.css
├── js/
│   ├── main.js          # cilpa, init, render dispatch
│   ├── config.js        # konstantes, parametri, krāsas
│   ├── press.js         # Press klase
│   ├── feeder.js        # FeederModule klase
│   ├── conveyor.js      # Conveyor un TurningConveyor klases
│   ├── briquette.js     # Briquette objekts
│   ├── grouping.js      # GroupingUnit klase
│   └── ui.js            # slaideri un statistika
└── assets/              # tekstūras, ja vēlams
```
