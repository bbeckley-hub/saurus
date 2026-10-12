<div align="center">

<img src="images/saurus_banner.png" alt="SAURUS banner" width="100%">

# 🦖 SAURUS

**Staphylococcus aureus Unified Resource for Universal Surveillance**

*One database. Every typing module. Every genome geolocated. Free and open.*

[![Live Site](https://img.shields.io/badge/🌐_Live_Site-bbeckley--hub.github.io/saurus-d4af37?style=for-the-badge)](https://bbeckley-hub.github.io/saurus/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](LICENSE)
[![Genomes](https://img.shields.io/badge/Genomes-26K%20→%20126K-blue?style=for-the-badge)](https://bbeckley-hub.github.io/saurus/)
[![Modules](https://img.shields.io/badge/Modules-11-purple?style=for-the-badge)](https://bbeckley-hub.github.io/saurus/)
[![Countries](https://img.shields.io/badge/Countries-105-0ea5e9?style=for-the-badge)](https://bbeckley-hub.github.io/saurus/geography.html)
[![Part of ARGUS](https://img.shields.io/badge/Part%20of-ARGUS-0a1628?style=for-the-badge)](https://github.com/bbeckley-hub/eclipse)
[![Status](https://img.shields.io/badge/Status-v0.2-brightgreen?style=for-the-badge)](https://github.com/bbeckley-hub/saurus/releases)

[**🏠 Home**](https://bbeckley-hub.github.io/saurus/) ·
[**🌍 Geography**](https://bbeckley-hub.github.io/saurus/geography.html) ·
[**🧬 Lineages**](https://bbeckley-hub.github.io/saurus/lineages.html) ·
[**📥 Downloads**](https://bbeckley-hub.github.io/saurus/downloads.html) ·
[**ℹ️ About**](https://bbeckley-hub.github.io/saurus/about.html)

</div>

---

## 📖 What is SAURUS?

**SAURUS** is an open-access genomic resource that integrates every major *Staphylococcus aureus* typing and gene-annotation scheme — **plus country, isolation source, host, and collection year** — into a single, queryable interface:

| Category | Modules |
|---|---|
| **Typing** | MLST · spa · SCCmec (CGE + RPet) · agr · capsule |
| **Genes** | AMR · Virulence (VFDB) · Plasmid replicons |
| **Clinical** | MRSA/MSSA consensus |
| **Epidemiology** | Country · isolation source · host · collection year |
| **Lineage context** | Curated catalogue of ~50 clonal complexes |
| **Retrieval** | Search → filter → export accession lists in one click |

No login, no API key, no install. Runs entirely in your browser over HTTPS.

> **The core deliverable is accession retrieval.** Every page lets you filter by genotype *and* geography and download the exact list of genome accessions that match — ready to feed to `datasets download genome accession`.

---

## 👁️ Part of the ARGUS family

SAURUS is the **flagship build** of **ARGUS** — *Antimicrobial Resistance Genomic Unified Surveillance* — a family of independent, open genomic surveillance sites, each dedicated to one of the WHO priority ESKAPE pathogens. Every resource shares the same architecture: accession-first, metadata-integrated, no login, no install, MIT-licensed. Each has its own name, its own DOI, and its own community.

Named for **Argus Panoptes** — the hundred-eyed giant of Greek myth who never slept — the umbrella is a bet that AMR surveillance has to be *unified* to be useful, and that the pathogens driving the crisis deserve the same treatment.

| Resource | Pathogen | Status |
|---|---|---|
| 🦖 **SAURUS** | *Staphylococcus aureus* | **This repo** — [live](https://bbeckley-hub.github.io/saurus/) |
| 🌑 **ECLIPSE** | *Escherichia coli* | [Live](https://bbeckley-hub.github.io/eclipse) |
| 🌊 **ABYSS** | *Acinetobacter baumannii* | Planned |
| 🏆 **KLEOS** | *Klebsiella pneumoniae* | Planned |
| 💧 **PSEUDA** | *Pseudomonas aeruginosa* | Planned |
| 👑 **EMPIRE** | *Enterococcus faecium* | Planned |
| 🌀 **ENTROPY** | *Enterobacter* spp. | Planned |

Every sibling is built on the same architecture — a static site, accession-first design, with a shared generator template. That means once one resource works, the next one ships in weeks rather than months, and every resource benefits from improvements made in any other.

---

## 🎯 Project goal — annotate all 126,245 public *S. aureus* genomes

SAURUS is being built incrementally toward a single milestone: **the complete annotation of every public *S. aureus* genome** in the NCBI Assembly database.

| Milestone | Scope | Status |
|---|---|---|
| **v0.1** | 20K RefSeq (GCF) genomes, 9 modules | ✅ **live** |
| **v0.2** | + Country · Source · Host · Year metadata · **Geography page** | ✅ **live** |
| **v0.3** | Full 26,197 GCF genomes · 913 STs · 13 CCs | ✅ **merged into v0.2** |
| **v0.4** | + 33,985 unique GCA genomes | 🔜 **next** |
| **v0.5** | + 73,472 Shelenkov-only GCA genomes | 📋 planned |
| **v1.0** | **126,245 genomes · unified master table · citable resource** | 🎯 target |

See the [**Roadmap**](#-roadmap) below for details.

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

### 🌍 Geography &amp; Metadata

- **26,349 BioSample records** across **105 countries**
- **250 source categories** — clinical, food, environmental, animal
- **4 interactive charts** — countries, sources, timeline, hosts
- **5 filters** — country · source · host · year · assembly level
- **Full provenance** — raw submitter strings preserved
- Combined queries: *`ST5` + `MRSA` + `United States` + `blood`*

</td>
</tr>
<tr>
<td valign="top">

### 🧬 Gene retrieval pages

- **Up to 5 genes per query**
- **ANY / ALL** match logic
- **Curated headline genes** for AMR, virulence, plasmid
- One-click **accession list export**
- **Click-to-copy** accession per row
- **Frequency table** — sortable, filterable

</td>
<td valign="top">

### 📚 Lineage catalogue

- ~50 curated clonal complexes
- **Live sample counts** from the current dataset
- **Reference-only cards** for lineages with no samples yet
- **Export all accessions** per lineage
- Geographic + clinical + virulence context per CC

</td>
</tr>
<tr>
<td valign="top">

### 📊 Statistics page

- Top 20 STs with **MRSA % overlay**
- CC distribution · spa distribution
- **SCCmec RPet vs CGE** side by side
- **4-level alluvial:** SCCmec → agr → Capsule → MRSA
- CC × SCCmec heatmap
- Capsule by CC stacked bars

</td>
<td valign="top">

### 📥 Bulk downloads

- Every merged TSV as `.tsv.gz`
- Row counts + file sizes at a glance
- **`metadata.tsv.gz`** — full BioSample table
- **Long-format gene tables** — pivot-ready
- One-file-per-module layout

</td>
</tr>
</table>

---

## 🚀 Quick start

**Just visit the live site:**

### 👉 **https://bbeckley-hub.github.io/saurus/**

### Example workflow — get all ST5 MRSA blood isolates from the United States

1. Open [**MRSA**](https://bbeckley-hub.github.io/saurus/pages/mrsa.html) → filter:
   - `MRSA Status = MRSA`
   - `MLST = ST5`
   - `Country = United States`
   - `Source = blood`
2. Click **🧬 Accessions** → save the `.txt` file
3. Feed it to NCBI:

   ```bash
   datasets download genome accession --inputfile accessions.txt
   ```

4. ✅ You have the exact genomes you want, filtered by genotype *and* geography

Or start from the [**Geography page**](https://bbeckley-hub.github.io/saurus/geography.html) to browse the collection by country, source, host, or year.

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
<summary><b>v0.2 — Epidemiological metadata</b> ✅ live</summary>

- [x] Country + isolation source + host + collection year from NCBI BioSample
- [x] Free-text sources normalized into ~30 categories
- [x] **Country** and **Source** filters on every typing page
- [x] **Country × MRSA** and **Source × MRSA** cross-tabs
- [x] New **Geography** page — 4 charts, 5 filters, full metadata browser
- [x] `metadata.tsv.gz` added to downloads

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

</details>

<details>
<summary><b>v0.5 — Shelenkov-only GenBank</b> 📋 planned</summary>

- [ ] + 73,472 GCA genomes where SCCmec / agr / capsule are re-typed by StaphScope
- [ ] AMR / virulence / plasmid annotations carried forward from Shelenkov et al. (2025)
- [ ] Deduplication pass

</details>

<details>
<summary><b>v1.0 — Full resource</b> 🎯 target</summary>

- [ ] **126,245 genomes** with unified master table
- [ ] Cross-module filter UI — CC + SCCmec + agr + capsule + country + source + any gene
- [ ] Boolean query builder for advanced users
- [ ] **Zenodo DOI** for citable release
- [ ] Database article submitted (*Database* — Oxford)

</details>

---

## 🧬 Data sources

| Layer | Source | Coverage |
|---|---|---|
| **Typing** | [StaphScope v2.0.0](https://github.com/bbeckley-hub/staphscope-typing-tool) on RefSeq genomes | 26,197 GCF → 126K |
| **Country / source / host / year** | [NCBI BioSample](https://www.ncbi.nlm.nih.gov/biosample/) via `datasets summary genome` | 26,349 records · 92% country · 74% source |
| **AMR genes** | [Shelenkov et al. 2025](https://doi.org/10.1186/s12863-025-01363-w) | 86,318 GCA |
| **Virulence (VFDB)** | Shelenkov et al. 2025 | 98,950 GCA |
| **Plasmid replicons** | Shelenkov et al. 2025 | 86,318 GCA |
| **Lineage reference** | Curated (literature-validated) | ~50 CCs |

All genome identifiers use the standard `GCA_XXXXXXXXX.Y` or `GCF_XXXXXXXXX.Y` format.

---

## 📁 Repository structure

```
saurus/
├── README.md
├── LICENSE
├── images/
│   └── saurus_banner.png
└── docs/                          ← GitHub Pages site (source: main /docs)
    ├── .nojekyll
    ├── index.html                 ← landing page
    ├── about.html                 ← project + team + methods
    ├── statistics.html            ← 9+ charts (ST+MRSA, CC×SCCmec, alluvial)
    ├── geography.html             ← NEW — metadata browser + 4 charts
    ├── lineages.html              ← curated CC catalogue
    ├── downloads.html             ← bulk data index
    ├── assets/
    │   └── chart.min.js           ← Chart.js (bundled locally)
    ├── data/                      ← bulk .tsv.gz downloads
    │   ├── *.tsv.gz               ← typing + gene tables
    │   ├── metadata.tsv.gz        ← NEW — BioSample metadata
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

## 🛠️ Running locally

**Prerequisites:** Python 3.9+

```bash
git clone https://github.com/bbeckley-hub/saurus.git
cd saurus/docs
python3 -m http.server 8000
```

Open **http://localhost:8000/**.

> ⚠️ **HTTP required.** The gene retrieval pages use `fetch()` to load JSON. Browsers block this from `file://` URLs. Served over HTTP (or from GitHub Pages), it just works.

---

## 🧪 Regenerating pages

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

---

## 📚 Citation

If you use SAURUS in your research, please cite the pipeline and the source gene dataset.

### Typing pipeline

> **Beckley B, Amarh V.** StaphScope: a species-optimized computational pipeline for rapid and accessible *Staphylococcus aureus* genotyping and surveillance. *BMC Genomics*. 2026;27:261.
> [doi:10.1186/s12864-026-12609-x](https://doi.org/10.1186/s12864-026-12609-x)

### Gene dataset

> **Shelenkov A, Slavakhotova A, Yunusova M, et al.** Genomic typing, antimicrobial resistance gene, virulence factor and plasmid replicon database for the important pathogenic bacteria *Staphylococcus aureus*. *BMC Genom Data*. 2025;26:65.
> [doi:10.1186/s12863-025-01363-w](https://doi.org/10.1186/s12863-025-01363-w)

### Metadata source

> **NCBI BioSample** — country, isolation source, host, and collection date attributes attached to each RefSeq assembly.

### Cite SAURUS itself

> **Beckley B.** SAURUS: *Staphylococcus aureus* Unified Resource for Universal Surveillance. 2026.
> [github.com/bbeckley-hub/saurus](https://github.com/bbeckley-hub/saurus)

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

**[⭐ Star this repo](https://github.com/bbeckley-hub/saurus)** if you find it useful.

</div>
