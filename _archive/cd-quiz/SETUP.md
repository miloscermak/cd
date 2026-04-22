# Jak nasadit ČD Kvíz — krok za krokem

## 1. Založit Firebase projekt (5 minut)

1. Jdi na **console.firebase.google.com**
2. Klikni **Add project** → pojmenuj třeba `cd-quiz`
3. Klikni **Continue** → Google Analytics nepotřebuješ (vypni) → **Create project**
4. V levém menu klikni **Build → Realtime Database**
5. Klikni **Create Database** → vyber **europe-west1** → **Start in test mode** → **Enable**
6. V levém menu klikni **Project Overview** (ikona domečku)
7. Klikni na ikonu **</>** (Web) → pojmenuj app `quiz` → **Register app**
8. Uvidíš `firebaseConfig` objekt — **zkopíruj ho**

## 2. Vložit config do kódu (1 minuta)

Otevři `index.html` a najdi řádky 789–796. Nahraď placeholder za svůj config:

```javascript
const firebaseConfig = {
    apiKey: "AIzaSy...",           // tvůj klíč
    authDomain: "cd-quiz.firebaseapp.com",
    databaseURL: "https://cd-quiz-default-rtdb.europe-west1.firebasedatabase.app",
    projectId: "cd-quiz",
};
```

Ulož soubor.

## 3. Nasadit na Netlify (2 minuty)

1. Jdi na **app.netlify.com**
2. Přihlas se (GitHub, email — jedno)
3. Přetáhni celou složku `quiz/` na stránku **Sites** (drag & drop deploy)
4. Netlify ti dá URL, např. `https://cd-quiz-abc123.netlify.app`
5. Volitelně: v **Site settings → Domain management** přejmenuj na hezčí URL

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
- Pokud chceš testovat lokálně: otevři `index.html` přes local server (např. `npx serve .`)
