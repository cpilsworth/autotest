# Page brief: COPD (BPCO) therapy-area page

A spec for recreating the French COPD page of the myAstraZeneca Switzerland HCP portal on Edge Delivery Services, either by re-running the import or by authoring it by hand.

| | |
|---|---|
| **Source** | https://www.myastrazeneca.ch/fr/startseite/therapiegebiete/ri/copd.html |
| **EDS path** | `/fr/startseite/therapiegebiete/ri/copd` |
| **Template** | `ri` (therapy-area pages, `/fr/startseite/therapiegebiete/ri/*`) |
| **Audience** | Healthcare professionals in Switzerland; French; regulatory copy must stay verbatim |
| **Job code** | `CH-12804 05/2026` (last line of the page) |

## Metadata

| Field | Value |
|---|---|
| Title | BPCO - Symptômes, diagnostic et prise en charge |
| Description | En savoir plus sur la bronchopneumopathie chronique obstructive (BPCO) : ses causes, ses symptômes, les approches thérapeutiques actuelles et des informations cliniques importantes pour les proches et les professionnels de la santé. |
| Image | none |

## Page-wide design

Uses the project's existing design system (`styles/styles.css`, `DESIGN.md`); nothing page-specific is needed globally.

- **Colours:** headings in default content and "core" teaser/card titles `--text-color-title-1` #830051 (mulberry); body text `--text-color-body-1` #3c4242; links hover `--text-color-interaction` #d0006f; tinted card ground `--bg-color-supporting-1` #ebefee.
- **Type:** headings Lexia (`--font-display`; Roboto Slab substitute, Lexia is not rehosted); body Inter 16/24. Heading sizes h1 56 / h2 46 / h3 36 / h4 26px from 768px (36 / 36 / 26 / 26 below).
- **Layout:** content capped at 1180px (`--container-max`), 16px gutter on mobile; breakpoint 768px.
- **Prose rhythm:** 16px between heading/paragraph/list (10px mobile); 96px before a heading that follows text in the same section (50px mobile).
- **Section style `spaced`:** 40px top/bottom (20px mobile). Applied server-side on publish, so it does not show in local preview.
- **Header/footer:** shared site fragments (`/nav`, `/footer`), not part of this page.

## Section structure

16 sections, in order. "Default" = default content (headings, paragraphs, lists, links) outside blocks.

| # | Section | Style | Content |
|---|---|---|---|
| 1 | Breadcrumb | | `breadcrumb`: Home › Domaines thérapeutiques › R&I › Bronchopneumopathie chronique obstructive |
| 2 | Hero | | `hero`: desktop image, mobile image, H1 "Bronchopneumopathie chronique obstructive" |
| 3 | Social | | `social-features`: like / share / save row |
| 4 | In-page nav | | `sub-nav-anchors`: Définition, Symptômes, Diagnostic, Traitement, Exacerbations, Recommandations, FAQ (links to the H2 ids below) |
| 5 | Overview | | Default: H2 "Aperçu de la bronchopneumopathie chronique obstructive" + intro. `cta-cards (cols-3, center, title-core, space-md)`: 3 key-figure cards: Incidence en Suisse / Exacerbations / Mortalité |
| 6 | What is COPD | | Default: H3 "Qu'est-ce que la BPCO ?" (paragraphs, list of consequences), H3 "Classification GOLD de la BPCO" |
| 7 | Symptoms | spaced | Default: H2 "Symptômes de la BPCO" + intro. `image-text-band (text-image, text-left, title-core, space-desktop-md)`: "Quels sont les symptômes typiques de la BPCO ?". Back-to-top link |
| 8 | Diagnosis intro | spaced | Default: H2 "Diagnostic de la BPCO et critères de dépistage". `image-text-band (text-left, space-desktop)`: image + intro copy, no title |
| 9 | Diagnosis details | | Default: H3 "Groupes à risque", H3 "Confirmation du diagnostic par spirométrie". `table-bordered`: GOLD stages (3 cols × 4 rows). Caption, text. H3 "Évaluation clinique initiale de la BPCO" + list. `table-bordered`: GOLD A/B/E groups. Caption, text. H3 "Guide de poche GOLD 2026" + download link, H3 "Guide de poche sur la BPCO" + download link. Back-to-top link |
| 10 | Treatment | spaced | Default: H2 "Traitement de la BPCO et options thérapeutiques en Suisse" + intro. `image-text-band (text-image, text-left, title-core, space-md)`: "Traitement de la BPCO : inhalateurs, rééducation et oxygénothérapie". H3s: médicamenteux, GOLD-ABE + `table-bordered` (A/B/E initial vs intensification) + footnotes, inhalation + `table-bordered` (DPI / pMDI / SMI / nébuliseur), Oxygénothérapie, Rééducation pulmonaire, Traitement non pharmacologique (vaccination list). Back-to-top link |
| 11 | Exacerbations | | Default: H2 "Reconnaître et traiter les exacerbations de la BPCO" + intro. `image-text-band (title-core, space-md)`: "Reconnaissance d'une exacerbation aiguë de la BPCO (AECOPD)". `table-bordered`: légère / modérée / sévère criteria (2 cols, lists in cells). H3 "Traitement aigu…", H3 "BPCO : quand une hospitalisation est-elle indiquée ?", flowchart image (alt "Chart1") + source link, H3 "Suivi et prévention". `cta-cards (cols-3, border, center, space-md)`: single card "Fiche d'information sur la BPCO" with DE / FR links |
| 12 | Resources | | Default: H2 "Recommandations et ressources". `cta-cards (cols-3, plain, title-core, space-md)`: 3 PDF cards: Guide de poche sur la BPCO 2025, Recommandations GOLD 2026, Guide de poche GOLD 2026 |
| 13 | FAQ | | Default: H2 "FAQ". `accordion-faq`: 6 question/answer rows |
| 14 | References | | `references`: indication footnote (#TRIXEO AEROSPHERE…), abbreviations, "Références :" + 16 numbered references |
| 15 | Act on COPD | spaced | Default: H2 "Act on COPD". `image-text-band (space-md)`: image + copy + "Découvrir maintenant" → https://www.actoncopd.ch/fr/index.html |
| 16 | Product info | | Default: H2 "Informations utiles sur les produits". `split-teaser`: copy + "Découvrir maintenant" → `/fr/startseite/produkte.html#…` + image. Back-to-top link, job code `CH-12804 05/2026` |

## Blocks

Authoring shapes (rows × cells). Options are added as block classes, e.g. `Cta Cards (cols-3, center)`.

| Block | Status | Shape | Options used here |
|---|---|---|---|
| `breadcrumb` | existing | 1 cell: list of crumb links, current page as text | none |
| `hero` | existing | rows: desktop picture, mobile picture, H1 | none |
| `social-features` | existing | 1 cell: icon | none |
| `sub-nav-anchors` | new | 1 cell: list of `#heading-id` links | none |
| `cta-cards` | existing | 1 row per card: [desktop + mobile picture] [H4 title, copy, CTA] | `cols-3`, `center`, `border`, `plain`, `title-core`, `space-md` |
| `image-text-band` | existing | 1 row: [desktop + mobile picture] [title, copy, CTA] | `text-image`, `text-left`, `title-core`, `space-md`, `space-desktop`, `space-desktop-md` |
| `table-bordered` | new | first row = header; 1 row per table row | none (`no-header` available) |
| `accordion-faq` | new | 1 row per item: [question] [answer] | none |
| `references` | existing | rows: indication note, abbreviations, label + ordered list | none |
| `split-teaser` | existing | 1 row: [copy + CTA] [picture] | none |

`title-core` = mulberry title, used where the source teaser carries `teaser--title-color-core`. The "Fiche d'information" card deliberately has no `title-core` (grey title, as on the source).

## Behaviour

- **In-page nav:** links must target the auto-generated ids of the section H2s: `#aperçu-de-la-bronchopneumopathie-chronique-obstructive`, `#symptômes-de-la-bpco`, `#diagnostic-de-la-bpco-et-critères-de-dépistage`, `#traitement-de-la-bpco-et-options-thérapeutiques-en-suisse`, `#reconnaître-et-traiter-les-exacerbations-de-la-bpco`, `#recommandations-et-ressources`, `#faq`. Renaming a heading breaks its link. Scroll arrows appear only when the list overflows.
- **FAQ:** native expand/collapse, all closed by default.
- **Tables:** shrink to the screen on mobile; horizontal scroll only as a fallback.
- **Back-to-top links** (`#top`) have no target, same as the source.

## Assets

Images are referenced from the source host (`https://www.myastrazeneca.ch/content/dam/intelligentcontent/portals/hcp/ch/de/home/therapiegebiete/r-and-i/chronisch-obstruktive-lungenerkrankung/…` and `/content/intelligentcontent/…/coreimg…` renditions). Most images have a desktop and a mobile version; keep both in blocks. For the flowchart (default content), keep only the desktop version: `aecopd-exacerbation-management-flowchart-fr.png`.

## Regulatory checks

- Job code `CH-12804 05/2026` present and last.
- Indication footnote, abbreviations and all 16 references verbatim, with superscript reference numbers kept in the body text.
- External links unchanged (GOLD, Ligue pulmonaire, swissmedicinfo-pro.ch, actoncopd.ch).

## Recreate by import

The import tooling in `tools/importer/` reproduces this page:

```bash
S=/home/node/.excat-marketplaces/excat-marketplace/excat/skills/excat-content-import/scripts
$S/aem-import-bundle.sh --importjs tools/importer/import-ri.js
node $S/run-bulk-import.js --import-script tools/importer/import-ri.bundle.js \
  --urls tools/importer/urls-ri.txt --force
```

The block mapping, section breaks and `spaced` styles are defined in `tools/importer/page-templates.json` (template `ri`). The cleanup transformer removes header/footer/cookie chrome, rewrites the in-page anchors to heading ids and drops the duplicate mobile flowchart. The importer's "content completeness" warning (~70%) is a known miscount caused by menu and footer text; against page content only the import scores 99.5%.

## Known gaps vs the source

- Section headings at 76–96px gaps on the source get 40px from `spaced` (Symptômes, Traitement, Act on COPD).
- Captions ("Adapté d'après GOLD 2026…") render at body size instead of 12/20px.
- The word "bronchopneumopathie" overflows a 375px screen slightly, as on the source.
