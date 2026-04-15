# Documentazione Quarkus Event Bus Logging Filter JAX-RS

[![Keep a Changelog v1.1.0 badge](https://img.shields.io/badge/changelog-Keep%20a%20Changelog%20v1.1.0-%23E05735)](CHANGELOG.md)
[![License: MIT](https://img.shields.io/badge/license-CC--BY--NC--SA--4.0-lightgrey)](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.it)

[![Build Docs and Deploy to Pages](https://github.com/amusarra/eventbus-logging-filter-jaxrs-docs/actions/workflows/build_docs.yml/badge.svg)](https://github.com/amusarra/eventbus-logging-filter-jaxrs-docs/actions/workflows/build_docs.yml)

L'approccio **Document as Code (doc-as-code)** è una metodologia che applica i principi dello sviluppo del software alla 
creazione, gestione e distribuzione della documentazione. Questo approccio mira a migliorare la qualità, l'efficienza 
e l'agilità della produzione di documentazione, trattando i documenti stessi come parte del codice sorgente del progetto.

In questo modo, è promossa la cultura di documentazione agilmente integrata con lo sviluppo del software, consentendo 
un flusso di lavoro più efficiente, una maggiore qualità della documentazione e una migliore esperienza complessiva 
per gli sviluppatori e gli utenti finali.

Questo repository contiene il codice sorgente dell'eBook **Quarkus Event Bus Logging Filter JAX-RS** che illustra com'è
stato realizzato il progetto [Quarkus Event Bus Logging Filter JAX-RS](https://github.com/amusarra/eventbus-logging-filter-jaxrs), 
pubblicato su GitHub.

Il progetto è stato quindi realizzato usando l'approccio **Document as Code (doc-as-code)**, utilizzato [AsciiDoc](https://asciidoc.org/), un 
linguaggio di markup testuale per scrivere documenti leggibili sia da esseri umani che da macchine. 

La toolchain utilizzata per la generazione dell'eBook è [Asciidoctor](https://asciidoctor.org/), un processore di testo
che supporta la sintassi AsciiDoc e produce output HTML5, DocBook, PDF e altri formati. A partire dalla versione 1.2.0
del progetto documentale, è supportato anche [Antora](https://antora.org/) per la generazione di un sito di documentazione
multi-pagina navigabile.

Gli output supportati per questa documentazione sono: **html5**, **pdf** e **sito Antora**.

Il progetto fa uso del plugin Maven [Asciidoctor](https://asciidoctor.org/docs/asciidoctor-maven-plugin/), responsabile
della processing dei file sorgente in formato AsciiDoc e della generazione dell'eBook in formato PDF.

## Struttura del Progetto

```
eventbus-logging-filter-jaxrs-docs/
├── docs/                              # Componente Antora (unica fonte di verità)
│   ├── antora.yml                     # Component descriptor Antora (versione: 1.3.0)
│   └── modules/
│       └── ROOT/
│           ├── nav.adoc               # Navigazione Antora (include voce Download)
│           ├── pages/                 # Pagine Antora (una per capitolo + downloads.adoc)
│           ├── partials/              # Partials AsciiDoc (contenuto capitoli + attributi)
│           │   ├── _attributes-common.adoc
│           │   ├── _attributes-pdf.adoc
│           │   └── chapters/          # File sorgente dei capitoli
│           └── images/                # Immagini della documentazione
├── src/main/docs/asciidoc/            # Sorgenti Maven Asciidoctor (PDF/HTML5)
│   ├── index.adoc                     # Documento master (include partials da docs/)
│   └── resources/                     # Temi per la build PDF Maven
├── supplemental-ui/                   # Personalizzazioni UI Antora
│   └── partials/
│       └── header-content.hbs         # Navbar con dropdown 📥 Download
├── antora-playbook.yml                # Playbook Antora (sviluppo locale)
├── antora-playbook-ci.yml             # Playbook Antora (CI — sorgente locale)
├── antora-playbook-prod.yml           # Playbook Antora (produzione — sorgente GitHub)
└── package.json                       # Dipendenze Node.js per Antora
```

## Requisiti

### Per la generazione PDF e HTML5 (Maven)
Per la generazione della documentazione nei formati supportati, è necessario avere installato sul proprio sistema
(postazione di sviluppo o CI/CD) i seguenti software:
- Java JDK 11 o superiore
- Maven 3.8.x o superiore

> **Nota**: I diagrammi Mermaid e altri tipi di diagramma vengono renderizzati in remoto tramite il servizio pubblico [Kroki](https://kroki.io/) — non è necessario installare `mmdc` o Puppeteer localmente.

### Per la generazione del sito Antora
Per la generazione del sito Antora è necessario:

- Node.js 18 o superiore
- npm (incluso con Node.js)

## Generazione dell'eBook
Per generare l'eBook in formato PDF è sufficiente eseguire il comando Maven:

```shell script
mvn clean asciidoctor:process-asciidoc@asciidoc-to-pdf
```
Console 1 - Esecuzione del comando Maven per la generazione dell'eBook

Il comando Maven eseguirà la compilazione del progetto e la generazione dell'eBook in formato PDF. Il file PDF generato
sarà disponibile nella cartella `target/generated-pdf` del progetto con il nome avente il 
pattern `${project.artifactId}-${project.version}.pdf`

## Generazione della documentazione HTML
Per generare la documentazione HTML è sufficiente eseguire il comando Maven:

```shell script
mvn clean asciidoctor:process-asciidoc@asciidoc-to-html
```
Console 2 - Esecuzione del comando Maven per la generazione della documentazione HTML

Il comando Maven eseguirà la compilazione del progetto e la generazione della documentazione HTML. La documentazione 
HTML sarà disponibile nella cartella `target/generated-html5` del progetto.

## Generazione del Sito di Documentazione Antora

[Antora](https://antora.org/) è un generatore di siti di documentazione multi-repository per AsciiDoc. A partire dalla
versione documentale **1.2.0** (allineata alla versione **1.3.0** del progetto software), il progetto supporta Antora
per la generazione di un sito di documentazione multi-pagina navigabile.

### Installazione delle dipendenze Antora

```shell script
npm install
```
Console 3 - Installazione di Antora CLI ed estensioni

### Generazione del sito Antora in locale

```shell script
npm run antora
```
Console 4 - Generazione del sito Antora (playbook locale)

Oppure direttamente con Antora CLI:

```shell
node_modules/.bin/antora antora-playbook.yml
```
Console 5 - Generazione del sito Antora con il playbook locale

Il sito generato sarà disponibile nella cartella `target/antora-site/`. Apri `target/antora-site/index.html`
in un browser per visualizzarlo.

### Struttura del Componente Antora

Il componente Antora si trova nella directory `docs/`:

| Percorso | Descrizione |
|----------|-------------|
| `docs/antora.yml` | Component descriptor — definisce nome, versione (`1.3.0`) e navigazione |
| `docs/modules/ROOT/pages/` | Una pagina AsciiDoc per ogni capitolo/sezione |
| `docs/modules/ROOT/partials/chapters/` | Contenuto sorgente dei capitoli come partials |
| `docs/modules/ROOT/partials/_attributes-common.adoc` | Attributi AsciiDoc comuni |
| `docs/modules/ROOT/images/` | Immagini della documentazione |
| `antora-playbook.yml` | Playbook per sviluppo locale |
| `antora-playbook-ci.yml` | Playbook per produzione (usato da CI/CD) |

### Configurazione dei Playbook Antora

Sono forniti tre playbook:

- **`antora-playbook.yml`** — Per lo sviluppo locale. Usa il filesystem locale come sorgente e produce output in `target/antora-site/`.
- **`antora-playbook-ci.yml`** — Per build CI/CD. Usa la sorgente locale già checkouttata (`url: .`) per garantire coerenza con l'ultimo commit senza latenze di rete. Output in `build/site/`.
- **`antora-playbook-prod.yml`** — Playbook di produzione alternativo. Usa il repository GitHub come sorgente remota; utile per build remoti.

### Supporto per i Diagrammi

Il sito Antora usa [Kroki](https://kroki.io/) tramite l'estensione `asciidoctor-kroki` per il rendering dei diagrammi
(Mermaid, PlantUML, ecc.) definiti nei sorgenti AsciiDoc. I diagrammi sono renderizzati server-side dal servizio Kroki
pubblico — non è richiesta alcuna installazione locale di tool per i diagrammi nelle build Antora.

## CI/CD e GitHub Pages

Un unico workflow GitHub Actions unificato ([Build Docs and Deploy to Pages](.github/workflows/build_docs.yml)) gestisce l'intera pipeline documentale ad ogni push su `main`:

1. **Genera PDF** — tramite Maven (`mvn generate-resources`) → `target/generated-pdf/eventbus-logging-filter-jaxrs-docs-1.0.0.pdf`
2. **Genera HTML5** — tramite Maven → `target/generated-html5/`
3. **Genera sito Antora** — usando `antora-playbook-ci.yml` (sorgente locale) → `build/site/`
4. **Copia i download** — PDF e HTML5 ZIP vengono copiati in `build/site/downloads/` e serviti come file statici su GitHub Pages
5. **Carica artefatti** — PDF e HTML5 vengono caricati come artefatti GitHub Actions (90 giorni) scaricabili dalla scheda Actions
6. **Pubblica su GitHub Pages** — il `build/site/` completo (sito Antora + downloads) viene pubblicato su [https://amusarra.github.io/eventbus-logging-filter-jaxrs-docs/](https://amusarra.github.io/eventbus-logging-filter-jaxrs-docs/)

### Download dall'interfaccia Antora

Il sito Antora include un dropdown **📥 Download** nella barra di navigazione superiore con link diretti a:
- 📄 **PDF** — `https://amusarra.github.io/eventbus-logging-filter-jaxrs-docs/downloads/eventbus-logging-filter-jaxrs-docs.pdf`
- 🗜️ **HTML5 ZIP** — `https://amusarra.github.io/eventbus-logging-filter-jaxrs-docs/downloads/eventbus-logging-filter-jaxrs-docs-html5.zip`
- ℹ️ **Pagina info download** — `eventbus-logging-filter-jaxrs/1.3.0/downloads.html`
