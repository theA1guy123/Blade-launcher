# Blade Launcher

Eaglercraft launcher. Light entry page, then a switchable sidebar/top-bar shell that loads each
section in an iframe. Only the client you actually launch gets downloaded.

## Structure

```
index.html        entry page — just the CONTINUE button (loads launcher.html in an iframe)
launcher.html     the shell: sidebar/top-bar nav + page iframe + full-window game stage
home.html         normal versions (7) + launch
custom.html       modded / custom-GUI clients (9 — 6 bundled + 3 online)
packs.html        resource packs (14) with download buttons
settings.html     accent colour, light mode, menu position, launch options
about.html        about + tips + credits
assets/           blade.css, logo.png, bg.jpg
clients/          the client HTML files (loaded on demand)
packs/            the resource pack .zip files (served as downloads)
```

Open **index.html**. Everything else is reached from there.

## Putting it on GitHub Pages

1. Make a new repository (public).
2. Upload the **contents of this folder** to the repo root — keep `assets/`, `clients/`
   and `packs/` as folders.
3. Repo **Settings → Pages → Source: Deploy from a branch**, branch `main`, folder `/ (root)`, Save.
4. Wait a minute, then open `https://<your-username>.github.io/<repo-name>/`.

Notes:
- Every file here is under GitHub's 100 MB per-file hard limit. The biggest is
  `clients/26_2.html` at 72 MB.
- Total is about 607 MB, which fits GitHub Pages' 1 GB published-site limit.
- Upload via the web UI in a few batches, or with git if you have it
  (`git add . && git commit -m "blade" && git push`).
- Because Pages serves over https, the settings sync and pack downloads work properly —
  better than opening the files locally.

## Client files

`clients/` should contain these exact names:

| File | Version |
|---|---|
| `1_8_8.html` | 1.8.8 (EaglercraftX 1.8 u53 signed) |
| `1_12_2.html` | 1.12.2 (u3 WASM-GC) |
| `1_14_4.html` | 1.14.4 |
| `1_16.html` | 1.16 |
| `1_20_6.html` | 1.20.6 |
| `1_21_11.html` | 1.21.11 |
| `26_2.html` | 26.2 (0.5) |
| `shadownet.html` | ShadowNet Client (1.12.2 WASM) |
| `tuff.html` | Tuff Client |
| `pixelclient.html` | PixelClient 3 (1.12.2) |
| `astra.html` | Astra Client |
| `ebclient.html` | EB Client Nextgen CU5 |
| `gxclient.html` | GX Client |

Three custom clients are **online** rather than bundled — they load from their own sites and
need internet:

| Client | URL |
|---|---|
| Precision Client | `https://rocketmcc-network.github.io/clients/Precision/index.html` |
| Apollo Client | `https://rocketmcc-network.github.io/clients/apollo/index.html` |
| Modern Client (WASM) | `https://wasm.modernclient.online/` |

If one of those sites goes down or gets blocked on a school network, that entry stops working —
the bundled clients keep working regardless.

## Adding or removing things

- **A version**: drop the client HTML in `clients/`, then add a line to the `V` array near the
  bottom of `home.html` (`name`, `file`, `size`, `desc`).
- **A custom client**: same, but the `C` array in `custom.html` (also takes `mc`).
- **A resource pack**: drop the `.zip` in `packs/`, then add a line to the `P` array in
  `packs.html` (`name`, `mc`, `size`, `file`).

No build step — they're plain HTML files, edit and save.
