# Angleške besede

Igrive vaje za angleške besede iz šole: kartice, poveži, spomin, poslušaj, kaj manjka, najdi, igra za dva in slovarček.
Aplikacija deluje na Android telefonih in iPhonih, se namesti kot prava aplikacija z ikono in deluje tudi brez povezave.
Ko skrbnik objavi nove besede, jih vsi uporabniki dobijo samodejno.

## Datoteke

| Datoteka | Namen |
|---|---|
| `index.html` | Celotna aplikacija |
| `besede.json` | Objavljene besede (to datoteko posodablja skrbnik) |
| `manifest.webmanifest` | Ime, barve in ikone za namestitev |
| `sw.js` | Delovanje brez povezave in samodejne posodobitve |
| `icon-*.png`, `apple-touch-icon.png` | Ikone |
| `*.woff2`, `pisave-licenca-OFL.txt` | Pisave in njihova licenca |
| `firebase-pravila.json` | Varnostna pravila za igro za dva |
| `android/`, `.github/workflows/apk.yml` | Android aplikacija (APK), ki jo zgradi GitHub |

Datoteke spletne aplikacije so namenoma v eni mapi, da jih lažje naložiš tudi s telefona. Mapi `android` in `.github` sta potrebni samo za APK.

---

## 1. Postavitev na GitHub (enkrat)

Najlažje gre z računalnikom. S telefonom gre tudi, če v Chromu v meniju ⋮ vklopiš »Spletno mesto za računalnike«.

1. Odpri **github.com** in ustvari brezplačen račun. Uporabniško ime bo del naslova aplikacije, zato izberi kratko ime.
2. Desno zgoraj tapni **+** → **New repository**.
   - Repository name: `app_ANG`
   - Izberi **Public**.
   - Tapni **Create repository**.
3. Na strani novega repozitorija tapni **uploading an existing file** (ali **Add file → Upload files**).
4. Povleci ali izberi **vse datoteke** iz razpakirane mape in tapni **Commit changes**.
5. Odpri **Settings → Pages**.
   - Pri **Source** izberi **Deploy from a branch**.
   - Pri **Branch** izberi **main** in **/ (root)**, nato **Save**.
6. Počakaj 1 do 2 minuti in osveži stran. Zgoraj se pokaže naslov, na primer:
   `https://urbanzb.github.io/app_ANG/`

To je povezava, ki jo pošlješ staršem.

## 2. Namestitev na telefon

**Android (Chrome):** povezavo odpri v **Chromu** (ali Samsung Internetu). Aplikacija sama ponudi gumb **Namesti**. Če ga ni, odpri meni **⋮** in izberi **Namesti aplikacijo**. Aplikacija se pojavi med ostalimi aplikacijami.

Če se nameščena aplikacija odpira v drugem brskalniku (npr. DuckDuckGo), nastavi Chrome za privzeti brskalnik ali namesti različico **APK** (razdelek 7).

**iPhone (Safari):** odpri povezavo v Safariju, tapni gumb **Deli** (kvadrat s puščico) in izberi **Dodaj na začetni zaslon**.

Posodobitev aplikacije in besed ni treba nameščati. Zgodi se samodejno ob odprtju, ko je telefon povezan s spletom.

## 3. GitHub žeton za skrbnika (enkrat)

Žeton omogoča, da aplikacija na tvojem telefonu objavlja besede. Ostane samo na tvojem telefonu. **Nikomur ga ne pošiljaj, tudi ne v klepet.**

1. V brskalniku odpri **github.com/settings/personal-access-tokens/new**. (Druga pot: slika desno zgoraj → **Settings** → čisto na dnu levega menija **Developer settings** → **Personal access tokens → Fine-grained tokens → Generate new token**.) Aplikacija GitHub za Android tega ne omogoča.
2. Če je stran na telefonu nepregledna, v meniju ⋮ vklopi **Spletno mesto za računalnike**.
3. Izpolni:
   - **Token name:** `appANG`
   - **Expiration:** izberi najdaljši rok, ki ga GitHub ponudi.
   - **Repository access:** **Only select repositories** → izberi `app_ANG`.
   - **Permissions:** **Add permissions → Contents → Read and write**.
4. Tapni **Generate token** in kopiraj žeton (začne se z `github_pat_`). GitHub ti ga pokaže samo enkrat.
5. V aplikaciji odpri **⚙️ Moje besede in nastavitve → Za skrbnika → Skrbniški način**.
   Uporabnik in repozitorij sta že izpolnjena. Prilepi žeton in tapni **Shrani in preveri**.
   Če piše »Povezava deluje«, je vse pripravljeno.

Če izgubiš telefon, žeton na GitHubu izbriši (isti meni kot zgoraj) in ustvari novega.

## 4. Dodajanje novih besed (vsakič)

1. Fotografiraj nov slovarček besed v zvezku.
2. Pošlji fotografijo Claudu v projektu (glej `navodila-za-claude-projekt.md`) in kopiraj besedilo, ki ga vrne.
   Lahko uporabiš tudi **Google Lens** in kopiraš prebrano besedilo.
3. V aplikaciji odpri **Skrbniški način**, besedilo prilepi v polje **Prilepi seznam besed** in tapni **Preberi besede**.
4. Preveri besede. Izberi temo ali ustvari novo. Kjer je polje za emoji rdeče, ga izberi s tipkovnico emojijev.
5. Tapni **Dodaj besede** in nato **Objavi za vse**.

Ostali bodo nove besede videli v nekaj minutah. Nove besede so 14 dni označene z ✨ in zbrane v temi **Novo**.

## 5. Besede staršev

Starši lahko v **⚙️ → Moje besede** dodajo svoje besede, tudi s prilepljanjem besedila iz Google Lens.
Te besede ostanejo samo na njihovi napravi in se mešajo z besedami iz šole.
Ob menjavi telefona jih izvozijo (**⬇️ Izvozi**) in na novem telefonu uvozijo (**⬆️ Uvozi**).

## 6. Igra za dva (Firebase, enkrat)

Igra za dva poveže dva telefona prek Googlove storitve Firebase. Brezplačni paket zadošča za cel razred.

**A. Ustvari projekt**
1. Odpri **console.firebase.google.com** in se prijavi z Google računom.
2. Ustvari projekt, na primer `appANG`. Google Analytics izklopi.

**B. Vklopi anonimno prijavo**
1. Levo pod **Project shortcuts** tapni **Authentication** (če se pokaže **Get started**, ga tapni).
2. Zavihek **Sign-in method** → **Anonymous** (ali **Add new provider → Anonymous**) → **Enable** → **Save**.

Brez tega koraka preizkus povezave javi napako `auth/admin-restricted-operation`.

**C. Ustvari bazo**
1. Levo **Databases & Storage → Realtime Database** (ne Firestore) → **Create database**.
2. Lokacija: **Belgium (europe-west1)**. Način: **Start in locked mode** → **Enable**.
3. Zavihek **Rules**: izbriši vse in prilepi vsebino datoteke `firebase-pravila.json`, nato **Publish**.

**D. Pridobi nastavitve**
1. **Project Overview → + Add app →** ikona **</>** (Web).
2. Ime `appANG`, Firebase Hosting ne označi, **Register app**.
3. Kopiraj celoten blok `const firebaseConfig = { … }`. Kasneje ga najdeš v **Settings → General → Your apps**.

**E. Vpiši v aplikacijo**
1. V aplikaciji odpri **Skrbniški način → 👫 Igra za dva (Firebase)**.
2. V zgornje polje prilepi celoten `firebaseConfig`. Polje **Database URL** lahko ostane prazno. Tapni **Uporabi nastavitve** in **Preizkusi povezavo**.
3. Ko piše »Povezava s Firebase deluje«, tapni **Objavi za vse**.

Nastavitve Firebase niso skrivnost, saj so v vsaki spletni aplikaciji, ki uporablja Firebase, vidne. Bazo varujejo pravila iz koraka C.

### Kako igrata otroka
1. Prvi otrok izbere temo na začetnem zaslonu, odpre **Igra za dva**, izbere živalco in tapne **Ustvari igro**.
2. Pokaže se štirimestna koda, ki jo pove prijatelju.
3. Drugi otrok odpre **Igra za dva**, vpiše kodo in tapne **Pridruži se**.
4. Izmenjujeta se pri odkrivanju kartic. Kdor najde par, je še enkrat na vrsti.

Igra potrebuje internet na obeh telefonih. Če kateri izmed otrok zapre aplikacijo ali zaklene telefon, se igra lahko prekine.

## 7. Android aplikacija – APK (dodatna možnost)

APK je mala Android aplikacija, ki odpre isto spletno aplikacijo. Besede in igre se posodabljajo samodejno kot doslej, APK pa ni odvisen od brskalnika. Uporabna je za telefone, kjer se nameščena aplikacija odpira v brskalniku. iPhoni še naprej uporabljajo spletno različico.

### Postavitev (enkrat, najlažje z računalnikom)
1. **Naloži mapo `android`:** na GitHubu **Add file → Upload files** in povleci celotno mapo `android` iz razpakiranega arhiva. Tapni **Commit changes**.
2. **Ustvari postopek za gradnjo:** **Add file → Create new file**. Za ime vpiši točno `.github/workflows/apk.yml`, v vsebino prilepi vsebino istoimenske datoteke iz arhiva in tapni **Commit changes**.
3. **Dodaj geslo za podpisovanje:** **Settings → Secrets and variables → Actions → New repository secret**.
   - **Name:** `APK_GESLO`
   - **Secret:** geslo po tvoji izbiri, vsaj 6 znakov. Shrani ga varno, ker z njim podpisuješ vse prihodnje različice.
4. **Zgradi APK:** zavihek **Actions → Zgradi APK → Run workflow**. Po približno 5 minutah se pokaže zelena kljukica.

Ob prvi gradnji GitHub ustvari ključ za podpisovanje in ga šifriranega z geslom shrani kot `android/keystore.enc`. Te datoteke ne briši, sicer starši posodobitev ne bodo mogli namestiti čez staro različico.

### Prenos in namestitev
- Povezava za prenos: **https://github.com/urbanzb/app_ANG/releases/download/apk/Besede.apk**
- V spletni aplikaciji na Androidu je povezava tudi v **⚙️ Nastavitve → Android aplikacija (APK)**.
- Ob odpiranju datoteke telefon vpraša, ali dovoliš namestitev iz tega vira. Dovoli in tapni **Namesti**. Če Play Protect opozori na neznano aplikacijo, izberi **Več podrobnosti → Vseeno namesti**.

### Posodobitve
- Besed in iger ni treba posodabljati, ker se naložijo s spleta.
- APK je treba na novo namestiti le, če se spremeni mapa `android`. GitHub ob vsaki spremembi zgradi novo različico na isti povezavi.

### Google in nepreverjeni razvijalci
Google uvaja preverjanje razvijalcev tudi za aplikacije zunaj Trgovine Play. Ko bo to veljalo v Sloveniji (napovedano za leto 2027), bo namestitev APK nepreverjenega razvijalca zahtevnejša. Takrat je spletna različica (razdelek 2) najpreprostejša pot.

## Zasebnost

Aplikacija nima prijav in ne zbira podatkov. Pisave so priložene, zato tudi Google Fonts ni v uporabi.
Edina zunanja storitev je Firebase pri igri za dva: tam se med igro shranijo le kartice, živalci in točke, brez imen. Igra se izbriše, ko jo ustvarjalec zapusti.
Zvezdice, nastavitve in lastne besede so shranjene samo na napravi.
Datoteka `besede.json` je javna, zato vanjo ne vpisuj imen otrok ali drugih osebnih podatkov.

## Pogoste težave

- **Aplikacija se odpira v brskalniku (npr. DuckDuckGo):** Chrome nastavi za privzeti brskalnik in aplikacijo znova namesti iz Chroma, ali pa namesti APK (razdelek 7). Žeton vpiši v aplikaciji, ki jo dejansko uporabljaš, ker ima vsak brskalnik svojo shrambo.
- **Novih besed ni:** počakaj nekaj minut, zapri aplikacijo in jo odpri znova.
- **»Žeton nima pravice za pisanje«:** pri žetonu preveri dovoljenje **Contents: Read and write** in da je izbran repozitorij `app_ANG`.
- **Slovenske besede se ne izgovarjajo:** naprava nima slovenskega glasu. Aplikacija uporabi hrvaškega, če obstaja. Izgovorjavo lahko izklopiš z gumbom **🔊 SLO**.
- **Napaka v objavljeni besedi:** v skrbniškem načinu besedo izbriši, jo dodaj pravilno in znova objavi. Lahko tudi neposredno uredi `besede.json` na GitHubu.
