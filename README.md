# Quarkus Event Bus Logging Filter JAX-RS Documentation

[![Keep a Changelog v1.1.0 badge](https://img.shields.io/badge/changelog-Keep%20a%20Changelog%20v1.1.0-%23E05735)](CHANGELOG.md)
[![License: MIT](https://img.shields.io/badge/license-CC--BY--NC--SA--4.0-lightgrey)](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.it)

[![Build Docs and Deploy to Pages](https://github.com/amusarra/eventbus-logging-filter-jaxrs-docs/actions/workflows/build_docs.yml/badge.svg)](https://github.com/amusarra/eventbus-logging-filter-jaxrs-docs/actions/workflows/build_docs.yml)

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
│           ├── nav.adoc               # Antora navigation (includes Downloads entry)
│           ├── pages/                 # Antora pages (one per chapter + downloads.adoc)
│           ├── partials/              # AsciiDoc partials (chapter content + attributes)
│           │   ├── _attributes-common.adoc
│           │   ├── _attributes-pdf.adoc
│           │   └── chapters/          # Chapter source files
│           └── images/                # Documentation images
├── src/main/docs/asciidoc/            # Maven Asciidoctor source (PDF/HTML5 generation)
│   ├── index.adoc                     # Master document (includes partials from docs/)
│   └── resources/                     # Themes for Maven PDF build
├── supplemental-ui/                   # Custom Antora UI overrides
│   └── partials/
│       └── header-content.hbs         # Navbar with 📥 Download dropdown
├── antora-playbook.yml                # Antora Playbook (local development)
├── antora-playbook-ci.yml             # Antora Playbook (CI — local source)
├── antora-playbook-prod.yml           # Antora Playbook (production — GitHub source)
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

Three playbooks are provided:

- **`antora-playbook.yml`** — For local development. Uses the local filesystem as content source and outputs to `target/antora-site/`.
- **`antora-playbook-ci.yml`** — For CI/CD builds. Uses the locally checked-out source (`url: .`) to ensure the runner processes the latest commit without network latency. Outputs to `build/site/`.
- **`antora-playbook-prod.yml`** — Alternative production playbook. Uses the GitHub repository as remote content source; useful for triggering remote builds.

### Diagram Support

The Antora site uses [Kroki](https://kroki.io/) via the `asciidoctor-kroki` extension to render diagrams (Mermaid, PlantUML, etc.) defined in the AsciiDoc source. Diagrams are rendered server-side by the public Kroki service — no local diagram tool installation is required for Antora builds.

## CI/CD and GitHub Pages

A single unified GitHub Actions workflow ([Build Docs and Deploy to Pages](.github/workflows/build_docs.yml)) handles the complete documentation pipeline on every push to `main`:

1. **Generate PDF** — via Maven (`mvn generate-resources`) → `target/generated-pdf/eventbus-logging-filter-jaxrs-docs-1.0.0.pdf`
2. **Generate HTML5** — via Maven → `target/generated-html5/`
3. **Generate Antora site** — using `antora-playbook-ci.yml` (local source) → `build/site/`
4. **Copy downloads** — PDF and HTML5 ZIP are copied to `build/site/downloads/` so they are served as static files on GitHub Pages
5. **Upload artifacts** — PDF and HTML5 are uploaded as GitHub Actions artifacts (90-day retention) for direct download from the Actions tab
6. **Deploy to GitHub Pages** — the complete `build/site/` (Antora site + downloads) is published at [https://amusarra.github.io/eventbus-logging-filter-jaxrs-docs/](https://amusarra.github.io/eventbus-logging-filter-jaxrs-docs/)

### Download from Antora UI

The Antora site includes a **📥 Download** dropdown in the top navigation bar with direct links to:
- 📄 **PDF** — `https://amusarra.github.io/eventbus-logging-filter-jaxrs-docs/downloads/eventbus-logging-filter-jaxrs-docs.pdf`
- 🗜️ **HTML5 ZIP** — `https://amusarra.github.io/eventbus-logging-filter-jaxrs-docs/downloads/eventbus-logging-filter-jaxrs-docs-html5.zip`
- ℹ️ **Downloads info page** — `eventbus-logging-filter-jaxrs/1.3.0/downloads.html`
