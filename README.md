<div align="center">

<img src="images/saurus_banner.png" alt="SAURUS banner" width="100%">

# 🦖 SAURUS

**Staphylococcus aureus Unified Resource for Universal Surveillance**

*One database. Every typing module. Every genome geolocated. Every interface — web and terminal.*

[![Live Site](https://img.shields.io/badge/🌐_Live_Site-saurus--db.org-d4af37?style=for-the-badge)](https://saurus-db.org/)
[![PyPI](https://img.shields.io/badge/PyPI-saurus--cli-3775A9?style=for-the-badge&logo=pypi&logoColor=white)](https://pypi.org/project/saurus-cli/)
[![Bioconda](https://img.shields.io/badge/Conda-bioconda-44A833?style=for-the-badge&logo=anaconda&logoColor=white)](https://anaconda.org/bioconda/saurus-cli)
[![Docker](https://img.shields.io/badge/Docker-ghcr.io-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://github.com/bbeckley-hub/saurus-cli/pkgs/container/saurus-cli)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](LICENSE)
[![Genomes](https://img.shields.io/badge/Genomes-134K-blue?style=for-the-badge)](https://saurus-db.org/)
[![Modules](https://img.shields.io/badge/Modules-11-purple?style=for-the-badge)](https://saurus-db.org/)
[![Countries](https://img.shields.io/badge/Countries-139-0ea5e9?style=for-the-badge)](https://saurus-db.org/geography.html)
[![Part of ARGUS](https://img.shields.io/badge/Part%20of-ARGUS-0a1628?style=for-the-badge)](https://argus-db.org/)

[**🏠 Home**](https://saurus-db.org/) ·
[**🌍 Geography**](https://saurus-db.org/geography.html) ·
[**🧬 Lineages**](https://saurus-db.org/lineages.html) ·
[**📥 Downloads**](https://saurus-db.org/downloads.html) ·
[**💻 CLI Manual**](https://saurus-db.org/manual.html) ·
[**ℹ️ About**](https://saurus-db.org/about.html)

</div>

---

## 🚨 The Problem — Genomic Data Is Public, but Genomic *Retrieval* Is Still Manual

We now have **134,299 public *Staphylococcus aureus* genomes**. The raw data exists. The annotations exist. The epidemiological metadata exists. And yet the most routine question in genomic epidemiology still requires a script.

Ask for *"all ST5 MRSA bloodstream isolates from the United States between 2015 and 2023 carrying mecA"* and watch what happens:

- You download typing tables from one source.
- You download gene presence/absence from another.
- You download NCBI BioSample metadata from a third.
- You write custom Python to cross-reference accessions.
- You reconcile column names, accession formats, and version suffixes.
- You iterate until the join doesn't silently drop records.
- **Then** you get your accession list.

That is not a data problem. That is an **interface problem** — and it is why the majority of researchers, clinicians, and public health teams who *should* be doing genomic surveillance are locked out of it. The data is free; the workflow is not.

---

## 💡 The Solution — SAURUS, Two Ways

**SAURUS** compiles eleven typing, gene-annotation, and epidemiological modules for the entire public *S. aureus* repository into a **single, queryable interface**. You can query it however you already work:

<table>
<tr>
<td width="50%" valign="top" align="center">

### 🌐 **Web UI**
**https://saurus-db.org**

Point, click, filter, export.
No install. Runs in your browser.

[**→ Open the web app**](https://saurus-db.org/)

</td>
<td width="50%" valign="top" align="center">

### 💻 **SAURUS-CLI**
`pip install saurus-cli`

Terminal-native. Pipeline-ready.
Bundled data, zero downloads.

[**→ Read the CLI manual**](https://saurus-db.org/manual.html)

</td>
</tr>
</table>

Both interfaces expose the same 11 modules, the same 134,299 genomes, the same epidemiological metadata — and both produce the same artifact: **a clean accession list** ready to feed directly to `datasets download genome accession`.

| Category | Modules |
|---|---|
| **Typing** | MLST · spa · SCCmec (CGE + RPet) · agr · capsule |
| **Genes** | AMR · Virulence (VFDB) · Plasmid replicons |
| **Clinical** | MRSA/MSSA consensus |
| **Epidemiology** | Country · isolation source · host · collection year |
| **Lineage context** | Curated catalogue of ~50 clonal complexes |
| **Retrieval** | Search → filter → export accession lists |

> **The core deliverable is accession retrieval** — regardless of interface.

---

### 🌐 The Two-Minute Web Workflow

1. Open [**saurus-db.org/pages/mrsa.html**](https://saurus-db.org/pages/mrsa.html)
2. Filter: `MRSA Status = MRSA` · `MLST = ST5` · `Country = United States` · `Source = blood`
3. Click **🧬 Accessions** → save the `.txt` file
4. Run:
   ```bash
   datasets download genome accession --inputfile accessions.txt
   ```
5. ✅ You have the exact genomes you want — filtered by **genotype, phenotype, and geography**.

---

### 💻 The Two-Minute CLI Workflow

```bash
# Install once
pip install saurus-cli

# Query with a single lineage signature
saurus --lineage USA100 --country USA --source blood --count
# → 297

# Export metadata table + accession list in one command
saurus --lineage USA100 --country USA --source blood \
    --format tsv,accession -o usa100_blood

# Pipe straight into NCBI — no intermediate files
saurus --lineage USA100 --country USA --source blood | \
    datasets download genome accession \
    --inputfile /dev/stdin --filename usa100_blood.zip
```

✅ **Same result, in the terminal, with reproducible config files.**

That is the difference between a *database* and a *tool*. SAURUS is both.

---

## 💻 SAURUS-CLI — Bioinformatician-First Retrieval

**SAURUS-CLI** is a companion command-line interface that ships the **entire SAURUS dataset bundled inside the installable artifact**. After installation, queries run locally — no downloads, no API keys, no network access.

### 📦 Three install paths, one artifact

| Ecosystem | Command | Data lands at |
|---|---|---|
| **pip** | `pip install saurus-cli` | `<venv>/share/saurus/data/` |
| **conda** | `conda install -c bioconda saurus-cli` | `${CONDA_PREFIX}/share/saurus/data/` |
| **Docker** | `docker run --rm ghcr.io/bbeckley-hub/saurus-cli --version` | `/usr/local/share/saurus/data/` |

### ⚡ Why it matters

- **Zero network calls.** The full 134,299-genome dataset (~18 MB gzipped) is baked into the wheel, conda package, and Docker image.
- **Lineage signatures.** Query `--lineage USA300` instead of typing 5 flags. Override any component: `--lineage USA300 --country Japan`.
- **Multi-format in one run.** `--format tsv,json,accession -o results` writes three files from one query.
- **Reproducible queries.** Save your query as JSON: `saurus --config my_query.json` — byte-for-byte reproducible across institutions.
- **Debug mode.** `--debug` prints a row-count trace after every filter, so you can see exactly where a query collapsed to 0.
- **Pipeline-native.** Pipes cleanly into `datasets`, Snakemake, Nextflow, and shell scripts.

### 📚 Documentation

- **Full CLI manual:** [saurus-db.org/manual.html](https://saurus-db.org/manual.html)
- **Example gallery:** `saurus --examples` (in your terminal)
- **Author + citation:** `saurus --about`
- **Source code:** [github.com/bbeckley-hub/saurus-cli](https://github.com/bbeckley-hub/saurus-cli)

### 🏷️ Lineage Signatures at a Glance

```bash
saurus --lineage USA100     # ST5, t002, SCCmec II, agr II, capsule 5
saurus --lineage USA300     # ST8, t008, SCCmec IV, agr I, capsule 5
saurus --lineage EMRSA-15   # ST22, t032, SCCmec IV, agr I, capsule 5
saurus --lineage EMRSA-16   # ST36, t018, SCCmec II, agr III, capsule 8
saurus --lineage "Bengal Bay"  # ST772, t657, SCCmec V, agr II, capsule 5
saurus --lineage ST152      # ST152, SCCmec V, agr III, capsule 5
```

One flag. Six components. Zero typos.

---

## 🌍 The Scale — Why This Matters

| Metric | Value |
|---|---|
| **Unique genomes indexed** | **134,299** |
| **De novo typed genomes** | **98,138** |
| **MRSA rate across typed collection** | **59.2%** |
| **Countries represented** | **139** |
| **Unique sequence types** | **2,116** |
| **Unique spa types** | **3,932** |
| **Curated clonal complexes** | **~50** |

These are not toy numbers. This is the largest unified *S. aureus* genomic typing resource built by a single team — and every genome, every annotation, and every metadata field is available **for free**, without login, and will remain available as long as the internet hosts static HTML and the PyPI registry.

---

## 👁️ Part of the ARGUS Family

SAURUS is the **flagship build** of **ARGUS** — *Antimicrobial Resistance Genomic Unified Surveillance* — a family of independent, open genomic surveillance sites, each dedicated to one of the WHO priority ESKAPE pathogens.

Named for **Argus Panoptes** — the hundred-eyed giant of Greek myth who never slept — the umbrella is a bet that AMR surveillance has to be *unified* to be useful, and that the pathogens driving the crisis deserve the same treatment.

**🏛️ ARGUS umbrella:** [**argus-db.org**](https://argus-db.org/)

| Resource | Pathogen | Live URL | Status |
|---|---|---|---|
| 🦖 **SAURUS** | *Staphylococcus aureus* | [**saurus-db.org**](https://saurus-db.org/) | ✅ **live** |
| 🌑 **ECLIPSE** | *Escherichia coli* | [bbeckley-hub.github.io/eclipse](https://bbeckley-hub.github.io/eclipse) | 🚧 in progress |
| 🌊 **ABYSS** | *Acinetobacter baumannii* | — | 📋 planned |
| 🏆 **KLEOS** | *Klebsiella pneumoniae* | — | 📋 planned |
| 💧 **PSEUDA** | *Pseudomonas aeruginosa* | — | 📋 planned |
| 👑 **EMPIRE** | *Enterococcus faecium* | — | 📋 planned |
| 🌀 **ENTROPY** | *Enterobacter* spp. | — | 📋 planned |

Every sibling is built on the same architecture — a static site, accession-first design, with a shared generator template. Once one resource works, the next ships in weeks rather than months, and every resource benefits from improvements made in any other.

---

## 🎯 Project Goal — Annotate All Public *S. aureus* Genomes

SAURUS is being built incrementally toward a single milestone: **the complete annotation of every public *S. aureus* genome** in the NCBI Assembly database.

| Milestone | Scope | Status |
|---|---|---|
| **v0.1** | 20K RefSeq (GCF) genomes, 9 modules | ✅ **live** |
| **v0.2** | + Country · Source · Host · Year metadata · **Geography page** | ✅ **live** |
| **v0.3** | Full 26,197 GCF genomes · 913 STs · 13 CCs | ✅ **merged into v0.2** |
| **v0.4** | + 33,985 unique GCA genomes | 🔜 **next** |
| **v0.5** | + 73,472 Shelenkov-only GCA genomes | 📋 planned |
| **v1.0** | **134,299 genomes · unified master table · citable resource** | 🎯 target |

---

## ✨ Features

<table>
<tr>
<td width="50%" valign="top">

### 🔬 Interactive typing pages

- **Live search** with exact-match operators (`ST5`, `CC5`, `t002`)
- **Multi-column filters** — combine ST + SCCmec + agr + capsule + MRSA + **Country + Source**
- **Column visibility toggle** — persisted per browser
- **Row selection** with select-all-visible
- **Sortable columns** — numeric-aware
- **Pagination** — 20 / 50 / 100 rows per page
- **Export** — TSV · CSV · JSON · **accession-only**

</td>
<td width="50%" valign="top">

### 💻 SAURUS-CLI

- **`pip install saurus-cli`** — full dataset bundled
- **Lineage signatures** — `--lineage USA300` instead of 5 flags
- **Multi-format output** — `--format tsv,json,accession` in one run
- **Reproducible configs** — `saurus --config query.json`
- **Debug mode** — `--debug` traces row counts per filter
- **Pipeline-native** — pipes into `datasets`, Snakemake, Nextflow

</td>
</tr>
<tr>
<td valign="top">

### 🌍 Geography &amp; Metadata

- **139 countries** · **~30 source categories**
- **4 interactive charts** — countries, sources, timeline, hosts
- **5 filters** — country · source · host · year · assembly level
- **Full provenance** — raw submitter strings preserved
- Combined queries: *`ST5` + `MRSA` + `United States` + `blood`*

</td>
<td valign="top">

### 🧬 Gene retrieval pages

- **Up to 5 genes per query**
- **ANY / ALL** match logic
- **Curated headline genes** for AMR, virulence, plasmid
- One-click **accession list export**
- **Click-to-copy** accession per row
- **Frequency table** — sortable, filterable

</td>
</tr>
<tr>
<td valign="top">

### 📚 Lineage catalogue

- ~50 curated clonal complexes
- **Live sample counts** from the current dataset
- **Reference-only cards** for lineages with no samples yet
- **Export all accessions** per lineage
- Geographic + clinical + virulence context per CC

</td>
<td valign="top">

### 📊 Statistics page

- Top 20 STs with **MRSA % overlay**
- CC distribution · spa distribution
- **SCCmec RPet vs CGE** side by side
- **4-level alluvial:** SCCmec → agr → Capsule → MRSA
- CC × SCCmec heatmap
- Capsule by CC stacked bars

</td>
</tr>
<tr>
<td valign="top">

### 📥 Bulk downloads

- Every merged TSV as `.tsv.gz`
- Row counts + file sizes at a glance
- **`metadata.tsv.gz`** — full BioSample table
- **Long-format gene tables** — pivot-ready
- One-file-per-module layout

</td>
<td valign="top">

### 📚 Documentation

- **Web manual** — [saurus-db.org/manual.html](https://saurus-db.org/manual.html)
- **CLI examples** — `saurus --examples`
- **Author + citation** — `saurus --about`
- **About page** — [saurus-db.org/about.html](https://saurus-db.org/about.html)

</td>
</tr>
</table>

---

## 🚀 Quick Start

### 🌐 Web (nothing to install)

**👉 [https://saurus-db.org/](https://saurus-db.org/)**

### 💻 CLI (installs in 5 seconds)

```bash
pip install saurus-cli
saurus --examples        # see the full gallery
saurus --lineage USA300 --count
# → 8,657
```

### 🐳 Docker (zero install, data baked in)

```bash
docker run --rm ghcr.io/bbeckley-hub/saurus-cli:latest \
    --lineage USA300 --country USA --source blood --count
```

---

### Example workflow — get all ST5 MRSA blood isolates from the United States

**Via web:**

1. Open [**saurus-db.org/pages/mrsa.html**](https://saurus-db.org/pages/mrsa.html) → filter:
   - `MRSA Status = MRSA`
   - `MLST = ST5`
   - `Country = United States`
   - `Source = blood`
2. Click **🧬 Accessions** → save the `.txt` file
3. Feed it to NCBI: `datasets download genome accession --inputfile accessions.txt`

**Via CLI (single command):**

```bash
saurus --st 5 --mrsa --country USA --source blood | \
    datasets download genome accession --inputfile /dev/stdin --filename st5_blood.zip
```

Both produce the same result. Pick the interface that fits your workflow.

---

## 🗺️ Roadmap

<details>
<summary><b>v0.1 — Foundation</b> ✅ live</summary>

- [x] 9 typing + gene modules live
- [x] Consistent nav across all pages
- [x] CC column added to MLST and MRSA pages
- [x] Lineage catalogue with live sample counts
- [x] Bulk download index
- [x] GitHub Pages deployment

**Dataset:** 20,000 RefSeq genomes

</details>

<details>
<summary><b>v0.2 — Epidemiological metadata + CLI</b> ✅ live</summary>

- [x] Country + isolation source + host + collection year from NCBI BioSample
- [x] Free-text sources normalized into ~30 categories
- [x] **Country** and **Source** filters on every typing page
- [x] **Country × MRSA** and **Source × MRSA** cross-tabs
- [x] New **Geography** page — 4 charts, 5 filters, full metadata browser
- [x] `metadata.tsv.gz` added to downloads
- [x] **SAURUS-CLI** released on PyPI, Bioconda, and GHCR
- [x] **Custom domains live** — `saurus-db.org` + `argus-db.org`
- [x] **CLI manual** at [saurus-db.org/manual.html](https://saurus-db.org/manual.html)

</details>

<details>
<summary><b>v0.3 — Complete RefSeq coverage</b> ✅ merged into v0.2</summary>

- [x] Full 26,197 GCF genomes merged
- [x] 913 unique STs · 13 clonal complexes · 1,966 spa types · 57 SCCmec types
- [x] 63.5% MRSA rate across the full collection

</details>

<details open>
<summary><b>v0.4 — GenBank merge</b> 🔜 next</summary>

- [ ] Process 33,985 unique GCA genomes through StaphScope
- [ ] Per-batch provenance — users see which genomes came from which release
- [ ] Merge with existing GCF collection into a unified master table
- [ ] Handle GCA ↔ GCF paired accessions
- [ ] Refresh SAURUS-CLI bundled data to include new genomes

</details>

<details>
<summary><b>v0.5 — Shelenkov-only GenBank</b> 📋 planned</summary>

- [ ] + 73,472 GCA genomes where SCCmec / agr / capsule are re-typed by StaphScope
- [ ] AMR / virulence / plasmid annotations carried forward from Shelenkov et al. (2025)
- [ ] Deduplication pass

</details>

<details>
<summary><b>v1.0 — Full resource</b> 🎯 target</summary>

- [ ] **134,299 genomes** with unified master table
- [ ] Cross-module filter UI — CC + SCCmec + agr + capsule + country + source + any gene
- [ ] Boolean query builder for advanced users
- [ ] **Zenodo DOI** for citable release
- [ ] Database article submitted (*Database* — Oxford)

</details>

---

## 🧬 Data Sources

| Layer | Source | Coverage |
|---|---|---|
| **Typing** | [StaphScope v2.0.0](https://github.com/bbeckley-hub/staphscope-typing-tool) on RefSeq genomes | 26,197 GCF → 134K |
| **Country / source / host / year** | [NCBI BioSample](https://www.ncbi.nlm.nih.gov/biosample/) via `datasets summary genome` | 92% country · 74% source |
| **AMR genes** | [Shelenkov et al. 2025](https://doi.org/10.1186/s12863-025-01363-w) | 86,318 GCA |
| **Virulence (VFDB)** | Shelenkov et al. 2025 | 98,950 GCA |
| **Plasmid replicons** | Shelenkov et al. 2025 | 86,318 GCA |
| **Lineage reference** | Curated (literature-validated) | ~50 CCs |

All genome identifiers use the standard `GCA_XXXXXXXXX.Y` or `GCF_XXXXXXXXX.Y` format.

---

## 📁 Repository Structure

```
saurus/
├── README.md
├── LICENSE
├── images/
│   └── saurus_banner.png
└── docs/                          ← GitHub Pages site (source: main /docs)
    ├── CNAME                      ← "saurus-db.org"
    ├── .nojekyll
    ├── index.html                 ← landing page
    ├── about.html                 ← project + team + methods
    ├── manual.html                ← SAURUS-CLI user manual
    ├── statistics.html            ← 9+ charts (ST+MRSA, CC×SCCmec, alluvial)
    ├── geography.html             ← metadata browser + 4 charts
    ├── lineages.html              ← curated CC catalogue
    ├── downloads.html             ← bulk data index
    ├── assets/
    │   └── chart.min.js           ← Chart.js (bundled locally)
    ├── data/                      ← bulk .tsv.gz downloads
    │   ├── *.tsv.gz               ← typing + gene tables
    │   ├── metadata.tsv.gz        ← BioSample metadata
    │   └── saurus_data_all.zip    ← everything, one archive
    └── pages/
        ├── mlst.html              ← MLST + CC
        ├── spa.html
        ├── sccmec.html            ← CGE + RPet + subtype tabs
        ├── capsule.html
        ├── agr.html
        ├── mrsa.html              ← MRSA + CC breakdown + country/source cross-tabs
        ├── amr.html               ← gene retrieval
        ├── vfdb.html
        ├── plasmid.html
        └── data/                  ← gene retrieval JSON indexes
```

> `merged/`, `batches/`, and `scripts/` are git-ignored — they hold the local pipeline.

---

## 🛠️ Running Locally

**Prerequisites:** Python 3.9+

```bash
git clone https://github.com/bbeckley-hub/saurus.git
cd saurus/docs
python3 -m http.server 8000
```

Open **http://localhost:8000/**.

> ⚠️ **HTTP required.** The gene retrieval pages use `fetch()` to load JSON. Browsers block this from `file://` URLs. Served over HTTP (or from GitHub Pages), it just works.

---

## 🧪 Regenerating Pages

Each page is produced by a self-contained Python script in `merged/`. The recommended way is:

```bash
cd merged/
bash ~/saurus/scripts/Regenerate_all.sh
```

This runs every generator, gzips `metadata.tsv`, refreshes the bulk zip, and finishes with `fix_nav.py` to guarantee the 15-link nav across all pages.

### Manual regeneration (per-module)

```bash
cd merged/

# Typing pages
python3 generate_mlst.py      -i mlst_all.tsv              -o ../docs/pages/mlst.html
python3 generate_spa.py       -i spa_all.tsv               -o ../docs/pages/spa.html
python3 generate_agr.py       -i agr_all.tsv               -o ../docs/pages/agr.html
python3 generate_capsule.py   -i capsule_all.tsv           -o ../docs/pages/capsule.html
python3 generate_sccmec.py    -c sccmec_cge_all.tsv \
                              -r sccmec_rpet_all.tsv       -o ../docs/pages/sccmec.html
python3 generate_mrsa.py      --mlst mlst_all.tsv --spa spa_all.tsv \
                              --cge sccmec_cge_all.tsv --rpet sccmec_rpet_all.tsv \
                              --capsule capsule_all.tsv --agr agr_all.tsv \
                              --cc cc.txt                  -o ../docs/pages/mrsa.html

# Gene retrieval pages
python3 generate_gene_page.py --db all --dir . \
    --outdir ../docs/pages/ --datadir ../docs/pages/data

# Supporting pages
python3 generate_statistics.py  --dir . -o ../docs/statistics.html
python3 generate_geography.py           -o ../docs/geography.html
python3 generate_index.py       --dir . -o ../docs/index.html
python3 generate_about.py               -o ../docs/about.html
python3 generate_manual.py              -o ../docs/manual.html
python3 generate_lineages.py            -o ../docs/lineages.html
python3 generate_downloads.py   --dir . -o ../docs/downloads.html

# Nav consistency (must be last)
python3 fix_nav.py ../docs
```

---

## 🤝 Contributing

We welcome:

- 🐛 **Bug reports** — [open an issue](https://github.com/bbeckley-hub/saurus/issues)
- 💡 **Feature suggestions** — [start a discussion](https://github.com/bbeckley-hub/saurus/discussions)
- 🧬 **Data corrections** — if you spot a lineage call that doesn't match the literature
- 📊 **New metadata sources** — geographic crosswalks, country name normalizations

Please keep pages **self-contained** (one script per page) and preserve the shared visual style.

For SAURUS-CLI contributions, see [github.com/bbeckley-hub/saurus-cli](https://github.com/bbeckley-hub/saurus-cli).

---

## 📚 Citation

If you use SAURUS in your research, please cite the web resource, the CLI, the pipeline, and the source gene dataset.

### SAURUS web resource

> **Beckley B, Olalekan A, Afeke I, Amarh V.** SAURUS: an interactive web resource for typing-based genome retrieval in *Staphylococcus aureus*. *BMC Genom Data* [under review]. 2026.

### SAURUS-CLI

> **Beckley B** SAURUS-CLI: a reproducible command-line interface for typing-based genome retrieval in *Staphylococcus aureus*. *BMC Bioinformatics* [under review]. 2026.
> [github.com/bbeckley-hub/saurus-cli](https://github.com/bbeckley-hub/saurus-cli)

### Typing pipeline

> **Beckley B, Amarh V.** StaphScope: a species-optimized computational pipeline for rapid and accessible *Staphylococcus aureus* genotyping and surveillance. *BMC Genomics*. 2026;27:261.
> [doi:10.1186/s12864-026-12609-x](https://doi.org/10.1186/s12864-026-12609-x)

### Gene dataset

> **Shelenkov A, Slavakhotova A, Yunusova M, et al.** Genomic typing, antimicrobial resistance gene, virulence factor and plasmid replicon database for the important pathogenic bacteria *Staphylococcus aureus*. *BMC Genom Data*. 2025;26:65.
> [doi:10.1186/s12863-025-01363-w](https://doi.org/10.1186/s12863-025-01363-w)

### Metadata source

> **NCBI BioSample** — country, isolation source, host, and collection date attributes attached to each RefSeq assembly.

---

## 🙏 Acknowledgements

SAURUS stands on the shoulders of the open-source genomics community. We thank:

- **Brown Beckley & Vincent Amarh** — for StaphScope, the typing engine
- **Andrey Shelenkov & colleagues** — for publishing their gene dataset openly
- **NCBI** — for the `datasets` CLI, AMRFinderPlus, and the Assembly + BioSample databases
- **Torsten Seemann** — for `mlst`, `ABRicate`, and a decade of pipeline standards
- **Robert A. Petit III** — for `sccmec` and `agrVATE` contributions
- **Center for Genomic Epidemiology (DTU)** — for `SCCmecFinder`
- **PubMLST & Ridom** — for allele and spa-type reference databases
- **The Python scientific stack** — pandas, numpy, and every dependency in between

---

## 📄 License

**MIT License** — free to use, modify, and redistribute. Attribution appreciated.

See [LICENSE](LICENSE) for details.

---

<div align="center">

**Built with 🧬 at the University of Ghana Medical School**

*Turning fragmented genomic data into coherent biological narratives.*

[**🌐 saurus-db.org**](https://saurus-db.org/) ·
[**👁️ argus-db.org**](https://argus-db.org/) ·
[**💻 saurus-cli on PyPI**](https://pypi.org/project/saurus-cli/)

**[⭐ Star this repo](https://github.com/bbeckley-hub/saurus)** if you find it useful.

</div>
