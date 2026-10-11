# Telepítési állapot — 2026-10-12

## Elvárt cél

A későbbi játékverzió **nem függhet az owner Macjétől**: telepítés és élesítés után ne kelljen helyi Mac-szerver, helyi fájl, futó alkalmazás vagy helyi böngészőprofil. A weboldal, a játékfájlok és a gépek között szinkronizáló mentésszolgáltatás is GitHubon legyen. A mentések felhasználónként privátak és elkülönítettek maradjanak; a jelenlegi személyes mentés nem kerülhet nyilvános repóba.

Ez az állapot **még nincs megvalósítva**.

## Jelenlegi eredmény

A saját repó: [Attikaaaa/playgta5-browser](https://github.com/Attikaaaa/playgta5-browser). A repó jelenleg dokumentációt tartalmaz; működő játékoldal és `github.io` cím még nincs telepítve. Nem állítja, hogy a játék vagy a felhőmentés működik.

## Mi áll rendelkezésre

- A meglévő macOS telepítés helyben működik a `~/Games/PlayGTA5` mappából, de a célverziónak erre nem szabad támaszkodnia.
- A játék snapshotja helyben körülbelül 20 GiB és 12 482 fájl.
- A helyi launcher és mentéstükrözés a Macen tárolja a natív mentéseket. Ez nem szinkronizál másik gépre.
- A nyilvános repóba nem kerültek játékbinarik, személyes mentések, böngészőadatok vagy mentéshash-ek.

## Miért nincs még nyilvános játéklink

- A GitHub Pages közzétett oldalának korlátja 1 GiB; a teljes helyi játék ennél jóval nagyobb. A Pages statikus tárhely, ezért önmagában nem tud közös, szerveroldali Story Mode mentéseket fogadni.
- A korábban kipróbált Vercel teljes játéktelepítést HTTP 402-vel letiltották: az akkori körülbelül 21 GiB-os deployment meghaladta a Hobby fiók 10 GiB-os tárolási keretét. Vercel nem felel meg a GitHub-only követelménynek.
- A Cloudflare Dashboard megnyitásakor bejelentkezési oldalt adott; nincs elérhető bejelentkezett Cloudflare-fiók. Ez egyébként sem felelne meg a most megadott GitHub-only célkitűzésnek.
- A gépen az ellenőrzéskor 4,5 GiB szabad hely volt. A helyi `build_pages.py` feldarabolhat nagy fájlokat, de a teljes adatmennyiséget nem csökkenti a Pages korlátja alá.
- A GitHub Pages nem futtat szerveroldali mentés API-t. Biztonságos, felhasználónként elkülönített mentéshez olyan írási útvonal kell, amely hitelesíti a felhasználót; statikus oldal önmagában erre nem képes.
- GitHub-only tervben külön kell igazolni, hogy a teljes játék eszközei GitHubon tárolhatók és a böngésző számára megbízhatóan kiszolgálhatók, illetve hogy megvalósítható a privát mentéstár. Ezek jelenleg nincsenek beállítva.

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

A cél teljesítéséhez GitHub-kompatibilis eszközterjesztést és biztonságos, bejelentkezett mentésírást kell megvalósítani, majd új eszközön ténylegesen visszatölteni egy Story Mode mentést. A jelenlegi repó ehhez még nem ad futtatható játékot vagy mentésszolgáltatást. Nem szabad a Macet vagy más külső hostot a végleges rendszer részeként használni.
