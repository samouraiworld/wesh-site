# wesh.samourai.app

Static website for Wesh, the free, non-profit, open-source emergency messaging app published by Samouraï Coop. When the mobile network or the Internet is cut off, phones pass messages to each other over Bluetooth.

Plain hand-written HTML5 and one stylesheet (`style.css`). No JavaScript, no build step, no cookies, no analytics, no external fonts, scripts or CDNs. Every page carries a Content-Security-Policy that only allows same-origin styles and images, so the site cannot make a third-party request even by mistake. The donate button is a plain link to Tipeee: nothing from Tipeee is embedded.

The visual style follows the Wesh "Pavé" design system: asphalt (night) and chalk (day) themes picked from the system setting, system fonts only, condensed 900 headings, hi-vis yellow reserved for "public".

## Layout

| Page | French (primary) | English |
| --- | --- | --- |
| Home | `index.html` → `/` | `en/index.html` → `/en/` |
| Privacy | `confidentialite.html` → `/confidentialite` | `en/privacy.html` → `/en/privacy` |
| Terms | `conditions.html` → `/conditions` | `en/terms.html` → `/en/terms` |
| Support | `support.html` → `/support` | `en/support.html` → `/en/support` |
| Child safety | `protection-mineurs.html` → `/protection-mineurs` | `en/child-safety.html` → `/en/child-safety` |
| Transparency | `transparence.html` → `/transparence` | `en/transparency.html` → `/en/transparency` |
| Donations | `dons.html` → `/dons` | `en/donate.html` → `/en/donate` |
| Security | `securite.html` → `/securite` | `en/security.html` → `/en/security` |
| Legal notice | `mentions-legales.html` → `/mentions-legales` | `en/legal.html` → `/en/legal` |

Other files:

- `privacy.html`, `terms.html`: redirect stubs, because the store listings and the legal documents announce `/privacy` and `/terms` for English.
- `404.html`: bilingual, uses absolute paths (GitHub Pages serves it at any depth).
- `.well-known/security.txt`: RFC 9116 file. Renew `Expires` before it passes (at most one year ahead).
- `CNAME`: `wesh.samourai.app`.
- `.nojekyll`: disables Jekyll so `.well-known/` is published and files are served as is.
- `robots.txt`, `favicon.svg`.

GitHub Pages serves `confidentialite.html` at `/confidentialite`, so the extensionless URLs in the store listings work. Internal links use relative `.html` paths so the site also works when opened from disk.

Preview locally: `python3 -m http.server 8000` in this folder, then open http://127.0.0.1:8000/.

## Publishing

GitHub Pages deploys the `main` branch, folder `/ (root)`, on the custom domain `wesh.samourai.app` with HTTPS enforced. The domain `samourai.app` is verified for the `samouraiworld` organisation, so no other account can claim the subdomain.

DNS, in the `samourai.app` zone:

```
wesh  CNAME  samouraiworld.github.io.
```

Every change goes through a pull request; never commit to `main` directly.

## Editing rules

- The privacy policy and terms reproduce the V1 legal documents (`POLITIQUE-CONFIDENTIALITE.md`, `CONDITIONS-UTILISATION.md`). Change the source documents first, then the pages, and update the version date.
- French and English pages must say the same thing.
- Text that only holds while Internet mode ships sits between `<!-- INTERNET:START -->` and `<!-- INTERNET:END -->`, as in the app's privacy policy. Keep these markers paired.
- Do not announce availability in a given country or a release date until it is confirmed.
- Never use « anonyme », « intraçable », « sécurisé », "anonymous", "untraceable" or "secure" as a promise.
- Hi-vis yellow (`--public`) is a fill for "public" only, never a text colour.
- Keep the site free of third-party requests: no web fonts, no embeds, no scripts.
- When the apps are published, add the App Store, Google Play and APK links in the "Télécharger" / "Download" section, with the APK SHA-256 and signing-certificate fingerprint.
