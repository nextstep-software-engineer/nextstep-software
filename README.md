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

### Rules for adding icons

Before adding or replacing an icon, verify its license rather than assuming
that every collection available through Iconify has the same terms.

1. Find the icon on the [Iconify icon sets directory](https://icon-sets.iconify.design/).
2. Open the collection page and confirm the collection name, author, license,
   and link to the upstream license.
3. Prefer permissively licensed open-source collections. **Tabler Icons** and
   **Lucide** are currently preferred because both use the MIT license.
4. Record the Iconify identifier (for example, `tabler:cloud`), collection
   license, component using it, and any modifications in this README.
5. Keep the upstream copyright and license notice when its license requires
   one. Do not remove attribution required by the collection.
6. Treat brand-logo collections separately. Availability through Iconify does
   not grant trademark permission; verify the brand owner's usage rules and
   use the mark only to identify the relevant company or technology.
7. Re-check the upstream repository before release if an icon's license is
   unclear or has changed. Do not use icons marked with an unknown, restricted,
   or incompatible license until that status is resolved.

When possible, save or inline the SVG locally so the production site has no
runtime dependency on the Iconify API. Do not alter an icon in a way that
misrepresents its original license or a protected brand mark.

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

### Solutions page icons (`src/components/pages/Solutions.astro`)

The Solutions page uses **Tabler Icons** (MIT) from Iconify, plus the existing
**Lucide** handshake icon (MIT) already used on the People page. Icons that
were already present elsewhere in the site reuse the same inline SVG path
data. New icons are saved locally in `public/icons-iconify/solutions/`, so the
production page has no runtime dependency on the Iconify API.

| Use | Iconify icon name | Source in this project |
| --- | --- | --- |
| Digital Engineering | `tabler:compass` | Local SVG file |
| Product Lifecycle Management | `tabler:cube` | Reused from `WhatWeDo.astro` |
| Custom Software & Enterprise Platforms | `tabler:device-laptop` | Local SVG file |
| Enterprise Integration | `tabler:hierarchy-3` | Local SVG file |
| Artificial Intelligence & Automation | `tabler:brain` | Reused from `WhatWeDo.astro` |
| Cloud, DevOps & Cyber Security | `tabler:cloud-lock` | Local SVG file |
| Engineering First | `tabler:users-group` | Reused from existing Home/People components |
| End-to-End Delivery | `tabler:shield-check` | Local SVG file |
| Global Expertise | `tabler:world` | Reused from existing Home/People components |
| Technology Independent | `tabler:bulb` | Local SVG file |
| Discover | `tabler:search` | Reused from `ProcessSection.astro` |
| Design | `tabler:pencil` | Local SVG file |
| Build | `tabler:hammer` | Local SVG file |
| Integrate | `tabler:route-alt-left` | Local SVG file |
| Deploy | `tabler:rocket` | Reused from `ProcessSection.astro` |
| Support | `lucide:handshake` | Reused from `WhyChooseTeam.astro` |
| Optimise | `tabler:chart-bar` | Local SVG file |

The locally saved SVGs were fetched from `api.iconify.design`, use the site
blue as their stroke color, and otherwise retain the original icon geometry.

### Approach page icons (`src/components/pages/Approach.astro`)

The delivery-step and value-pillar icons use locally inlined SVG paths from
**Tabler Icons**, accessed through Iconify. Tabler Icons is licensed under the
[MIT license](https://github.com/tabler/tabler-icons/blob/master/LICENSE).

| Use | Iconify icon name |
| --- | --- |
| Business Challenge | `tabler:users-group` |
| Discovery & Strategy | `tabler:search` |
| Solution Design | `tabler:edit` |
| Engineering & Development | `tabler:code` |
| Testing & Validation | `tabler:shield-check` |
| Deployment & Integration | `tabler:cloud-upload` |
| Continuous Improvement | `tabler:trending-up` |
| Business Driven | `tabler:target-arrow` |
| Engineering Excellence | `tabler:settings` |
| Modern Technology | `tabler:cloud` |
| Collaborative Partnership | `tabler:users-group` |
| Measurable Outcomes | `tabler:chart-bar` |
| Continuous Innovation | `tabler:rocket` |

The SVGs are decorative and inlined in the component, with no runtime request
to Iconify. Verify the collection license again at
[icon-sets.iconify.design/tabler](https://icon-sets.iconify.design/tabler/)
before replacing them with icons from another collection.

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
| Aerospace Engineering      | `tabler:plane`           |
| Government                 | `tabler:building-pavilion` |
| Compliance & Security      | `tabler:shield-lock`     |
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

## People page (`src/pages/people/`, `src/components/People*.astro`, `src/components/ExecutiveLeadership.astro`, `src/components/WhyChooseTeam.astro`, `src/components/LeadershipQuote.astro`)

### Executive photos

`public/people-karsten-wenschuh.webp`, `public/people-niaz-rahman.webp`, and
`public/people-walter-krutzner.webp` are real, provided headshots (not
derived/AI-generated), resized and re-encoded as optimized webp site assets.

### Logo mark

`public/logo-icon-nextstep.svg` is the gear+rocket icon extracted from the
existing `public/logo-nextstep.svg` wordmark (same vector paths, just the
viewBox cropped to the icon group and the text group excluded) — used for the
Hero's decorative ring graphic and the closing CTA badge, in place of
`favicon.svg`, which is a rasterized PNG unsuitable for that use.

### Icons

Tabler Icons (MIT) and Lucide (MIT) via the Iconify API, plus `logos:linkedin-icon`
(brand mark) for the "View LinkedIn Profile" buttons.

| Use                                    | Iconify icon name          |
| ---------------------------------------- | ----------------------------- |
| Decades of Combined Experience           | `tabler:users-group`          |
| Business First                           | `tabler:target-arrow`         |
| Engineering Excellence                   | `tabler:settings`             |
| Collaborative Partnership                | `lucide:handshake`            |
| Global Perspective                       | `tabler:world`                |
| Long-Term Commitment                     | `tabler:shield-check`         |
| LinkedIn brand mark                      | `logos:linkedin-icon`         |

Each "Key Expertise" list item (`src/components/ExecutiveLeadership.astro`) also
gets its own topic-suitable Tabler icon instead of a repeated bullet:

| Expertise label                  | Iconify icon name         |
| ---------------------------------- | ---------------------------- |
| Executive Leadership               | `tabler:crown`               |
| Software Architecture              | `tabler:sitemap`             |
| Engineering Management             | `tabler:settings-cog`        |
| Digital Transformation             | `tabler:refresh`             |
| Aerospace & Automotive Systems     | `tabler:car`                 |
| Technology Innovation              | `tabler:bulb`                |
| Business Development               | `tabler:trending-up`         |
| Aftersales Transformation          | `tabler:tool`                |
| Six Sigma Black Belt               | `tabler:certificate`         |
| Lean Manufacturing                 | `tabler:building-factory`    |
| Operational Excellence             | `tabler:adjustments`         |
| Executive Advisory                 | `tabler:message-2`           |
| Strategic Technology Advisory      | `tabler:compass`             |
| Enterprise Architecture            | `tabler:building-skyscraper` |
| Technology Modernisation           | `tabler:cpu`                 |
| Software Engineering               | `tabler:code`                |
