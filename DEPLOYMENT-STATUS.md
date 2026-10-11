# Telepítési állapot — 2026-10-12

## Eredmény

A saját repó: [Attikaaaa/playgta5-browser](https://github.com/Attikaaaa/playgta5-browser). Ez jelenleg forrásdokumentációt tartalmaz; működő játékoldal és `github.io` cím még nincs telepítve. Nem állítja, hogy a játék vagy a felhőmentés működik.

## Mi áll rendelkezésre

- A meglévő macOS telepítés helyben működik a `~/Games/PlayGTA5` mappából.
- A játék snapshotja helyben körülbelül 20 GiB és 12 482 fájl.
- A helyi launcher és mentéstükrözés a Macen tárolja a natív mentéseket. Ez nem szinkronizál másik gépre.
- A nyilvános repóba nem kerültek játékbinarik, személyes mentések, böngészőadatok vagy mentéshash-ek.

## Miért nincs még nyilvános játéklink

- A GitHub Pages közzétett oldalának korlátja 1 GiB; a teljes helyi játék ennél jóval nagyobb. A Pages statikus tárhely, ezért önmagában nem tud közös, szerveroldali Story Mode mentéseket tárolni.
- A korábban kipróbált Vercel teljes játéktelepítést HTTP 402-vel letiltották: az akkori körülbelül 21 GiB-os deployment meghaladta a Hobby fiók 10 GiB-os tárolási keretét.
- A Cloudflare Dashboard megnyitásakor bejelentkezési oldalt adott; nincs elérhető bejelentkezett Cloudflare-fiók a telepítéshez.
- A gépen az ellenőrzéskor 4,5 GiB szabad hely volt. A helyi telepítés `build_pages.py` eszköze feldarabolhatja a nagy fájlokat Pages-kompatibilis darabokra, de ez nem csökkenti eléggé a teljes tárhelyigényt, és feltöltési jogosultságot sem ad.
- A géphez kötött API vagy a böngésző IndexedDB-je nem oldja meg az eszközök közötti szinkront. Ehhez működő, hozzáférés-védett felhő API és felhasználónként elkülönített mentéstár szükséges. Közös, nyilvánosan írható mentésvégpont felülírhatóvá tenné a játékosok mentéseit.

## Mentés-ellenőrzés helyi bizonyítéka

A részletes, kizárólag helyben tárolt jegyzőkönyv: `~/Games/PlayGTA5/SAVE-VERIFICATION.md`. A helyi mentések biztonsági másolata a `~/Games/PlayGTA5/saves-backup` alatt van.

- **Tároló létezik:** PASS. A helyi natív játékmentés fájljai és az IndexedDB rekordjai megvoltak.
- **Helyi szerver újraindítása:** PASS. Ugyanazon az eredeten a mentés API HTTP 200-zal indult újra; a helyi natív mentés nem változott.
- **Teljes böngészőleállítás utáni mentéstartalom:** UNVERIFIED. Nem történt kontrollált, dedikált Brave profilban végzett hidegindítási próba.
- **A korábbi, pontos Story Mode checkpoint visszatöltése:** UNVERIFIED. A Story Mode újra elindult egy oldalfrissítés után, de a teszt előtt nem készült összehasonlítható checkpoint-állapotfelvétel. Ez nem Level 3 end-to-end bizonyíték.

A jegyzőkönyv és a mentésfájlok nem kerültek fel erre a nyilvános repóra.

## Hivatkozások

- [GitHub Pages korlátai](https://docs.github.com/en/pages/getting-started-with-github-pages/github-pages-limits)
- [GitHub tervezetekhez tartozó használati keretek](https://docs.github.com/en/billing/reference/product-usage-included)

## Következő technikai feltételek

A játszható, bárhonnan elérhető verzióhoz olyan engedélyezett tárhely kell, amely a teljes játék eszközeit kiszolgálja; ehhez valódi build és feltöltés szükséges. A közös folytatáshoz ezen felül hozzáférés-védett, felhasználói mentéseket külön tároló backend és hidegindítás utáni játékbeli visszatöltési teszt kell. E feltételek nélkül nem adok működőként feltüntetett `github.io` linket.
