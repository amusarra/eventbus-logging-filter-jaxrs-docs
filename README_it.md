# Documentazione Quarkus Event Bus Logging Filter JAX-RS

[![Keep a Changelog v1.1.0 badge](https://img.shields.io/badge/changelog-Keep%20a%20Changelog%20v1.1.0-%23E05735)](CHANGELOG.md)
[![License: MIT](https://img.shields.io/badge/license-CC--BY--NC--SA--4.0-lightgrey)](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.it)

[![Maven AsciiDoc to PDF](https://github.com/amusarra/eventbus-logging-filter-jaxrs-docs/actions/workflows/build_asciidoc_to_pdf.yml/badge.svg)](https://github.com/amusarra/eventbus-logging-filter-jaxrs-docs/actions/workflows/build_asciidoc_to_pdf.yml)
[![Build AsciiDoc to HTML5](https://github.com/amusarra/eventbus-logging-filter-jaxrs-docs/actions/workflows/build_asciidoc_to_html_github_page.yml/badge.svg)](https://github.com/amusarra/eventbus-logging-filter-jaxrs-docs/actions/workflows/build_asciidoc_to_html_github_page.yml)
[![Deploy Antora Site to Pages](https://github.com/amusarra/eventbus-logging-filter-jaxrs-docs/actions/workflows/build_antora_site.yml/badge.svg)](https://github.com/amusarra/eventbus-logging-filter-jaxrs-docs/actions/workflows/build_antora_site.yml)

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
│           ├── nav.adoc               # Navigazione Antora
│           ├── pages/                 # Pagine Antora (una per capitolo)
│           ├── partials/              # Partials AsciiDoc (contenuto capitoli + attributi)
│           │   ├── _attributes-common.adoc
│           │   ├── _attributes-pdf.adoc
│           │   └── chapters/          # File sorgente dei capitoli
│           └── images/                # Immagini della documentazione
├── src/main/docs/asciidoc/            # Sorgenti Maven Asciidoctor (PDF/HTML5)
│   ├── index.adoc                     # Documento master per PDF/HTML5
│   ├── attributes/                    # Attributi per PDF/HTML5
│   ├── chapters/                      # File capitoli (copie - per build Maven)
│   └── resources/                     # Temi e immagini per build Maven
├── antora-playbook.yml                # Playbook Antora (sviluppo locale)
├── antora-playbook-prod.yml           # Playbook Antora (produzione / CI)
└── package.json                       # Dipendenze Node.js per Antora
```

## Requisiti

### Per la generazione PDF e HTML5 (Maven)
Per la generazione della documentazione nei formati supportati, è necessario avere installato sul proprio sistema
(postazione di sviluppo o CI/CD) i seguenti software:
- Java JDK 11 o superiore
- Maven 3.8.x o superiore
- Mermaid CLI 10.8.4 o superiore

[Mermaid CLI](https://www.npmjs.com/package/@mermaid-js/mermaid-cli?activeTab=readme) è un tool per la generazione di diagrammi di flusso, sequenza, Gantt e classi a partire da codice sorgente;
all'interno della documentazione sono presenti alcuni diagrammi generati tramite Mermaid.

L'installazione di questo tool è possibile tramite il package manager npm per cui è richiesto la disponibilità di Node.js
sul sistema (versione ^14.13 || >=16.0).

```shell script
npm install -g @mermaid-js/mermaid-cli
```
Console 0 - Installazione di Mermaid CLI

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

```shell script
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
| `antora-playbook-prod.yml` | Playbook per produzione (usato da CI/CD) |

### Configurazione dei Playbook Antora

Sono forniti due playbook:

- **`antora-playbook.yml`** — Per lo sviluppo locale. Usa il filesystem locale come sorgente e produce output in `target/antora-site/`.
- **`antora-playbook-prod.yml`** — Per build CI/CD di produzione. Usa il repository GitHub come sorgente e produce output in `build/site/`.

### Supporto per i Diagrammi

Il sito Antora usa [Kroki](https://kroki.io/) tramite l'estensione `asciidoctor-kroki` per il rendering dei diagrammi
(Mermaid, PlantUML, ecc.) definiti nei sorgenti AsciiDoc. I diagrammi sono renderizzati server-side dal servizio Kroki
pubblico — non è richiesta alcuna installazione locale di tool per i diagrammi nelle build Antora.

## Pubblicazione della documentazione HTML su GitHub Pages
La documentazione HTML generata è disponibile anche su [GitHub Pages](https://amusarra.github.io/eventbus-logging-filter-jaxrs-docs/). Questo è possibile grazie alla GitHub Actions [Deploy AsciiDoc to Pages](.github/workflows/build_asciidoc_to_html_github_page.yml)
che si occupa di pubblicare la documentazione HTML generata (tramite il plugin Maven di AsciiDoc) su GitHub Pages.

Il sito Antora è pubblicato tramite il workflow GitHub Actions [Deploy Antora Site to Pages](.github/workflows/build_antora_site.yml),
attivato ad ogni push sul branch `main` quando cambia il contenuto sotto `docs/`.
