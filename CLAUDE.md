# E.ON Kvíz — Live hlasovací aplikace

## O co jde

Single-file HTML aplikace pro živý kvíz pro vedení E.ON. Otázky postavené na integrované výroční zprávě E.ON SE za rok 2024. Presenter promítá otázky, účastníci hlasují na mobilech, výsledky se zobrazují v reálném čase.

Původně stejná šablona sloužila pro kvíz na AI Masterclass Českých drah — ta verze je archivovaná v `_archive/cd-quiz/`.

## Struktura repo

```
./
├── CLAUDE.md                          # Tento brief
├── netlify.toml                       # base = e-on/quiz (produkční verze)
├── e-on/                              # ⭐ AKTIVNÍ PROJEKT
│   └── quiz/
│       ├── index.html                 # Hlavní aplikace (deploy tohle)
│       └── SETUP.md                   # Instrukce pro Firebase + Netlify
├── ceske-drahy/                       # Masterclass materiály (research, texty) — zachováno
│   ├── research/                      # 3 researche + executive summary
│   ├── masterclass/
│   │   ├── 01-uvod.md
│   │   └── 02-kviz.md                 # Textová verze původního ČD kvízu
│   └── CLAUDE.md                      # Starý brief pro ČD Masterclass
├── _archive/
│   └── cd-quiz/                       # Archivovaná původní ČD verze aplikace
│       ├── index.html
│       └── SETUP.md
└── e.on se_vyrocni zprava_2024.pdf    # Zdroj pro otázky E.ON (mimo worktree, ve složce quiz/)
```

## Tech stack

- Vanilla HTML/CSS/JS, zero dependencies kromě CDN
- Firebase Realtime Database (v9 compat mode) pro synchronizaci hlasů
- QRCode.js pro generování QR kódu
- Hosting: Netlify (auto-deploy z `main` přes `netlify.toml`)

## Branding E.ON

- Primary: `#E2001A` (E.ON červená)
- Hover: `#B8001A`
- Landing gradient: `linear-gradient(135deg, #6B0F6E 0%, #E2001A 100%)` — purple→red jako obálka výroční zprávy
- Claim: **„Nechte to na nás"**
- Font: Inter (Google Fonts)

## Deploy na Netlify

- `netlify.toml` → `base = "e-on/quiz"`, `publish = "."`
- Build command: žádný (statický soubor)
- Branch: `main`
- Po pushi do `main` se spustí auto-deploy

## Jak to funguje

- `?mode=presenter&room=XXXX` → presenter view (tmavý, na projektor)
- `?room=XXXX` → voter view (světlý, na mobil)
- Bez parametrů → landing page (vytvořit/připojit se k místnosti)

## Firebase config

V `e-on/quiz/index.html` je zatím ponechán Firebase config z ČD verze (`cd-quiz-e6e3f`) — funguje out-of-the-box. Pro ostrý workshop E.ON je lepší vytvořit vlastní Firebase projekt, viz `e-on/quiz/SETUP.md`.

## Pravidla pro úpravy

- Kvízová data jsou hardcoded v JS (pole `QUIZ_DATA` v `e-on/quiz/index.html`) — edituj přímo tam
- Formát otázky: `question`, `options {A,B,C,D}`, `correct`, `comment`
- Zdroj pro fakta: integrovaná výroční zpráva E.ON SE 2024 (PDF ve složce `masterclass/quiz/` — mimo tento worktree)
- Nemazat a nepřepisovat soubory v `ceske-drahy/research/` ani `_archive/` bez souhlasu
