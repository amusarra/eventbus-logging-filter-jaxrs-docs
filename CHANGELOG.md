# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- `supplemental-ui/partials/footer-content.hbs` — Footer personalizzato del sito Antora con copyright © Antonio Musarra's Blog ([dontesta.it](https://www.dontesta.it)), link al profilo GitHub ([amusarra](https://github.com/amusarra)) e profilo LinkedIn ([amusarra](https://www.linkedin.com/in/amusarra))

### Changed
- Adeguamento della GitHub Action per il supporto a Node.js 24: aggiornamento del file `build_docs.yml` con `FORCE_JAVASCRIPT_ACTIONS_TO_NODE24: true` a livello di workflow per optare in anticipo su Node.js 24 e prevenire warning di deprecazione

### Removed
### Deprecated
### Security

## [1.4.1] - 2026-04-15

### Added
- Contenuto documentazione per la release software **1.4.1**:
  - `05_2_realizzazione_del_resource_endpoint.adoc` — Sezione "Aggiornamento v1.4.1 — Endpoint reattivo": documenta il nuovo endpoint `POST /api/rest/echo/reactive` che restituisce `Uni<Response>` abilitando il percorso non-bloccante (event-loop) di Quarkus REST
  - `05_3_realizzazione_del_filtro_jax_rs.adoc` — Sezione "Aggiornamento v1.4.0 — Filtro annotation-based e pattern capture-only": documenta l'adozione delle annotazioni `@ServerRequestFilter`/`@ServerResponseFilter` di RESTEasy Reactive e il pattern capture-only che delega serializzazione e pubblicazione al `TraceEventDispatcher`
  - `05_6_adeguamento_filtro_jax_rs.adoc` — Sezione "Aggiornamento v1.4.0 — Nuove proprietà di configurazione del dispatcher": documenta le due nuove property (`app.trace.dispatcher.queue.capacity` e `app.trace.dispatcher.drain.sleep-ms`) che controllano la coda bounded e il thread di drain di `TraceEventDispatcher`
  - `05_7_realizzazione_dispatcher_e_event_handler.adoc` — Sezione "Aggiornamento v1.4.0 — TraceEventDispatcher ad alte prestazioni": descrive l'architettura del nuovo `TraceEventDispatcher` (thread daemon dedicato, `ArrayBlockingQueue` bounded con backpressure) e include la tabella dei benchmark comparativi (v1.3.0 → v1.4.0: throughput +10–15%, latenza media −11–14%, latenza p95 −17–22%, errori zero)
  - `08_conclusioni.adoc` — Sezione "Evoluzioni nella versione 1.4.x": riepilogo sintetico di tutti i miglioramenti architetturali e dei risultati misurabili introdotti nelle versioni 1.4.0 e 1.4.1
- Supporto multi-versione Antora: creazione del branch `release/1.4.1` (versione stabile corrente) e `release/1.3.0` (versione stabile precedente)
- Link navbar "Info sui download" dinamico con variabile Handlebars `{{page.version}}` per URL versione-consapevoli nel version switcher Antora

### Changed
- Tutti i playbook Antora aggiornati per referenziare i branch di release espliciti:
  - `antora-playbook.yml` — `HEAD` → `release/1.4.1`
  - `antora-playbook-ci.yml` — `HEAD` → `release/1.4.1` + commento aggiornato per riflettere la strategia multi-branch
  - `antora-playbook-prod.yml` — `main` → `release/1.4.1`
- Allineamento versioni in tutti i file di configurazione:
  - `docs/antora.yml` — `version: '1.4.1'`, `display_version: '1.4.1 (Quarkus 3.34.3)'`, `quarkus-version: '3.34.3'`, `project-version: '1.4.1'`; aggiunto campo `name: eventbus-logging-filter-jaxrs` richiesto da Antora 3.x
  - `pom.xml` — `<software.version>1.4.1</software.version>`, `<quarkus.version>3.34.3</quarkus.version>`; `<revnumber>` ora usa `${software.version}` anziché `${project.version}`; aggiunti attributi AsciiDoc globali (`project-version`, `quarkus-version`, `github-url`, `github-docs-url`, `diagram-server-url`, `diagram-server-type`)
  - `docs/modules/ROOT/partials/_attributes-common.adoc` — `:revnumber: v1.4.1`, `:revdate: Aprile 2026`
  - Playbook (`antora-playbook*.yml`) — `project-version: '1.4.1'`, `quarkus-version: '3.34.3'`
- `README.md` e `README_it.md` — Rimosso il requisito di installazione di Mermaid CLI (`mmdc`): il rendering dei diagrammi avviene ora via Kroki remoto

### Fixed
- Rendering diagrammi Mermaid/PlantUML: migrazione da `mmdc` CLI locale (richiedeva Puppeteer/Chrome, causa di errori CI `"mmdc failed: Generating single mermaid chart"`) al servizio remoto [Kroki](https://kroki.io) tramite attributi `diagram-server-url` e `diagram-server-type` in `pom.xml`
- GitHub Actions — warning di deprecazione Node.js 20: aggiunto `FORCE_JAVASCRIPT_ACTIONS_TO_NODE24: true` come variabile d'ambiente a livello di workflow in `build_docs.yml` per optare in anticipo su Node.js 24
- Livelli heading AsciiDoc fuori sequenza nei nuovi paragrafi di aggiornamento: corretti `====` → `==` in `05_2`, `05_3`, `05_6`, `05_7` e `===` → `==` in `08_conclusioni` eliminando i warning Antora `"section title out of sequence"`

## [1.3.0] - 2026-04-15

### Added
- Workflow GitHub Actions unificato `.github/workflows/build_docs.yml` che sostituisce i tre workflow separati (`build_asciidoc_to_pdf.yml`, `build_asciidoc_to_html_github_page.yml`, `build_antora_site.yml`): genera PDF e HTML5 via Maven, produce il sito Antora con `antora-playbook-ci.yml` e pubblica tutto su GitHub Pages in un'unica pipeline
- `antora-playbook-ci.yml` — Playbook Antora ottimizzato per CI che usa la sorgente locale già checkouttata (`url: .`) garantendo coerenza con l'ultimo commit senza dipendenze di rete
- `docs/modules/ROOT/pages/downloads.adoc` — Pagina Antora con tabella dei formati disponibili (PDF, HTML5 ZIP), istruzioni per la generazione manuale e informazioni sulla licenza
- Dropdown **📥 Download** nella navbar Antora (`supplemental-ui/partials/header-content.hbs`) con link diretti a PDF, HTML5 ZIP e pagina info download
- Voce `📥 Download` nel sidebar di navigazione (`docs/modules/ROOT/nav.adoc`)
- Attributo `downloads-url` in tutti i playbook Antora e in `docs/antora.yml` per risolvere `{downloads-url}` nelle pagine AsciiDoc
- Copia automatica del PDF generato in `build/site/downloads/eventbus-logging-filter-jaxrs-docs.pdf` (servito come file statico su GitHub Pages)
- Creazione automatica dello ZIP HTML5 in `build/site/downloads/eventbus-logging-filter-jaxrs-docs-html5.zip`
- Upload di PDF e HTML5 come artefatti GitHub Actions con retention 90 giorni (scaricabili dalla scheda Actions)

### Changed
- `README.md` e `README_it.md` — Aggiornati: badge CI unificato, struttura progetto aggiornata, sezione CI/CD riscritta con descrizione della pipeline unificata e della funzionalità di download dall'UI Antora, configurazione playbook aggiornata a tre playbook

### Removed
- `.github/workflows/build_asciidoc_to_pdf.yml` — sostituito dal workflow unificato `build_docs.yml`
- `.github/workflows/build_asciidoc_to_html_github_page.yml` — sostituito dal workflow unificato `build_docs.yml`
- `.github/workflows/build_antora_site.yml` — sostituito dal workflow unificato `build_docs.yml`

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