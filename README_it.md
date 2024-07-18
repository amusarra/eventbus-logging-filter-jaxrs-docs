# Documentazione Quarkus Event Bus Logging Filter JAX-RS

[![Keep a Changelog v1.1.0 badge](https://img.shields.io/badge/changelog-Keep%20a%20Changelog%20v1.1.0-%23E05735)](CHANGELOG.md)
[![License: MIT](https://img.shields.io/badge/license-CC--BY--NC--SA--4.0-lightgrey)](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.it)

[![Maven AsciiDoc to PDF](https://github.com/amusarra/eventbus-logging-filter-jaxrs-docs/actions/workflows/build_asciidoc_to_pdf.yml/badge.svg)](https://github.com/amusarra/eventbus-logging-filter-jaxrs-docs/actions/workflows/build_asciidoc_to_pdf.yml)
[![Deploy AsciiDocs Pages](https://github.com/amusarra/eventbus-logging-filter-jaxrs-docs/actions/workflows/build_asciidoc_to_html_github_page.yml/badge.svg)](https://github.com/amusarra/eventbus-logging-filter-jaxrs-docs/actions/workflows/build_asciidoc_to_html_github_page.yml)

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
che supporta la sintassi AsciiDoc e produce output HTML5, DocBook, PDF e altri formati.

Gli output supportati per questa documentazione sono: html5 e pdf.

Il progetto fa uso del plugin Maven [Asciidoctor](https://asciidoctor.org/docs/asciidoctor-maven-plugin/), responsabile
della processing dei file sorge in formato AsciiDoc e della generazione dell'eBook in formato PDF.

## Requisiti
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

## Pubblicazione della documentazione HTML su GitHub Pages
La documentazione HTML generata è disponibile anche su [GitHub Pages](https://amusarra.github.io/eventbus-logging-filter-jaxrs-docs/). Questo è possibile grazie alla GitHub Actions [Deploy AsciiDoc to Pages](.github/workflows/build_asciidoc_to_html_github_page.yml)
che si occupa di pubblicare la documentazione HTML generata (tramite il plugin Maven di AsciiDoc) su GitHub Pages.
