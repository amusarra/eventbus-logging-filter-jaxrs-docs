# Quarkus Event Bus Logging Filter JAX-RS Documentation

[![Keep a Changelog v1.1.0 badge](https://img.shields.io/badge/changelog-Keep%20a%20Changelog%20v1.1.0-%23E05735)](CHANGELOG.md)
[![License: MIT](https://img.shields.io/badge/license-CC--BY--NC--SA--4.0-lightgrey)](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.it)

[![Maven AsciiDoc to PDF](https://github.com/amusarra/eventbus-logging-filter-jaxrs-docs/actions/workflows/build_asciidoc_to_pdf.yml/badge.svg)](https://github.com/amusarra/eventbus-logging-filter-jaxrs-docs/actions/workflows/build_asciidoc_to_pdf.yml)
[![Deploy AsciiDocs Pages](https://github.com/amusarra/eventbus-logging-filter-jaxrs-docs/actions/workflows/build_asciidoc_to_html_github_page.yml/badge.svg)](https://github.com/amusarra/eventbus-logging-filter-jaxrs-docs/actions/workflows/build_asciidoc_to_html_github_page.yml)

The **Document as Code (doc-as-code)** approach applies software development principles to the creation, management, and distribution of documentation. This method aims to improve the quality, efficiency, and agility of documentation production by treating documents as part of the project’s source code.

This fosters a culture of documentation that is agilely integrated with software development, allowing for a more efficient workflow, higher quality documentation, and a better overall experience for developers and end users.

This repository contains the source code of the [Quarkus Event Bus Logging Filter JAX-RS](https://github.com/amusarra/eventbus-logging-filter-jaxrs) eBook, illustrating how the project was created and published on GitHub.

The project was developed using the Document as Code (doc-as-code) approach, using [AsciiDoc](https://asciidoc.org/), a lightweight markup language for writing human-readable and machine-readable documents.

The toolchain used for generating the eBook is [Asciidoctor](https://asciidoctor.org/), a text processor supporting AsciiDoc syntax that produces HTML5, DocBook, PDF, and other formats.

Supported outputs for this documentation are: html5 and pdf.

The project uses the [Asciidoctor](https://asciidoctor.org/docs/asciidoctor-maven-plugin/) Maven Plugin, responsible for processing source files in AsciiDoc format and generating the eBook in PDF format.

## Requirements
To generate documentation in the supported formats, the following software needs to be installed on your system (development workstation or CI/CD):

- Java JDK 11 or higher
- Maven 3.8.x or higher
- Mermaid CLI 10.8.4 or higher

[Mermaid CLI](https://www.npmjs.com/package/@mermaid-js/mermaid-cli?activeTab=readme) is a tool for generating flowcharts, sequence diagrams, Gantt charts, and class diagrams from source code; some diagrams in the documentation are generated using Mermaid.


Install this tool via the npm package manager, requiring Node.js (version ^14.13 || >=16.0).

```shell script
npm install -g @mermaid-js/mermaid-cli
```
Console 0 - Install Mermaid CLI


## Generating the eBook
To generate the eBook in PDF format, run the Maven command:

```shell script
mvn clean asciidoctor:process-asciidoc@asciidoc-to-pdf
```
Console 1 - Execute the Maven command to generate the eBook

The Maven command will compile the project and generate the PDF eBook. The generated PDF file will be available in the project’s `target/generated-pdf` folder, named `${project.artifactId}-${project.version}.pdf`.

## Generating HTML Documentation
To generate HTML documentation, run the Maven command:

```shell script
mvn clean asciidoctor:process-asciidoc@asciidoc-to-html
```
Console 2 - Execute the Maven command to generate the HTML docs

The Maven command will compile the project and generate the HTML documentation. The HTML documentation will be available in the project’s `target/generated-html5` folder.

## Publishing HTML Documentation on GitHub Pages
The generated HTML documentation is also available on [GitHub Pages](https://amusarra.github.io/eventbus-logging-filter-jaxrs-docs/). This is made possible by the GitHub Actions [Deploy AsciiDoc to Pages](.github/workflows/build_asciidoc_to_html_github_page.yml), which publishes the generated HTML documentation (via the AsciiDoc Maven plugin) to GitHub Pages.
