# eBook Quarkus Event Bus Logging Filter JAX-RS

[![Keep a Changelog v1.1.0 badge](https://img.shields.io/badge/changelog-Keep%20a%20Changelog%20v1.1.0-%23E05735)](CHANGELOG.md)
[![License: MIT](https://img.shields.io/badge/license-CC--BY--NC--SA--4.0-lightgrey)](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.it)

L'approccio **Document as Code (doc-as-code)** è una metodologia che applica i principi dello sviluppo del software alla 
creazione, gestione e distribuzione della documentazione. Questo approccio mira a migliorare la qualità, l'efficienza 
e l'agilità della produzione di documentazione, trattando i documenti stessi come parte del codice sorgente del progetto.

In questo modo, è promossa la cultura di documentazione agilmente integrata con lo sviluppo del software, consentendo 
un flusso di lavoro più efficiente, una maggiore qualità della documentazione e una migliore esperienza complessiva 
per gli sviluppatori e gli utenti finali.

Questo repository contiene il codice sorgente dell'eBook **Quarkus Event Bus Logging Filter JAX-RS** che illustra com'è
stato realizzato il progetto [Quarkus Event Bus Logging Filter JAX-RS](https://github.com/amusarra/eventbus-logging-filter-jaxrs), 
pubblicato su GitHub.

Il progetto è stato quindi realizzato usando l'approccio **Document as Code (doc-as-code)**, utilizzato asciiDoc, un 
linguaggio di markup testuale per scrivere documenti leggibili sia da esseri umani che da macchine. 

La toolchain utilizzata per la generazione dell'eBook è [Asciidoctor](https://asciidoctor.org/), un processore di testo
che supporta la sintassi AsciiDoc e produce output HTML5, DocBook, PDF e altri formati.

Il progetto fa uso del plugin Maven [Asciidoctor](https://asciidoctor.org/docs/asciidoctor-maven-plugin/), responsabile
della processing dei file sorge in formato AsciiDoc e della generazione dell'eBook in formato PDF.

## Requisiti
Per la generazione dell'eBook è necessario avere installato sul proprio sistema i seguenti software:
- Java JDK 1.8 o superiore
- Maven 3.8.x o superiore

## Generazione dell'eBook
Per generare l'eBook è sufficiente eseguire il comando Maven:

```shell script
mvn clean package
```
Console 1 - Esecuzione del comando Maven per la generazione dell'eBook

Il comando Maven eseguirà la compilazione del progetto e la generazione dell'eBook in formato PDF. Il file PDF generato
sarà disponibile nella cartella `target/generated-docs-basic-theme` del progetto con il nome avente il 
pattern `${project.artifactId}-${project.version}.pdf`
