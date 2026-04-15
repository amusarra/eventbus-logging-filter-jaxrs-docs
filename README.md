# Quarkus Event Bus Logging Filter JAX-RS Documentation

[![Keep a Changelog v1.1.0 badge](https://img.shields.io/badge/changelog-Keep%20a%20Changelog%20v1.1.0-%23E05735)](CHANGELOG.md)
[![License: MIT](https://img.shields.io/badge/license-CC--BY--NC--SA--4.0-lightgrey)](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.it)

[![Maven AsciiDoc to PDF](https://github.com/amusarra/eventbus-logging-filter-jaxrs-docs/actions/workflows/build_asciidoc_to_pdf.yml/badge.svg)](https://github.com/amusarra/eventbus-logging-filter-jaxrs-docs/actions/workflows/build_asciidoc_to_pdf.yml)
[![Build AsciiDoc to HTML5](https://github.com/amusarra/eventbus-logging-filter-jaxrs-docs/actions/workflows/build_asciidoc_to_html_github_page.yml/badge.svg)](https://github.com/amusarra/eventbus-logging-filter-jaxrs-docs/actions/workflows/build_asciidoc_to_html_github_page.yml)
[![Deploy Antora Site to Pages](https://github.com/amusarra/eventbus-logging-filter-jaxrs-docs/actions/workflows/build_antora_site.yml/badge.svg)](https://github.com/amusarra/eventbus-logging-filter-jaxrs-docs/actions/workflows/build_antora_site.yml)

The **Document as Code (doc-as-code)** approach applies software development principles to the creation, management, and distribution of documentation. This method aims to improve the quality, efficiency, and agility of documentation production by treating documents as part of the project's source code.

This fosters a culture of documentation that is agilely integrated with software development, allowing for a more efficient workflow, higher quality documentation, and a better overall experience for developers and end users.

This repository contains the source code of the [Quarkus Event Bus Logging Filter JAX-RS](https://github.com/amusarra/eventbus-logging-filter-jaxrs) eBook, illustrating how the project was created and published on GitHub.

The project was developed using the Document as Code (doc-as-code) approach, using [AsciiDoc](https://asciidoc.org/), a lightweight markup language for writing human-readable and machine-readable documents.

The toolchain used for generating the eBook is [Asciidoctor](https://asciidoctor.org/), a text processor supporting AsciiDoc syntax that produces HTML5, DocBook, PDF, and other formats. Starting from version 1.2.0 of this docs project, [Antora](https://antora.org/) is also supported for generating a multi-page navigable documentation site.

Supported outputs for this documentation are: **html5**, **pdf** and **Antora site**.

The project uses the [Asciidoctor](https://asciidoctor.org/docs/asciidoctor-maven-plugin/) Maven Plugin, responsible for processing source files in AsciiDoc format and generating the eBook in PDF format.

## Project Structure

```
eventbus-logging-filter-jaxrs-docs/
├── docs/                              # Antora component (single source of truth)
│   ├── antora.yml                     # Antora component descriptor (version: 1.3.0)
│   └── modules/
│       └── ROOT/
│           ├── nav.adoc               # Antora navigation
│           ├── pages/                 # Antora pages (one per chapter)
│           ├── partials/              # AsciiDoc partials (chapter content + attributes)
│           │   ├── _attributes-common.adoc
│           │   ├── _attributes-pdf.adoc
│           │   └── chapters/          # Chapter source files
│           └── images/                # Documentation images
├── src/main/docs/asciidoc/            # Maven Asciidoctor source (PDF/HTML5 generation)
│   ├── index.adoc                     # Master document for PDF/HTML5
│   ├── attributes/                    # PDF/HTML5 attributes
│   ├── chapters/                      # Chapter files (copies - for Maven build)
│   └── resources/                     # Themes and images for Maven build
├── antora-playbook.yml                # Antora Playbook (local development)
├── antora-playbook-prod.yml           # Antora Playbook (production / CI)
└── package.json                       # Node.js dependencies for Antora
```

## Requirements

### For PDF and HTML5 generation (Maven)
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

### For Antora site generation
To generate the Antora site, the following software is required:

- Node.js 18 or higher
- npm (bundled with Node.js)

## Generating the eBook
To generate the eBook in PDF format, run the Maven command:

```shell script
mvn clean asciidoctor:process-asciidoc@asciidoc-to-pdf
```
Console 1 - Execute the Maven command to generate the eBook

The Maven command will compile the project and generate the PDF eBook. The generated PDF file will be available in the project's `target/generated-pdf` folder, named `${project.artifactId}-${project.version}.pdf`.

## Generating HTML Documentation
To generate HTML documentation, run the Maven command:

```shell script
mvn clean asciidoctor:process-asciidoc@asciidoc-to-html
```
Console 2 - Execute the Maven command to generate the HTML docs

The Maven command will compile the project and generate the HTML documentation. The HTML documentation will be available in the project's `target/generated-html5` folder.

## Generating Antora Documentation Site

[Antora](https://antora.org/) is a multi-repository documentation site generator for AsciiDoc. Starting from documentation version **1.2.0** (aligned with project version **1.3.0**), the project supports Antora for generating a multi-page navigable documentation site.

### Install Antora dependencies

```shell script
npm install
```
Console 3 - Install Antora CLI and extensions

### Generate the Antora site locally

```shell script
npm run antora
```
Console 4 - Generate the Antora site (local playbook)

Or directly with the Antora CLI:

```shell script
node_modules/.bin/antora antora-playbook.yml
```
Console 5 - Generate the Antora site with the local playbook

The generated site will be available in the `target/antora-site/` folder. Open `target/antora-site/index.html` in a browser to view it.

### Antora Project Structure

The Antora component is located in the `docs/` directory:

| Path | Description |
|------|-------------|
| `docs/antora.yml` | Component descriptor — defines name, version (`1.3.0`) and navigation |
| `docs/modules/ROOT/pages/` | One AsciiDoc page per chapter/section |
| `docs/modules/ROOT/partials/chapters/` | Chapter source content (included by pages) |
| `docs/modules/ROOT/partials/_attributes-common.adoc` | Common AsciiDoc attributes |
| `docs/modules/ROOT/images/` | Documentation images |
| `antora-playbook.yml` | Local development playbook |
| `antora-playbook-prod.yml` | Production playbook (used by CI/CD) |

### Antora Playbook Configuration

Two playbooks are provided:

- **`antora-playbook.yml`** — For local development. Uses the local filesystem as content source and outputs to `target/antora-site/`.
- **`antora-playbook-prod.yml`** — For CI/CD production builds. Uses the GitHub repository as content source and outputs to `build/site/`.

### Diagram Support

The Antora site uses [Kroki](https://kroki.io/) via the `asciidoctor-kroki` extension to render diagrams (Mermaid, PlantUML, etc.) defined in the AsciiDoc source. Diagrams are rendered server-side by the public Kroki service — no local diagram tool installation is required for Antora builds.

## Publishing HTML Documentation on GitHub Pages
The generated HTML documentation is also available on [GitHub Pages](https://amusarra.github.io/eventbus-logging-filter-jaxrs-docs/). This is made possible by the GitHub Actions [Deploy AsciiDoc to Pages](.github/workflows/build_asciidoc_to_html_github_page.yml), which publishes the generated HTML documentation (via the AsciiDoc Maven plugin) to GitHub Pages.

The Antora site is published via the GitHub Actions [Deploy Antora Site to Pages](.github/workflows/build_antora_site.yml) workflow, triggered on every push to the `main` branch when content under `docs/` changes.
