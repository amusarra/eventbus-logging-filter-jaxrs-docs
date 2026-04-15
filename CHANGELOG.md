# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
### Changed
### Removed
### Deprecated
### Security

## [1.2.0] - 2026-04-15

### Added
- Integrazione di [Antora](https://antora.org/) 3.1.9 per la generazione di un sito di documentazione multi-pagina navigabile
- `docs/antora.yml` — Component descriptor Antora (versione 1.3.0, allineata al progetto software)
- `docs/modules/ROOT/nav.adoc` — Albero di navigazione Antora con tutti i capitoli e sotto-capitoli
- `docs/modules/ROOT/pages/index.adoc` — Landing page del sito Antora con overview e Quick Start
- `docs/modules/ROOT/pages/*.adoc` — 28 pagine Antora (una per capitolo/sezione), thin wrapper che includono i partials con il `leveloffset` appropriato
- `docs/modules/ROOT/partials/chapters/*.adoc` — Contenuto sorgente dei capitoli come partials Antora
- `docs/modules/ROOT/partials/_attributes-common.adoc` — Attributi AsciiDoc comuni
- `docs/modules/ROOT/partials/_attributes-pdf.adoc` — Attributi AsciiDoc specifici per PDF
- `docs/modules/ROOT/images/` — Immagini della documentazione nella struttura Antora
- `antora-playbook.yml` — Playbook Antora per sviluppo locale (output: `target/antora-site/`)
- `antora-playbook-prod.yml` — Playbook Antora per CI/CD produzione (output: `build/site/`)
- `package.json` — Dipendenze Node.js: `@antora/cli`, `@antora/site-generator`, `@antora/lunr-extension`, `asciidoctor-kroki`
- `.github/workflows/build_antora_site.yml` — GitHub Actions workflow per la build e pubblicazione del sito Antora su GitHub Pages
- Badge nel `README.md` per il workflow di deploy Antora

### Changed
- `README.md` — Aggiornato con sezione completa dedicata ad Antora: struttura progetto, requisiti, istruzioni per la generazione del sito e configurazione dei Playbook
- `README_it.md` — Versione italiana dello stesso aggiornamento; badge aggiornati
- `.gitignore` — Aggiunti `node_modules/`, `build/` e `package-lock.json`
- `antora-playbook.yml` e `antora-playbook-prod.yml` — Aggiunto `supplemental_files: ./supplemental-ui` per l'override del template dell'header
- `.github/workflows/build_asciidoc_to_html_github_page.yml` — Convertito da workflow di deploy su GitHub Pages a semplice build artifact (il deploy su Pages è ora esclusivo del workflow Antora)

### Added (2026-04-15 patch)
- `supplemental-ui/partials/header-content.hbs` — Template Handlebars personalizzato che rimuove le voci "Home", "Products", "Services" e "Download" dal navbar dell'UI Antora predefinita, sostituendole con link a GitHub del progetto software e della documentazione

### Refactoring: Unica fonte di verità per il contenuto
- `src/main/docs/asciidoc/index.adoc` — Aggiornato: gli `include::` puntano ora ai partials Antora (`docs/modules/ROOT/partials/`) tramite percorsi relativi (`../../../../docs/modules/ROOT/partials/...`) eliminando la duplicazione del contenuto
- `pom.xml` — Aggiornato: `imagesdir` punta a `${project.basedir}/docs/modules/ROOT/images`; `<resources>` copia le immagini dalla struttura Antora verso l'output HTML5
- Rimossi `src/main/docs/asciidoc/chapters/` — contenuto spostato in `docs/modules/ROOT/partials/chapters/`
- Rimossi `src/main/docs/asciidoc/attributes/` — contenuto spostato in `docs/modules/ROOT/partials/`
- Rimosso `src/main/docs/asciidoc/resources/images/` — immagini ora in `docs/modules/ROOT/images/`
- In `src/main/docs/asciidoc/` rimane solo `index.adoc` (entry point Maven) e `resources/themes/` (temi PDF specifici Maven)

## [1.0.1] - 2024-07-18
- Added the README.md translation in English
- Renamed the README.md file in README_it.md

## [1.0.0] - 2024-06-17
- First release of the project