<div align="center">

<img src="images/saurus_banner.png" alt="SAURUS banner" width="100%">

# 🦖 SAURUS

**Staphylococcus aureus Unified Resource for Universal Surveillance**

*One database. Every typing module. Every genome geolocated. Every interface — web and terminal.*

[![Live Site](https://img.shields.io/badge/🌐_Live_Site-saurus--db.org-d4af37?style=for-the-badge)](https://saurus-db.org/)
[![Release](https://img.shields.io/badge/Release-v0.8-2ea043?style=for-the-badge)](https://github.com/bbeckley-hub/saurus/releases)
[![PyPI](https://img.shields.io/badge/PyPI-saurus--cli-3775A9?style=for-the-badge&logo=pypi&logoColor=white)](https://pypi.org/project/saurus-cli/)
[![Bioconda](https://img.shields.io/badge/Conda-bioconda-44A833?style=for-the-badge&logo=anaconda&logoColor=white)](https://anaconda.org/bioconda/saurus-cli)
[![Docker](https://img.shields.io/badge/Docker-ghcr.io-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://github.com/bbeckley-hub/saurus-cli/pkgs/container/saurus-cli)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](LICENSE)
[![Genomes](https://img.shields.io/badge/Genomes-134K-blue?style=for-the-badge)](https://saurus-db.org/)
[![Modules](https://img.shields.io/badge/Modules-11-purple?style=for-the-badge)](https://saurus-db.org/)
[![Countries](https://img.shields.io/badge/Countries-~150-0ea5e9?style=for-the-badge)](https://saurus-db.org/geography.html)
[![Part of ARGUS](https://img.shields.io/badge/Part%20of-ARGUS-0a1628?style=for-the-badge)](https://argus-db.org/)
[![DOI](https://zenodo.org/badge/1055583691.svg)](https://doi.org/10.5281/zenodo.23264894)

[**🏠 Home**](https://saurus-db.org/) ·
[**🌍 Geography**](https://saurus-db.org/geography.html) ·
[**🧬 Lineages**](https://saurus-db.org/lineages.html) ·
[**📥 Downloads**](https://saurus-db.org/downloads.html) ·
[**💻 CLI Manual**](https://saurus-db.org/manual.html) ·
[**ℹ️ About**](https://saurus-db.org/about.html)

</div>

---

## 🚨 The Problem — Genomic Data Is Public, but Genomic *Retrieval* Is Still Manual

We now have **134,160 fully typed public *Staphylococcus aureus* genomes**. The raw data exists. The annotations exist. The epidemiological metadata exists. And yet the most routine question in genomic epidemiology still requires a script.

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

Both interfaces expose the same 11 modules, the same 134,160 genomes, the same epidemiological metadata — and both produce the same artifact: **a clean accession list** ready to feed directly to `datasets download genome accession`.

| Category | Modules |
|---|---|
| **Typing** | MLST · spa · SCCmec (CGE + RPet) · agr · capsule |
| **Genes** | AMR · Virulence (VFDB) · Plasmid replicons |
| **Clinical** | MRSA/MSSA consensus |
| **Epidemiology** | Country · isolation source · host · collection year · BioProject · BioSample |
| **Lineage context** | Curated catalogue of 74 clonal complexes |
| **Retrieval** | Search → filter → export accession lists |

> **The core deliverable is accession retrieval** — regardless of interface.

---

## 🆕 What's New in v0.8

**Release date:** 2026-11-02 · **Live site:** [saurus-db.org](https://saurus-db.org/)

### Full typing complete — 134,160 genomes across all 6 modules

The final 17K-batch spa merge is done. Every typing table now reports exactly **134,160 unique accessions**:

| Module | Rows |
|---|---|
| `mlst_all.tsv` | 134,160 |
| `spa_all.tsv` | 134,160 |
| `agr_all.tsv` | 134,160 |
| `capsule_all.tsv` | 134,160 |
| `sccmec_cge_all.tsv` | 134,160 |
| `sccmec_rpet_all.tsv` | 134,160 |

Zero exact-string duplicates. Zero base-ID duplicates. Zero cross-prefix duplicates. Uniform across all modules.

### BioProject + BioSample columns on every typing page

Both fields are now available as **toggleable columns** in the ⚙ Columns panel of every typing page. Hidden by default to preserve the compact view; one click shows `PRJNA…` and `SAMN…` identifiers inline.

### Sortable filter dropdowns across all pages

- **Collection Year** — newest first (`2026 → 1927`)
- **Country / Region** — alphabetical (`Afghanistan → Zimbabwe`)
- **Source / Host / SCCmec type** — by frequency (most common first)
- **MLST / CC** — numeric (`ST1 < ST2 < ST10 < ST398`)
- **agr** — canonical Roman order (`I → IV`)
- **Capsule** — semantic (`Type 5 → Type 8`)

Fixed a long-standing bug where `2020.0` and `2020` appeared as duplicate years, truncating the top of the list and hiding recent years from search.

### New "Methods" section on the About page

Six subsections documenting: data sources, typing pipeline, deduplication strategy, reproducibility (with a tool-version table), data access, and correction reporting. Every number on the site can now be traced to a documented decision.

### SAURUS-CLI now on the homepage

Prominent green terminal-themed hero section, install pills for pip / conda / docker, live example of `--lineage USA300` query, and links to the GitHub CLI repo.

### Compare page count fix

`compare_data.json` previously reported 139,257 genomes due to a union bug that included filtered-out accessions. Fixed to build from the canonical `mlst_all.tsv` base set — now reports exactly **134,160** everywhere.

### Deduplication — complete

Three classes of duplicates resolved, all documented in `merged/gca_drop.txt` and applied deterministically:

| Class | Count | Rule applied |
|---|---|---|
| Cross-prefix (GCF vs GCA, same BioSample) | 115 pairs | GCF kept, GCA dropped |
| Version drift (same numeric ID, different `.N`) | 12 pairs | Highest version kept |
| Cross-batch duplicates | 9,996 rows | First-seen kept |

---

## 🌍 The Scale — Why This Matters

| Metric | Value |
|---|---|
| **Unique genomes typed** | **134,160** |
| **De novo typed genomes** | **134,160** (100%) |
| **MRSA / MSSA / total typed** | 80,224 / 53,936 / 134,160 |
| **MRSA rate across typed collection** | **59.8%** |
| **Metadata rows (BioSample)** | 134,184 |
| **Genomes in both typing + metadata** | 134,136 |
| **Countries represented** | ~150 |
| **Source categories** | ~300 |
| **Unique MLST sequence types** | **2,738** |
| **Unique clonal complexes** | **74** |
| **Unique spa types** | **4,873** |
| **Unique SCCmec types (RPet)** | 80,224 typed · 63,362 with subtype |
| **CGE ↔ RPet agreement rate** | **94.1%** |

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

Every sibling is built on the same architecture — a static site, accession-first design, with a shared generator template.

---

## 🎯 Project Goal — Annotate All Public *S. aureus* Genomes

SAURUS is being built incrementally toward a single milestone: **the complete annotation of every public *S. aureus* genome** in the NCBI Assembly database.

| Milestone | Scope | Status |
|---|---|---|
| **v0.1** | 20K RefSeq (GCF) genomes, 9 modules | ✅ **done** |
| **v0.2** | + Country · Source · Host · Year metadata · Geography page · SAURUS-CLI | ✅ **done** |
| **v0.3** | Full 26,197 GCF genomes typed | ✅ **done** |
| **v0.4** | + 33,985 unique GCA genomes | ✅ **done** |
| **v0.5** | + 73,472 Shelenkov-only GCA genomes | ✅ **done** |
| **v0.6** | Deduplication pass (9,996 + 115 + 12 dupes removed) | ✅ **done** |
| **v0.7** | Serverless architecture, dual SCCmec callers, full metadata | ✅ **done** |
| **v0.8** | **All 134,160 genomes fully typed · BioProject/BioSample columns · sorted filters · Methods section** | ✅ **CURRENT** |
| **v0.9** | Reconcile 89 typing-only / 24 metadata-only · cross-module filter UI | 📋 next |
| **v1.0** | **Zenodo DOI · Database manuscript · frozen versioned release** | 🎯 target |

---

## ✨ Features

<table>
<tr>
<td width="50%" valign="top">

### 🔬 Interactive typing pages

- **Live search** with exact-match operators (`ST5`, `CC5`, `t002`)
- **Multi-column filters** — combine ST + SCCmec + agr + capsule + MRSA + Country + Source + BioProject + BioSample
- **Column visibility toggle** — persisted per browser
- **Sorted dropdowns** — country A→Z, year newest first, STs numeric, agr Roman
- **Row selection** with select-all-visible
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

- **~150 countries** · **~300 source categories**
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

- **74 clonal complexes** with curated metadata
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
- **Methods section** — [saurus-db.org/about.html#methods](https://saurus-db.org/about.html)
- **CLI examples** — `saurus --examples`
- **Author + citation** — `saurus --about`

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
<summary><b>v0.1 — Foundation</b> ✅ done</summary>

- [x] 9 typing + gene modules live
- [x] Consistent nav across all pages
- [x] CC column added to MLST and MRSA pages
- [x] Lineage catalogue with live sample counts
- [x] Bulk download index
- [x] GitHub Pages deployment

**Dataset:** 20,000 RefSeq genomes

</details>

<details>
<summary><b>v0.2 — Epidemiological metadata + CLI</b> ✅ done</summary>

- [x] Country + isolation source + host + collection year from NCBI BioSample
- [x] Free-text sources normalized into ~300 categories
- [x] **Country** and **Source** filters on every typing page
- [x] **Country × MRSA** and **Source × MRSA** cross-tabs
- [x] New **Geography** page — 4 charts, 5 filters
- [x] `metadata.tsv.gz` added to downloads
- [x] **SAURUS-CLI** released on PyPI, Bioconda, and GHCR
- [x] **Custom domains live** — `saurus-db.org` + `argus-db.org`
- [x] **CLI manual** at [saurus-db.org/manual.html](https://saurus-db.org/manual.html)

</details>

<details>
<summary><b>v0.3–0.5 — Scaling to 134K genomes</b> ✅ done</summary>

- [x] Full 26,197 GCF genomes merged
- [x] + 33,985 unique GCA genomes
- [x] + 73,472 Shelenkov-only GCA genomes
- [x] All 6 typing modules report 134,160 unique accessions

</details>

<details>
<summary><b>v0.6 — Deduplication pass</b> ✅ done</summary>

- [x] 115 GCF/GCA cross-prefix pairs resolved (GCF kept)
- [x] 12 version-drift pairs resolved (highest version kept)
- [x] 9,996 cross-batch duplicates removed
- [x] Deterministic `gca_drop.txt` applied by every generator

</details>

<details>
<summary><b>v0.7 — Serverless architecture</b> ✅ done</summary>

- [x] Dual SCCmec callers (CGE + RPet) with agreement chart
- [x] Full BioSample metadata on every page
- [x] Complete 6-module typing at 134,160 genomes
- [x] `fix_nav.py` post-processor guarantees canonical 17-link nav
- [x] spa 17K-batch crash resolved via single-threaded re-run

</details>

<details open>
<summary><b>v0.8 — Full typing complete + metadata-enriched</b> ✅ CURRENT</summary>

- [x] All 134,160 genomes fully typed (MLST, spa, agr, capsule, SCCmec CGE, SCCmec RPet)
- [x] **BioProject + BioSample columns** on every typing page (toggleable)
- [x] **Sorted dropdowns** — country A→Z, year newest first, STs numeric, agr Roman
- [x] **Methods section** on About page — 6 subsections documenting full reproducibility
- [x] **SAURUS-CLI section** on homepage
- [x] **Compare page count fix** — 134,160 everywhere
- [x] BioProject / BioSample in metadata column selectors

**Version stamp:** `v0.8 · 134,160 GENOMES · 2026-11-02`

</details>

<details>
<summary><b>v0.9 — Reconciliation & advanced filtering</b> 📋 next</summary>

- [ ] Reconcile 89 typing-only / 24 metadata-only genomes
- [ ] Cross-module filter UI (all 11 modules in one query builder)
- [ ] Boolean query expressions (`(ST5 OR ST8) AND SCCmec IV`)
- [ ] Extended lineage catalogue
- [ ] Additional curated clonal complexes

</details>

<details>
<summary><b>v1.0 — Full resource</b> 🎯 target</summary>

- [ ] **Zenodo DOI** for citable data release
- [ ] **Database (Oxford) manuscript** submission
- [ ] Frozen, versioned data snapshot (H2 2026)
- [ ] Complete reproducibility package for external audit

</details>

---

## 🧬 Data Sources

| Layer | Source | Coverage |
|---|---|---|
| **Typing** | [StaphScope v2.1.0](https://github.com/bbeckley-hub/staphscope-typing-tool) on all RefSeq + GenBank genomes | 134,160 genomes (100% typed) |
| **Country / source / host / year** | [NCBI BioSample](https://www.ncbi.nlm.nih.gov/biosample/) via `datasets summary genome` | ~85% country · ~65% source |
| **BioProject / BioSample** | NCBI Assembly database | 100% (BioProject), 100% (BioSample) |
| **AMR genes** | [Shelenkov et al. 2025](https://doi.org/10.1186/s12863-025-01363-w) | Carried forward |
| **Virulence (VFDB)** | Shelenkov et al. 2025 | Carried forward |
| **Plasmid replicons** | Shelenkov et al. 2025 | Carried forward |
| **Lineage reference** | Curated (literature-validated) | 74 CCs |

All genome identifiers use the standard `GCA_XXXXXXXXX.Y` or `GCF_XXXXXXXXX.Y` format.

### Deduplication

Three classes of duplicates resolved (documented in `merged/gca_drop.txt`):

- **Cross-prefix (GCF vs GCA):** 115 pairs, GCF kept
- **Version drift:** 12 pairs, highest version kept
- **Cross-batch:** 9,996 rows, first-seen kept

---

## 📁 Repository Structure

```
saurus/
├── README.md
├── LICENSE
├── CHANGELOG.md
├── images/
│   └── saurus_banner.png
└── docs/                          ← GitHub Pages site (source: main /docs)
    ├── CNAME                      ← "saurus-db.org"
    ├── .nojekyll
    ├── index.html                 ← landing page (with SAURUS-CLI section)
    ├── about.html                 ← project + team + Methods section
    ├── manual.html                ← SAURUS-CLI user manual
    ├── statistics.html            ← 9+ charts (ST+MRSA, CC×SCCmec, alluvial)
    ├── geography.html             ← metadata browser + 4 charts
    ├── lineages.html              ← curated CC catalogue
    ├── downloads.html             ← bulk data index
    ├── assets/
    │   └── chart.min.js           ← Chart.js (bundled locally)
    ├── data/                      ← bulk .tsv.gz downloads + JSON indexes
    │   ├── *.tsv.gz               ← typing + gene tables
    │   ├── metadata.tsv.gz        ← BioSample metadata
    │   └── saurus_data_all.zip    ← everything, one archive
    └── pages/
        ├── mlst.html              ← MLST + CC + metadata columns
        ├── spa.html
        ├── sccmec.html            ← CGE + RPet + subtype tabs
        ├── capsule.html
        ├── agr.html
        ├── mrsa.html              ← MRSA + CC breakdown + country/source cross-tabs
        ├── amr.html               ← gene retrieval
        ├── vfdb.html
        └── plasmid.html
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

This runs every generator, gzips `metadata.tsv`, refreshes the bulk zip, and finishes with `fix_nav.py` to guarantee the 17-link nav across all pages.

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

> **Beckley B, Olalekan A, Afeke I, Amarh V.** SAURUS: an interactive web resource for typing-based genome retrieval in *Staphylococcus aureus*. *BMC Genom Data* [under review]. 2026. https://doi.org/10.5281/zenodo.23264894
> **Beckley B, Olalekan A, Afeke I, Amarh V.** SAURUS: an interactive web resource for typing-based genome retrieval in *Staphylococcus aureus*. *Zenodo*. 2026. https://doi.org/10.5281/zenodo.23264894

### SAURUS-CLI

> **Beckley B** SAURUS-CLI: a reproducible command-line interface for typing-based genome retrieval in *Staphylococcus aureus*. *BMC Bioinformatics* [under review]. 2026.
> [github.com/bbeckley-hub/saurus-cli](https://github.com/bbeckley-hub/saurus-cli)

### Typing pipeline

> **Beckley B, Amarh V.** StaphScope: a species-optimized computational pipeline for rapid and accessible *Staphylococcus aureus* genotyping and surveillance. *BMC Genomics*. 2026;27:261.
> [doi:10.1186/s12864-026-12609-x](https://doi.org/10.1186/s12864-026-12609-x)

### Gene dataset

> **Shelenkov A, Slavokhotova A, Yunusova M, et al.** Genomic typing, antimicrobial resistance gene, virulence factor and plasmid replicon database for the important pathogenic bacteria *Staphylococcus aureus*. *BMC Genom Data*. 2025;26:65.
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
