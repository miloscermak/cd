# ČD Kvíz — Live hlasovací aplikace

## O co jde

Single-file HTML aplikace pro živý kvíz na AI Masterclass pro vedení Českých drah. Presenter promítá otázky, účastníci hlasují na mobilech, výsledky se zobrazují v reálném čase.

## Struktura repo

```
ceske-drahy/
├── CLAUDE.md                          # Projektový brief
├── research/                          # Zdrojové researche (3 dokumenty + executive summary)
├── masterclass/
│   ├── 01-uvod.md                     # Úvodní řeč k Masterclass
│   ├── 02-kviz.md                     # Textová verze kvízu
│   └── quiz/
│       ├── index.html                 # ⭐ Hlavní aplikace (single-file, deploy tohle)
│       └── SETUP.md                   # Instrukce pro Firebase + Netlify
```

## Tech stack

- Vanilla HTML/CSS/JS, zero dependencies kromě CDN
- Firebase Realtime Database (v9 compat mode) pro synchronizaci hlasů
- QRCode.js pro generování QR kódu
- Hosting: Netlify (nebo cokoliv statického)

## Před deployem

V `index.html` na řádcích 789–796 je placeholder pro Firebase config. Musí se nahradit skutečným configem z Firebase Console. Postup v `SETUP.md`.

## Deploy na Netlify

- Publish directory: `ceske-drahy/masterclass/quiz`
- Build command: žádný (statický soubor)
- Branch: `main`

## Jak to funguje

- `?mode=presenter&room=XXXX` → presenter view (tmavý, na projektor)
- `?room=XXXX` → voter view (světlý, na mobil)
- Bez parametrů → landing page (vytvořit/připojit se k místnosti)

## Pravidla pro úpravy

- Kvízová data jsou hardcoded v JS (pole `QUIZ_DATA`) — edituj přímo tam
- Nemazat a nepřepisovat soubory v `research/` bez souhlasu
- Při přidávání otázek dodržovat formát: question, options {A,B,C,D}, correct, comment
