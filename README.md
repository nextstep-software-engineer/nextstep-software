# Astro Starter Kit: Basics

```sh
npm create astro@latest -- --template basics
```

> 🧑‍🚀 **Seasoned astronaut?** Delete this file. Have fun!

## 🚀 Project Structure

Inside of your Astro project, you'll see the following folders and files:

```text
/
├── public/
│   └── favicon.svg
├── src
│   ├── assets
│   │   └── astro.svg
│   ├── components
│   │   └── Welcome.astro
│   ├── layouts
│   │   └── Layout.astro
│   └── pages
│       └── index.astro
└── package.json
```

To learn more about the folder structure of an Astro project, refer to [our guide on project structure](https://docs.astro.build/en/basics/project-structure/).

## 🧞 Commands

All commands are run from the root of the project, from a terminal:

| Command                   | Action                                           |
| :------------------------ | :----------------------------------------------- |
| `npm install`             | Installs dependencies                            |
| `npm run dev`             | Starts local dev server at `localhost:4321`      |
| `npm run build`           | Build your production site to `./dist/`          |
| `npm run preview`         | Preview your build locally, before deploying     |
| `npm run astro ...`       | Run CLI commands like `astro add`, `astro check` |
| `npm run astro -- --help` | Get help using the Astro CLI                     |

## 👀 Want to learn more?

Feel free to check [our documentation](https://docs.astro.build) or jump into our [Discord server](https://astro.build/chat).

## 🎨 Icon credits

The 8 solution-card icons in `src/components/WhatWeDo.astro` were fetched from
the [Iconify](https://iconify.design/) API (`api.iconify.design`), sourced
from the **Tabler Icons** set ([MIT license](https://github.com/tabler/tabler-icons/blob/master/LICENSE)).
Verify licensing status directly at [icon-sets.iconify.design/tabler](https://icon-sets.iconify.design/tabler/) if needed.

| Card                    | Iconify icon name              |
| ------------------------ | ------------------------------- |
| Engineering Software     | `tabler:device-desktop-cog`     |
| Product Lifecycle Management (PLM) | `tabler:cube`         |
| Cloud Engineering        | `tabler:cloud`                  |
| AI & Analytics           | `tabler:brain`                  |
| Software Development     | `tabler:code`                   |
| DevOps                   | `tabler:infinity`               |
| Industrial IoT           | `tabler:antenna-bars-5`         |
| Digital Transformation   | `tabler:trending-up`            |

Fetched via `curl "https://api.iconify.design/tabler:<name>.svg"` and inlined
as raw SVG path data (no runtime dependency on Iconify).

### Stats bar icons (`src/components/StatsBar.astro`)

Also Tabler Icons (MIT), same fetch method as above.

| Stat                  | Iconify icon name       |
| ---------------------- | ------------------------ |
| Projects Delivered     | `tabler:rocket`          |
| Engineering Experts    | `tabler:users-group`     |
| Countries Served       | `tabler:world`           |
| Years of Experience    | `tabler:award`           |
| Client Satisfaction    | `tabler:mood-smile`      |

### Trust bar brand logos (`src/components/TrustBar.astro`, `public/icons-iconify/`)

Real company logos, fetched as full SVG files (not inlined) and saved to
`public/icons-iconify/`. Sourced from Iconify's **Logos** collection (brand
logos, license varies per trademark owner — these are the companies' own
marks, used here to indicate technologies we work with) except Azure, which
came from the **Devicon** wordmark variant because `logos:microsoft-azure` is
icon-only (no text). Google Cloud uses `logos:google-cloud` (icon only) paired
with a plain text label styled in the component — Devicon's Google Cloud
wordmark is a vertically-stacked lockup (icon large, text tiny below it) that
reads poorly at logo-strip sizes, so a real icon + independently-sized text
gives more control over proportions.

| Brand         | Iconify icon name                  | Saved as                                       |
| -------------- | ------------------------------------ | ------------------------------------------------- |
| Microsoft      | `logos:microsoft`                    | `public/icons-iconify/microsoft.svg`              |
| AWS            | `logos:aws`                          | `public/icons-iconify/aws.svg`                    |
| Azure          | `devicon:azure-wordmark`             | `public/icons-iconify/azure.svg`                  |
| Google Cloud   | `logos:google-cloud` (icon only)     | `public/icons-iconify/google-cloud-icon.svg`      |
| SAP            | `logos:sap`                          | `public/icons-iconify/sap.svg`                    |

Note: the Azure SVG had its `viewBox` cropped (via a `getBBox()` measurement)
to remove excess padding in the original file, and its `width`/`height`
attributes changed from `1em` to explicit pixel values matching the new
viewBox — browsers otherwise render `<img>`-embedded SVGs with `1em`
dimensions as a square, ignoring the viewBox aspect ratio.

Siemens has no logo asset (none found on Iconify) — it's rendered as styled
text instead. Oracle and PTC (shown in the Home.png mockup) were intentionally
left out per a prior request.

### Industries We Empower icons (`src/components/IndustrySection.astro`)

Also Tabler Icons (MIT), same fetch method as above.

| Industry                  | Iconify icon name       |
| -------------------------- | ------------------------ |
| Automotive                 | `tabler:car`             |
| Healthcare                 | `tabler:shield-plus`     |
| Financial Services         | `tabler:building-bank`   |
| Energy & Utilities         | `tabler:bolt`            |
| Retail & E-commerce        | `tabler:shopping-cart`   |
| Logistics & Supply Chain   | `tabler:truck-delivery`  |
| Telecommunications         | `tabler:broadcast`       |
| Government                 | `tabler:building-pavilion` |
| Education & Research       | `tabler:school`          |
| And Many More               | `tabler:dots`            |

### Our Engineering Process icons (`src/components/ProcessSection.astro`)

Also Tabler Icons (MIT), same fetch method as above.

| Step       | Iconify icon name         |
| ---------- | -------------------------- |
| Discover   | `tabler:search`            |
| Architect  | `tabler:file-analytics`    |
| Develop    | `tabler:code`               |
| Test       | `tabler:clipboard-check`    |
| Deploy     | `tabler:rocket`             |
| Support    | `tabler:headset`            |

### Case study thumbnails (`src/components/CaseStudies.astro`)

Real case-study photography doesn't exist yet as a site asset, so each
thumbnail uses the standard designer "image placeholder" convention instead:
a diagonal cross (hand-drawn SVG, not fetched) plus the `tabler:photo`
mountain/frame icon (Tabler Icons, MIT, via Iconify) centered on top.
