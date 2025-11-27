# ✅ INSTALLARE CAPACITOR IN UN PROGETTO VITE + REACT (Build Android)

Questa guida spiega come integrare Capacitor in un progetto Vite + React per generare build Android.

## 1. Installazione di Capacitor

Nel tuo progetto Vite, installare il pacchetto capacitor con:  
`npm install @capacitor/core @capacitor/cli --save`

Installa la piattaforma Android (necessaria prima di aggiungerla):
`npm install @capacitor/android`


## 2. Inizializzazione di Capacitor

Nella root del progetto:
`npx cap init`

Durante l’inizializzazione verranno richiesti:
`Nome app (es. MyApp)`
`ID app (es. com.example.app)`

Questo crea il file `capacitor.config.json`.


## 3. Build del progetto web
Capacitor utilizza la versione build del progetto. Generala con:
`npm run build`

Assicurati che la build finisca in `dist/`.

## 4. Aggiungere la piattaforma Android
Dopo aver installato `@capacitor/android`:
`npx cap add android`

Verrà creata la cartella:
`android/`


## 5. Sincronizzazione dei file
Dopo ogni build web, aggiorna Capacitor con:
`npx cap copy`

oppure:
`npx cap sync`

(sync include anche l’aggiornamento dei plugin)


## 6. Aprire il progetto Android
Per aprire Android Studio con il progetto Capacitor:
`npx cap open android`


## 7. Generare la build Android (APK o AAB)
In Android Studio:
- Seleziona il modulo app.
- Vai su Build → Build Bundle(s) / APK(s).
- Scegli:
  - Build APK(s) → per test locali
  - Build Bundle(s) → per Play Store

Android Studio genererà il file nella cartella `app/build/outputs/`.

## 8. Test su dispositivo o emulatore
Puoi installare l’APK su:
- Emulatore Android
- Dispositivo reale collegato via USB

Ogni modifica richiede:
``` bash,
npm run build
npx cap copy
```

Poi puoi rilanciare l’app dall'emulatore/dispositivo.

## ⚠️ Note importanti
- Capacitor non serve file da un dev-server: Android usa sempre la build statica generata in `dist/`.
- I plugin Capacitor vanno installati via `npm` e sincronizzati con `npx cap sync`.
- `npx cap serve` è utile solo per test web, non per Android.


## 🐱 .gitignore consigliato:
``` gitignore,
# -----------------------------
# Node / Vite / React
# -----------------------------
node_modules/
dist/
dist-ssr/
*.local
.env
.env.*
!.env.example

# Logs
npm-debug.log*
yarn-debug.log*
yarn-error.log*
pnpm-debug.log*

# Editor e sistema
.DS_Store
Thumbs.db
.idea/
.vscode/
*.swp

# -----------------------------
# Capacitor
# -----------------------------
# Cartelle generate automaticamente da Capacitor
android/app/build/
android/app/release/
android/app/profile/
android/.gradle/
android/.idea/
android/local.properties
android/capacitor-cordova-android-plugins/
android/capacitor-cordova-ios-plugins/

# Capacitor plugins
**/build/
**/dist/
plugins/

# Output generati da cap sync/copy
www/

# -----------------------------
# Android / Gradle
# -----------------------------
*.apk
*.aab

# Gradle
.gradle/
build/
**/build/
!android/app/src/main/assets/

# Cache
.cxx/
*.iml

# Keystore (NON VA MAI COMMESSO)
*.jks
*.keystore
*.keystore.old

# Files Android vari
android/app/debug/
android/app/release/
android/*.keystore

# -----------------------------
# JetBrains / IDE vari
# -----------------------------
*.idea/
*.ipr
*.iws

# -----------------------------
# Capacitor iOS (se mai aggiungerai iOS)
# -----------------------------
ios/App/build/
Pods/
*.xcworkspace
DerivedData/
```
