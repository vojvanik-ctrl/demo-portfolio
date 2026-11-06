# Tereza Malá – Malá procházka mým portfoliem

Hratelné studentské portfolio: jednoduchá 2D skákačka ve večerním modelovém Zlíně. Statický web bez backendu, bez knihoven a bez externích požadavků. Funguje na desktopu i na mobilu.

> Fiktivní studentské portfolio vytvořené jako ukázka pro předmět Creative Competitions and Portfolio Building (FMK UTB).

## Co je ve složce

| Soubor | K čemu je |
| --- | --- |
| `index.html` | Celá stránka: hra, texty, dialogy i ovládání (HTML + CSS + JS v jednom souboru) |
| `assets/img/…` | Obrázky ve formátu WebP (postava, město, auta, projekty) |
| `portfolio.json` | Profil pro Galerii studentských portfolií FMK (schéma `schemaVersion: 1`) |
| `assets/fmk/portrait-original.png` | Původní fotografie Terezy (`photoOriginal`), beze změn |
| `assets/fmk/portrait-stamp-v3.png` | Razítkový portrét pro galerii (`photoStamp`) |
| `assets/img/photo/…` | Zmenšené kopie fotografie pro web (Bez hry, O mně, CV) |
| `og-image.jpg` | Náhled při sdílení odkazu (Facebook, LinkedIn, Messenger…) |
| `.nojekyll` | Říká GitHub Pages, ať soubory jen vystaví a nic nepřekládá |

## Nahrání na GitHub

1. Na GitHubu vytvořte nový repozitář (nebo složku ve společném repozitáři galerie).
2. Přetáhněte do něj **celý obsah této složky** (včetně `assets` a `.nojekyll`), ne jen `index.html`.
3. V repozitáři: **Settings → Pages → Deploy from a branch → `main` / root → Save**.
4. Za minutu je web na adrese, kterou GitHub ukáže v sekci Pages.

## Před zveřejněním doplňte

- **E-mail a CV:** v `index.html` najděte blok `NASTAVENÍ` (hned na začátku skriptu) a vyplňte `contactEmail` a `cvPdf`. Dokud jsou `null`, tlačítka ukazují „Kontakt bude doplněn“ a „CV bude doplněno“.
- **Adresa webu:** počítá se s `https://studentifmk.work/tereza-mala/`. Pokud bude jiná, přepište ji v `portfolio.json` (`portfolioUrl`) a v `index.html` u `og:url` a `og:image`.

## Napojení na společnou galerii

Profil pro galerii je připraven v `portfolio.json` vedle `index.html`. Na skutečném hostingu bude dostupný v kořeni portfolia, včetně případného podadresáře. Nastavená adresa je `https://studentifmk.work/tereza-mala/portfolio.json`, její veřejnou dostupnost se ale nepodařilo ověřit. Tato úprava web nepublikuje ani nezapojuje automatický import společné galerie. Soubor odpovídá Promptu 1 z „FMK prompty pro studenty“:

```json
{
  "schemaVersion": 1,
  "name": "Tereza Malá",
  "studyProgram": "Marketingová komunikace",
  "bio": "Píšu claimy, kampaně a obsah pro sociální sítě. Portfolio si projdete jako malou procházku večerním Zlínem.",
  "countryCode": "CZ",
  "portfolioUrl": "https://studentifmk.work/tereza-mala/",
  "photoOriginal": "assets/fmk/portrait-original.png",
  "photoStamp": "assets/fmk/portrait-stamp-v3.png"
}
```

- Cesty k obrázkům jsou relativní vůči `portfolio.json` (bez úvodního lomítka), takže fungují i v podadresáři.
- `bio` má 107 znaků (limit je 180).
- **Razítkový portrét je vložen.** Jediná verze je `assets/fmk/portrait-stamp-v3.png` (6. 11. 2026, PNG 1122 × 1402 px s průhledným pozadím, přibližně 4:5). Starší varianty byly odstraněny; zůstávají jen v historii repozitáře. V galerii se zobrazuje v ploše 4:5 s `object-fit: contain`, bez natahování. Původní fotografie i její webové kopie zůstaly zachovány.
- Číslo složky přiděluje galerie, v souboru není.
- **Společný zdroj jména a oboru:** při spuštění přes HTTP nebo HTTPS stránka načítá `portfolio.json` a používá jeho `name` a `studyProgram` ve shodných profilových polích, přehledu Bez hry, O mně a CV. Změny se projeví po novém načtení stránky. Otevíraný dialog se aktualizuje i při pozdějším doběhnutí požadavku. Text se vkládá bezpečně jako text, nikoli jako cizí HTML.
- **Náhradní údaje pro offline náhled:** při otevření přes `file://`, nedostupném JSONu nebo chybě zůstávají vložené původní údaje v HTML; hra se nezastaví. Při přejmenování profilu upravte i tyto náhradní údaje a statické meta popisky pro sdílení.
- `bio`, `countryCode` a `portfolioUrl` jsou samostatná galerijní data. Krátké `bio` nenahrazuje delší text O mně. Vyprávění, umělecké podklady, statické SEO popisky a optimalizované webové kopie fotografie se automaticky nepřepisují. Razítkový portrét se na osobním webu automaticky nezobrazuje místo původní fotografie.
- Hodnoty `countryCode: "CZ"` a `portfolioUrl` byly již v dodaném profilu. Byly zachovány, nikoli odhadnuty ze jména či fotografie. Před zveřejněním potvrďte skutečnou cílovou adresu. Po publikování musí `portfolio.json` vracet JSON, nikoli náhradní HTML stránku.

## Lokální náhled

Stačí otevřít `index.html` dvojklikem. Pro věrný test jako na webu:

```
python3 -m http.server 8000
```

a pak otevřít `http://localhost:8000`.

## Ovládání

- Desktop: ← → / A D pohyb, mezerník / ↑ / W skok, E / Enter otevře projekt, Esc zavře.
- Mobil: dvě šipky vlevo, skok a otevření vpravo.
- **Bez hry:** celý obsah (O mně, 6 projektů, CV) bez hraní. Nic není zamčené za skóre.
- Tlačítko pauzy zastaví okolní pohyb (dopravu, světla). Při `prefers-reduced-motion` je okolní pohyb vypnutý rovnou.

## Ověření úprav pro galerii

Příprava proběhla lokálně 6. listopadu 2026. JSON byl ověřen spolu s limitem popisku a existencí obou obrázků. Stránka se nadále spouští jako statický web bez sestavení a bez nových služeb. Veřejné nasazení touto úpravou nevzniklo; aktuální veřejnou dostupnost nastavené adresy se nepodařilo ověřit.

### Co bylo skutečně ověřeno

- Platný JSON se správnými poli, 107 znaků v popisku a existující odkazy na původní i aktuální razítkový portrét.
- Lokální HTTP server vrátil `portfolio.json` jako JSON a oba obrázky jako PNG při provozu v podadresáři.
- JavaScript prošel kontrolou syntaxe. Testy přímo z vloženého profilového modulu ověřily aktualizaci jména a oboru, bezpečné escapování hodnot, zachování náhradních údajů při chybném JSONu a vynechání požadavku při `file://`.
- Původní fotografie, webové kopie, herní podklady a projektové obrázky zůstaly shodné s dodaným archivem.
- Interakce a vzhled v živém prohlížeči nebyly ověřeny: prostředí blokuje spuštění lokálního prohlížeče a vzdálený prohlížeč nemá přístup k lokálnímu serveru. Veřejná adresa ani nasazení nejsou touto úpravou potvrzeny.
