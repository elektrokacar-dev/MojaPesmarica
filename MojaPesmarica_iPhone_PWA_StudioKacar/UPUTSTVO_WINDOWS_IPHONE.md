# Moja Pesmarica 1.0 – Studio Kačar · PWA za iPhone/iPad

Ovo je **druga iOS opcija**: instalacija na početni ekran preko Safarija, bez Xcode-a, bez Apple developerskog potpisa i bez isteka posle sedam dana.

## VAŽNO: ovo nije IPA datoteka

PWA se mora postaviti na javno dostupan **HTTPS** sajt. Sam ZIP ili otvaranje `index.html` iz iPhone Files aplikacije **nisu dovoljni** za punu offline instalaciju i servisni radnik (service worker). Hosting može biti besplatan, npr. GitHub Pages ili Cloudflare Pages.

## Najjednostavnije objavljivanje (Windows)

1. Raspakujte ZIP. Datoteke `index.html`, `app.js`, `style.css`, `sw.js`, `manifest.webmanifest` i folder `icons` moraju ostati zajedno.
2. Otvorite https://pages.cloudflare.com/ ili https://pages.github.com/ .
3. Na Cloudflare Pages kreirajte projekat i izaberite **Direct Upload** / **Upload assets** ako je ta opcija dostupna; pošaljite **sadržaj** raspakovanog foldera, tako da `index.html` bude u korenu sajta. Ako koristite GitHub Pages, učitajte datoteke u GitHub repozitorijum, uključite **Settings → Pages → Deploy from branch → main / root**. Sačekajte dobijenu HTTPS adresu.
4. Na iPhone-u tu HTTPS adresu otvorite u **Safari** pregledaču.
5. Izaberite **Share / Deli → Add to Home Screen / Dodaj na početni ekran** (na novijem iOS-u opcija može biti u meniju Share → More).
6. Pokrenite ikonicu **Moja Pesmarica**. Pri prvom otvaranju posetite sve kartice sa internetom kako bi se resursi učitali; nakon uspešnog keširanja pesme i liste rade bez interneta.

Kada se sajt jednom uspešno učita i servisni radnik instalira (prvi put može biti potrebno osvežiti stranicu), aplikacija radi sa početnog ekrana bez obnavljanja razvojnog potpisa. Ipak, to nije trajna garancija za lokalne podatke: brisanje Safari podataka, resetovanje uređaja ili upravljanje memorijom iOS-a može ukloniti lokalne podatke. Redovno izvozite **⋮ → Napravi rezervnu kopiju** u iCloud Drive ili Files i ne oslanjajte se samo na memoriju uređaja.

## Šta radi

- Internet pretraga preko LRCLIB-a (potreban internet), otvaranje Pesmarica.rs i po izboru Google-a u novoj kartici. Pesmarica.rs se ne čita automatski zbog različitog sajta i ograničenja pristupa.
- Sačuvane pesme, izvođači A–Z, omiljene, uređivanje, deljenje, pojedinačno i **grupno brisanje** (Moje pesme → Alati → Obriši više pesama).
- U grupnom brisanju postoji pretraga, izbor više pesama, „Označi sve prikazane“, poništavanje izbora i obavezna potvrda. Izbrisane pesme se uklanjaju iz korisničkih lista, ali same liste ostaju.
- Korisničke liste, redosled pesama, režim nastupa, A−/A+, osam brzina, svetla/tamna pozadina.
- Izvoz i uvoz JSON rezervne kopije formata `moja-pesmarica` / `setlists`, kompatibilan sa Android aplikacijom. DEMO uvoz odbija celu datoteku koja bi prešla 15 pesama; ništa se ne briše.
- ⋮ → Uvoz i alati ili Moje pesme → Alati: uvoz TXT, uvoz PDF tekstualnog sloja i grupno brisanje; ostale stavke menija su podešavanja, rezervne kopije, aktivacija, info. PDF uvoz učitava biblioteku sa CDN-a pri prvom korišćenju i zahteva internet. PDF sa skeniranim fotografijama bez tekstualnog sloja nije podržan za OCR. PDF se uvozi kao **jedan nacrt** koji možeš ručno razdvojiti, za razliku od naprednijeg Android uvoza.
- DEMO: 15 pesama. FULL: neograničeno, uz verifikaciju potpisanih SK1 kodova.

## FULL aktivacija

1. U iPhone aplikaciji ⋮ → **Aktiviraj FULL** → **Kopiraj ID instalacije**.
2. ID pošalji Studiju Kačar. Kod se izdaje postojećim **privatnim licencnim alatom** za taj ID.
3. Nalepi ceo `SK1.…` kod u aplikaciji i klikni Aktiviraj FULL. Privatni ključ **nije** u ovom PWA paketu.
4. Android FULL kod nije automatski važeći na iPhone-u jer je vezan za drugi ID.

Ovaj sistem je primer direktne distribucije preko sajta, a ne Apple App Store prodaje. Ako se PWA postavlja na javni sajt, obezbedite pravne informacije, privatnost i odgovarajuća prava za sadržaj.

## Testiranje na Windows-u pre postavljanja

Ako imate Python: otvorite PowerShell u raspakovanom folderu i pokrenite `py -m http.server 8080`, zatim na istom računaru `http://localhost:8080`. Offline režim sa početnog ekrana radi kada je aplikacija objavljena na HTTPS adresi. Samo za lokalno testiranje nije potrebno izdavati sertifikat.

**Napomena o hostingu:** Bez javnog HTTPS linka, ne mogu direktno instalirati PWA na vaš iPhone iz ove datoteke. Kod je spreman da ga sami postavite na hosting. 

## Nadogradnja na GitHub Pages bez gubitka pesama

Ako već imate prethodnu PWA verziju na GitHub Pages, zamenite fajlove u **istom folderu i na istoj HTTPS adresi**; ne menjajte domen ni putanju. IndexedDB skladište i format rezervne kopije ostaju nepromenjeni. Sačuvajte rezervnu kopiju pre ažuriranja. Posle objavljivanja sačekajte GitHub Pages, na iPhone-u otvorite adresu u Safari-ju i osvežite je; po potrebi potpuno zatvorite i ponovo pokrenite aplikaciju sa početnog ekrana da novi servisni radnik učita izmenjene datoteke. Ne brišite staru ikonicu/website data pre kopije.

Ova PWA nadogradnja uključuje **grupno brisanje** kao na Androidu, ali ne uključuje Android OCR kameru ni automatsko razdvajanje pesama iz skeniranog PDF-a.
