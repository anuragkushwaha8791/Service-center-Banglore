# Service Center CRM  (React edition)

Ek hi `index.html` file poora CRM hai. Koi server nahi, koi paid service nahi.
Data aapke **Firebase (free / Spark plan)** me rehta hai, website **GitHub Pages** (free) se chalti hai.

## Is folder me kya hai

| File / folder        | Kaam                                                                                  |
|----------------------|----------------------------------------------------------------------------------------|
| `index.html`         | Poora app (React + sab code andar hi hai). Yahi GitHub Pages par chalta hai.           |
| `firestore.rules`    | Database ke security rules. **GitHub se kaam nahi karta** – Firebase Console me paste karna hai (neeche step 3). |
| `SECURITY_CHECKLIST.txt` | Safety ke steps (API key restriction, App Check, roles).                          |
| `source/`            | Code ka source (sirf tab chahiye jab future me code badalna ho).                       |
| `.nojekyll`, `.gitignore` | GitHub ke liye chhoti settings files. Inhe rehne do.                              |

## 1) GitHub par daalna (website banana)

1. github.com par naya repository banao (naam jaise `service-center-crm`). Free plan par Pages ke liye repository **Public** hona chahiye.
   Isme koi password/secret nahi hai – Firebase ki web key secret nahi hoti, data rules se surakshit hai (SECURITY_CHECKLIST.txt dekho).
2. **Add file → Upload files** → is folder ki **saari files aur `source` folder** drag karke daalo → **Commit changes**.
3. Repository me **Settings → Pages → Build and deployment → Source: Deploy from a branch → Branch: `main` / `(root)` → Save**.
4. 1–2 minute baad address milega: `https://<aapka-username>.github.io/<repository-name>/`

## 2) Firebase me ek baar

1. **Authentication → Settings → Authorized domains → Add domain**: `<aapka-username>.github.io`
2. **Authentication → Sign-in method → Email/Password** enabled hona chahiye.
3. **Firestore Database → Rules** me `firestore.rules` ka poora text paste karke **Publish** karo.
   (Rules sirf aapke Google account se badalte hain. GitHub me file badalne se Firebase rules nahi badalte – isi liye dost code badal de to bhi aapka data surakshit hai.)
4. Owner login: `operations194@mooving.com` (pehli baar login page par **Owner first-time setup** se password banao).

## 3) Zaroori safety (10 minute ka kaam)

`SECURITY_CHECKLIST.txt` ka **A** aur **B** section zaroor karo (Firebase project me sirf aap rahein, aur API key ko apni website tak restrict karo).

## 4) Code / website update karna

* Sirf `index.html` badalni ho: GitHub me file kholo → pencil/Upload se nayi `index.html` daalo → Commit. 1–2 minute me live. Browser me `Ctrl+F5`.
* Source se dobara banana (optional): Node.js (v20+) install karo, phir
  ```
  cd source
  npm install
  npm run build        # ../index.html dobara ban jata hai
  ```
  Code `source/src/` me hai: `logic.js` (CRM ka dimaag), `ui.jsx` (React screens), `styles.css`, `store.js`, `main.jsx`.

## 5) 10 saal tak bina maintenance – sach kya hai

* Koi database server / hosting server aapke paas nahi hai, isliye maintenance lagbhag zero hai.
* Sirf ek bahari cheez: Firebase ki libraries Google ke server se load hoti hain, **version pinned hai (`10.13.2`)**.
  Google purane versions aam taur par barson hosted rakhta hai, par guarantee nahi deta.
  **Saal me ek baar** site kholkar login karke dekh lo. Agar kabhi na khule to `source/src/logic.js` me `FBV="10.13.2"` ko naye version se badalkar dobara build karo (ya kisi developer se 5 minute ka kaam karwa lo).
* Firebase free plan: 1 GB data, roz 50,000 reads / 20,000 writes. App isi ke hisaab se bana hai (entries 5 → 10 → 20 karke load hoti hain).
* Har mahine **Full Backup (JSON)** download karke Google Drive me rakho (Admin Settings → Backup). App 30 din baad yaad dilata hai.
* Firestore me **TTL policy kabhi on mat karna** (wo data delete kar deti hai). Activity Log 40 din baad apne aap saaf hota hai – entries kabhi nahi.
* Kam se kam maheene me ek baar koi login kare, taaki project active rahe.
