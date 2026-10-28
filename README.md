# hagames.uz — HA Games sayti

Studiyaning ochiq sayti: bosh sahifa, har bir o'yin uchun alohida bo'lim (do'kon havolalari, xaridlar, yordam, privacy). Bir vaqtning o'zida GitHub Pages'da ham (`one2223.github.io/hagames-privacy/`) ishlaydi — eski do'kon havolalari buzilmasligi uchun.

## Tuzilma
| Yo'l | Nima | App Store Connect'da |
|---|---|---|
| `home.html` | Bosh sahifa: barcha o'yin va ilovalar | — |
| `<o'yin>/index.html` | O'yin sahifasi: tavsif, do'kon tugmalari, xaridlar, yordam (FAQ, kontakt) | **Marketing URL** va **Support URL** |
| `<o'yin>/privacy.html` | O'sha o'yinning privacy policy'si | **Privacy Policy URL** |
| `assets/site.css` | Umumiy uslub (yorug'/qorong'i rejim) | — |
| `app-ads.txt` | Reklama tarmoqlari qatorlari (domen ildizida bo'lishi shart) | — |

O'yinlar: `commute-jam/` (yangi tuzilmada), `blob-merge/`, `find-top/` (sahifa yangi, privacy hozircha eski faylda), `one-pos/`.

**Eski fayllar o'zgartirilmaydi** — ular hozir chiqqan ilovalarning do'kon sahifalarida ko'rsatilgan: `bm.html` (Blob Merge), `findtop.html` (Find Top), `index.html` va `privacy-policy.html` (Forest Strike). Do'kon sahifalaridagi havolalar `hagames.uz/<o'yin>/privacy.html` ga o'tkazilgach, ular yangi joyga ko'chiriladi va eski fayllar yo'naltirishga (redirect) aylanadi.

## Yangi o'yin qo'shish
1. `<o'yin>/` papkasi: `index.html` (mavjud o'yin sahifasidan nusxa) va `privacy.html`.
2. `home.html` ga kartochka.
3. Yangi reklama tarmog'i qo'shilsa — `app-ads.txt` ga qator.

## Server (DevOps)
`https://hagames.uz` — Nginx shu reponi statik beradi:
```nginx
root /srv/hagames-site;          # shu repo (git pull)
index home.html index.html;      # "/" -> home.html; papkalarda index.html
location = /app-ads.txt { default_type text/plain; }
location / { try_files $uri $uri.html $uri/ =404; }
```
`api.hagames.uz` — alohida (backend), bu repoga aloqasi yo'q.
