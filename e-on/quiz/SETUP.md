# Jak nasadit E.ON Kvíz — krok za krokem

## 1. Založit Firebase projekt (5 minut)

1. Jdi na **console.firebase.google.com**
2. Klikni **Add project** → pojmenuj třeba `eon-quiz`
3. Klikni **Continue** → Google Analytics nepotřebuješ (vypni) → **Create project**
4. V levém menu klikni **Build → Realtime Database**
5. Klikni **Create Database** → vyber **europe-west1** → **Start in test mode** → **Enable**
6. V levém menu klikni **Project Overview** (ikona domečku)
7. Klikni na ikonu **</>** (Web) → pojmenuj app `quiz` → **Register app**
8. Uvidíš `firebaseConfig` objekt — **zkopíruj ho**

## 2. Vložit config do kódu (1 minuta)

Otevři `index.html` a najdi blok `firebaseConfig` v JS sekci. Nahraď ho svým configem:

```javascript
const firebaseConfig = {
    apiKey: "AIzaSy...",
    authDomain: "eon-quiz.firebaseapp.com",
    databaseURL: "https://eon-quiz-default-rtdb.europe-west1.firebasedatabase.app",
    projectId: "eon-quiz",
};
```

Ulož soubor. (Pozn.: zatím je v kódu ponechán původní Firebase projekt z ČD verze — funguje out-of-the-box, ale pro ostrý workshop doporučuji vlastní.)

## 3. Nasadit na Netlify (automaticky přes git push)

Tento repo má `netlify.toml`, který publish directory ukazuje na `e-on/quiz`. Po pushi do `main` se Netlify deploy spustí sám.

Pokud děláš první setup:
1. Jdi na **app.netlify.com** → **Add new site → Import from Git**
2. Zvol tento repo, branch `main`
3. Netlify si přečte `netlify.toml` — žádná další konfigurace
4. Volitelně: v **Site settings → Domain management** nastav hezčí URL

## 4. Jak to funguje na workshopu

**Ty (presenter):**
1. Otevři URL v prohlížeči na projektoru
2. Klikni **Vytvořit kvíz** → vygeneruje se kód místnosti + QR kód
3. Řekni účastníkům, ať naskenují QR nebo zadají kód
4. Ovládej kvíz tlačítky: **Odhalit odpověď** → **Další otázka**

**Účastníci (voter):**
1. Naskenují QR kód nebo otevřou URL a zadají kód
2. Vidí otázku a 4 tlačítka
3. Kliknou na odpověď → „Hlasováno!"
4. Po odhalení vidí, jestli měli pravdu

## Poznámky

- Firebase free tier zvládne 100 simultánních připojení — pro 50 lidí v pohodě
- Test mode u Realtime Database vyprší za 30 dní — pro jednorázový workshop stačí
- Žádná data se neukládají trvale, po workshopu můžeš Firebase projekt smazat
- Lokální test: `npx serve .` ve složce `e-on/quiz`
