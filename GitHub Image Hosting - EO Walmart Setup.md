# Hosting EO Product Images on GitHub for Walmart

A one-time setup so your Walmart item sheets have clean, direct image URLs. Walmart fetches each image **once** at ingestion and copies it to its own CDN, so you only need this live until the listings show the images — then you can delete it.

---

## Part 1 — GitHub requirements (the non-negotiables)

- **The repository MUST be Public.** Private repos require a login, so their URLs won't work for Walmart.
- **Filenames: no spaces.** Spaces become `%20` in the URL and can break Walmart ingestion. Rename any file with spaces before uploading (keep the `.png` / `.jpg` extension).
- **Keep the file extension** in the name (`...FRONT.png`) — the URL must end in `.png`/`.jpg`.
- **No renaming the folders after upload** — the URL includes the folder path, so moving/renaming breaks every link.
- A free GitHub account is all you need. No paid plan, ever.

## Part 2 — Walmart image spec (so the images actually pass)

Your **2400X2400** folder already satisfies these — use that folder, not the thumbnails.

- **Format:** JPEG, JPG, PNG, or BMP. **No GIF.**
- **Size:** at least 1000 × 1000 px (2400 × 2400 is great).
- **Square**, white or transparent background, product fills most of the frame.
- **No** added text, watermarks, borders, or collages on the main image.
- Walmart recommends **at least 4 images** per listing.
- URL must be **HTTPS** (HTTP hard-fails), **no query strings / tokens / `?…`**, and **no redirect chains**.

---

## Part 3 — Bulk drag-and-drop, step by step

1. **Create a free account:** https://github.com/signup (skip if you have one).
2. **Download the `2400X2400` folder** from your Drive folder "Walmart March 2026" to your computer.
   - Drive folder: https://drive.google.com/drive/folders/1IITnFUClbH2XFLXVM6yraxG5-HWFJs8L
3. **Create a new Public repo:** https://github.com/new
   - Name it with no spaces, e.g. `eo-walmart-images`
   - Select **Public** → **Create repository**
4. **Bulk upload:** in the repo click **Add file → Upload files**, then **drag the entire `2400X2400` folder** onto the page. GitHub keeps the folder structure. Scroll down → **Commit changes**.
   - Tip: if the browser upload struggles with hundreds of files at once, upload one product-type folder at a time (3in1, HAND SOAP, KIDS, LOTION, SANITIZER).

## Part 4 — The URL pattern

Every image becomes:

```
https://raw.githubusercontent.com/USERNAME/REPO/main/2400X2400/TYPE/SIZE/SCENT/FILENAME.png
```

- `main` is the default branch name.
- **Main image** = the product's **FRONT** render.
- **Ingredients / Label image** = the **RIGHT** render.

Example (once your username/repo exist):
`https://raw.githubusercontent.com/tjmay/eo-walmart-images/main/2400X2400/3in1/32oz/CL/EVE_3in1_CL_..._FRONT.png`

---

## Part 5 — Which Drive folder each SKU lives in

Drive path = `2400X2400 › [Type] › [Size] › [Scent code]`. Main image = FRONT, Label image = RIGHT.

**Scent code legend:** CC = Cedar + Citrus · CL = Coconut + Lemon · CM = Citrus + Mint · LA = Lavender + Aloe · PE = Pacific Eucalyptus · PPT = Peppermint Tea Tree · UN = Unscented · VL = Vanilla + Lavender · RG = Ruby Grapefruit · SL = Spearmint + Lemongrass · ML = Meyer Lemon + Mandarin · LC = Lavender + Coconut · BB = Berry Blast · TC = Tropical Coconut · LL = Lavender Lullaby · OS = Orange Squeeze
*(3-in-1 codes are confirmed; Hand Soap / Kids / Sanitizer codes are my best guess — verify against the actual subfolder names.)*

| SKU | Product | Type | Size | Scent |
|---|---|---|---|---|
| 221601 | 3-in-1 Soap Coconut + Lemon | 3in1 | 32oz | CL |
| 221618 | 3-in-1 Soap Citrus + Mint | 3in1 | 32oz | CM |
| 221625 | 3-in-1 Soap Lavender + Aloe | 3in1 | 32oz | LA |
| 224046 | 3-in-1 Soap Cedar + Citrus | 3in1 | 32oz | CC |
| 230054 | 3-in-1 Soap Vanilla + Lavender | 3in1 | 32oz | VL |
| 231044 | 3-in-1 Soap Unscented | 3in1 | 32oz | UN |
| 232065 | 3-in-1 Soap Peppermint + Tea Tree | 3in1 | 32oz | PPT |
| 231655 | 3-in-1 Soap Coconut + Lemon (1 Gal) | 3in1 | 128oz | CL |
| 231129 | Kids Soap Berry Blast | KIDS | 32oz | BB |
| 224039 | Kids Soap Tropical Coconut | KIDS | 32oz | TC |
| 224022 | Kids Soap Lavender Lullaby | KIDS | 32oz | LL |
| 228105 | Kids Soap Orange Squeeze | KIDS | 32oz | OS |
| 232454 | Lotion Coconut + Lemon 8oz | LOTION | 8oz | CL |
| 232461 | Lotion Citrus + Mint 8oz | LOTION | 8oz | CM |
| 232508 | Lotion Unscented 8oz | LOTION | 8oz | UN |
| 232447 | Lotion Vanilla + Lavender 8oz | LOTION | 8oz | VL |
| 232430 | Lotion Lavender + Aloe 8oz | LOTION | 8oz | LA |
| 221632 | Lotion Coconut + Lemon 32oz | LOTION | 32oz | CL |
| 221649 | Lotion Citrus + Mint 32oz | LOTION | 32oz | CM |
| 221656 | Lotion Lavender + Aloe 32oz | LOTION | 32oz | LA |
| 231051 | Lotion Unscented 32oz | LOTION | 32oz | UN |
| 221342 | Hand Soap Meyer Lemon + Mandarin 12.75oz | HAND SOAP | 12.75oz | ML |
| 221359 | Hand Soap Lavender + Coconut 12.75oz | HAND SOAP | 12.75oz | LC |
| 221366 | Hand Soap Spearmint + Lemongrass 12.75oz | HAND SOAP | 12.75oz | SL |
| 230047 | Hand Soap Ruby Grapefruit 12.75oz | HAND SOAP | 12.75oz | RG |
| 231433 | Hand Soap Lavender + Coconut 32oz | HAND SOAP | 32oz | LC |
| 231440 | Hand Soap Meyer Lemon + Mandarin 32oz | HAND SOAP | 32oz | ML |
| 230955 | Hand Soap Meyer Lemon + Mandarin (1 Gal) | HAND SOAP | 128oz | ML |
| 231648 | Hand Soap Ruby Grapefruit (1 Gal) | HAND SOAP | 128oz | RG |
| 232232 | Hand Soap Spearmint + Lemongrass (1 Gal) | HAND SOAP | 128oz | SL |
| 232706 | Hand Soap Pacific Eucalyptus (1 Gal) | HAND SOAP | 128oz | PE |
| 230825 | Hand Sanitizer Spray Coconut + Lemon 6pk | SANITIZER | 2oz | CL |
| 230832 | Hand Sanitizer Spray Lavender + Aloe 6pk | SANITIZER | 2oz | LA |
| 230856 | Hand Sanitizer Spray Ruby Grapefruit 6pk | SANITIZER | 2oz | RG |

## Part 6 — After the listings show the images

Once Walmart displays the images (it has copied them to its own CDN), you can delete the repo:
**Repo → Settings → scroll to "Danger Zone" → Delete this repository.**
Keep it up until every listing is confirmed live, and note you'd need to re-host if you ever resubmit those items.

---

## Part 7 — I'll finish the URLs for you

Once you've created the repo and uploaded the `2400X2400` folder, send me your **GitHub username + repo name**. I'll read the repo's file tree and generate the complete, exact `mainImageUrl` and `labelImageURL` list (all ~68 links) matched to each SKU, ready to paste into the Walmart sheet — so you don't have to click "Raw" on every file.
