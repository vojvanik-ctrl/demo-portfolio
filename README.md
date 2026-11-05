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

Galerie čte `portfolio.json` z kořene portfolia, tedy `https://studentifmk.work/tereza-mala/portfolio.json`. Soubor odpovídá Promptu 1 z „FMK prompty pro studenty“:

```json
{
  "schemaVersion": 1,
  "name": "Tereza Malá",
  "studyProgram": "Marketingová komunikace",
  "bio": "Píšu claimy, kampaně a obsah pro sociální sítě. Portfolio si projdete jako malou procházku večerním Zlínem.",
  "countryCode": "CZ",
  "portfolioUrl": "https://studentifmk.work/tereza-mala/",
  "photoOriginal": "assets/fmk/portrait-original.png",
  "photoStamp": null
}
```

- Cesty k obrázkům jsou relativní vůči `portfolio.json` (bez úvodního lomítka), takže fungují i v podadresáři.
- `bio` má 107 znaků (limit je 180).
- **Razítkový portrét zatím chybí.** Vytvořte ho Promptem 2 z fotografie `assets/fmk/portrait-original.png`, uložte jako `assets/fmk/portrait-stamp.png` (PNG s průhledným pozadím, 4:5, ideálně 1200 × 1500 px) a teprve potom vyplňte `"photoStamp": "assets/fmk/portrait-stamp.png"`. Do té doby galerie ukáže dočasný stav.
- Číslo složky přiděluje galerie, v souboru není.
- Jméno, obor a fotografie jsou na stránce zapsané přímo v `index.html`. Při změně profilu je upravte na obou místech; automatická synchronizace se `portfolio.json` zapojená není.

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
