# lowmagic.github.io (`lowmag.cc`)

Zero-build static site for **[lowmag.cc](https://lowmag.cc)** (GitHub Organization Pages for [@lowmagic](https://github.com/lowmagic)).

Because `.nojekyll` is present, GitHub Pages serves `index.html`, `style.css`, and `assets/` directly with no Ruby/Node build step. Any repository in `lowmagic` with GitHub Pages enabled automatically mounts at `https://lowmag.cc/<repo>/` (for example, `https://lowmag.cc/chimera-tts/`).

## Zero-Downtime Cutover to `lowmag.cc`

`CNAME` is intentionally omitted on initial push so pushing `lowmagic/lowmagic.github.io` makes `https://lowmagic.github.io/` live immediately **without** breaking `https://lowmagic.github.io/chimera-tts/` before DNS propagates.

1. Push this repo to GitHub:
   ```sh
   gh repo create lowmagic/lowmagic.github.io --public --source=. --remote=origin --push
   ```
2. At your DNS registrar for `lowmag.cc`, add GitHub Pages apex records:
   - `A` `@` → `185.199.108.153`
   - `A` `@` → `185.199.109.153`
   - `A` `@` → `185.199.110.153`
   - `A` `@` → `185.199.111.153`
   - `CNAME` `www` → `lowmagic.github.io`
3. Once `dig +short lowmag.cc` returns those IPs, enter `lowmag.cc` under `github.com/lowmagic/lowmagic.github.io/settings/pages` (GitHub commits `CNAME` and provisions TLS) and check **Enforce HTTPS**.
4. In `github.com/organizations/lowmagic/settings/domains`, verify `lowmag.cc` via TXT record for the green **Verified** badge on `@lowmagic`.

## Adding Screenshots / Static UI Demos

- **Idea Machine screenshot:** Drop `assets/screenshots/im-web.png` and swap the `.ui-preview` block in `index.html` (marked with an HTML comment) if you want a full-bleed capture alongside or in place of the structured card preview.
- **Interactive Idea Machine demo:** Enable GitHub Pages on `lowmagic/ideamachine` publishing a static export of `im web` against public sample transcripts—it will automatically go live at `https://lowmag.cc/ideamachine/`.

## Local Preview

```sh
python3 -m http.server 8080
```
