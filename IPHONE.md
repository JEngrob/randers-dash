# Randers Dash på iPhone

**Spil nu:** åbn **https://jengrob.github.io/randers-dash/** i Safari på iPhonen, tryk på **Del** og vælg **Føj til hjemmeskærm**.
Så ligger spillet som en app, der også virker uden net.

Spillet er én HTML-fil, så der er tre veje til iPhonen.

## 1. Hurtig test over wifi (virker nu, gratis)

1. Start en lille webserver på Mac'en i mappen `randers-dash`:

   ```bash
   cd ~/Kode/Christina/randers-dash && python3 -m http.server 8765
   ```

2. Åbn Safari på iPhonen (samme wifi som Mac'en) og gå til `http://<Mac'ens IP>:8765`.
   Find Mac'ens IP med `ipconfig getifaddr en0`.
3. Tryk på **Del** (firkanten med pilen) og vælg **Føj til hjemmeskærm**.

Så ligger Randers Dash som en app med ikon og kører i fuld skærm uden Safaris bjælker.
**Begrænsning:** Mac'en og serveren skal være tændt, og telefonen skal være på samme wifi.

## 2. Rigtig web-app, der også virker uden net (gratis – det er den, der bruges nu)

Spillet er allerede klar til det: der er et manifest, et ikon og en service worker (`sw.js`), som gemmer spillet på telefonen.
Det kræver bare, at mappen ligger på en **https**-adresse, fx:

- **GitHub Pages:** læg mappen i et repo og slå Pages til.
- **Netlify Drop** (app.netlify.com/drop): træk mappen ind i browseren.
- **Cloudflare Pages.**

Åbn adressen i Safari, og vælg **Føj til hjemmeskærm**. Herefter starter spillet også i flytilstand, og fremskridt, stjerner og hestesko gemmes på telefonen.

**OBS:** siden bliver offentlig for alle med linket, og den indeholder FC Randers' logo (bane 4). Til privat brug kan man give siden et svært gætteligt navn. Logoet skal fjernes, hvis spillet deles bredt.

## 3. Ægte app via Xcode (Capacitor)

Spillet pakkes ind i en lille iOS-app med en indbygget browser (WKWebView).

1. Installér **Xcode** fra App Store. Det er ikke installeret på Mac'en nu og fylder mange GB.
2. I mappen:

   ```bash
   npm init -y && npm i @capacitor/core @capacitor/cli @capacitor/ios
   ```

   ```bash
   npx cap init "Randers Dash" dk.engrob.randersdash --web-dir www
   ```

   Læg `index.html`, ikoner, `manifest.webmanifest` og `sw.js` i `www/`, og kør:

   ```bash
   npx cap add ios && npx cap open ios
   ```

3. I Xcode:
   - Under *Signing & Capabilities* vælger du dit Apple-id som "Personal Team".
   - Sæt iPhonen til med kabel.
   - Slå *Udviklertilstand* til på telefonen (Indstillinger → Anonymitet & sikkerhed).
   - Tryk ▶.

**Gratis Apple-id:** appen virker i **7 dage** ad gangen og skal derefter installeres igen fra Xcode. Du kan højst have 3 apps.

**Apple Developer Program (99 $ om året):** appen virker i et år, kan deles med familien via **TestFlight**, og kan sendes til App Store.

**App Store:** Apple afviser apps, der bruger andres navn eller logo uden tilladelse. FC Randers' logo og navn kræver klubbens skriftlige accept. Uden den skal bane 4 have et neutralt tema.

## Hvad der allerede er gjort i spillet til iPhone

- Fuld skærm fra hjemmeskærmen, mørk statuslinje og eget ikon (`icon-180.png`).
- Plads til notch og home-streg (safe area).
- Tryk på skærmen = hop. Lyden starter ved første tryk, som iOS kræver.
  Læg mærke til, at **lydløs-knappen på siden** slukker spillets lyd på iPhone.
- På højkant viser spillet "Drej telefonen", for det spilles på tværs.
- Spillet holder pause, hvis man skifter app eller får et opkald.
