# Changelog

All notable changes to the SAURUS web resource are documented here.
The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).
Data releases are versioned independently of the generator scripts.

## [Unreleased]

## [0.8.1] — 2026-11-07

### Added
- SRA raw-read export: every typing page now exports BioSamples, SRA
  Runs, or BioProjects alongside the existing assembly accessions.
  22,277 of 134,160 genomes (16.6%) have at least one resolved SRA run.
- Searchable, frequency-sorted datalists for ST, CC, and spa filters.
- BioProject and BioSample columns on every typing page (toggleable via
  the Columns panel).
- Methods section on the About page with six subsections documenting
  data sources, typing pipeline, deduplication, reproducibility, data
  access, and correction reporting.
- Raw Sequencing Reads section on the homepage with per-tool
  recommendations and paired-end/multi-run tradeoffs.

### Fixed
- Compare page count now reports 134,160, not 139,257 (union bug that
  included filtered-out accessions).
- Year dropdown no longer shows `2020` and `2020.0` as separate entries.
- Sortable filter dropdowns now use semantic sorting: newest-first for
  year, alphabetical for country, frequency for source, numeric for
  MLST, Roman for agr, semantic for capsule.

## [0.8.0] — 2026-11-02

### Added
- Complete de novo typing of all 134,160 publicly available S. aureus
  genomes in the NCBI Assembly database (MLST, spa, SCCmec dual
  callers, capsule, agr).
- BioProject, BioSample, and full BioSample metadata columns on every
  typing page.
- Sortable filter dropdowns across all pages.
- New Methods section on the About page.
- Hero "Download data" CTA on the homepage.

### Fixed
- Compare page count bug (139,257 → 134,160).
- Year dropdown duplicate entries.
- spa regex now accepts letter-suffixed alleles (`t1234a`).
- Gene retrieval pages show "showing N of M" instead of a silent
  1000-row cap.
- `SCCmec_type_IV(2B)` and `Type IV(2B)` normalised to the same value.
- Complete deduplication: 115 cross-prefix pairs, 12 version conflicts,
  9,996 cross-batch duplicates collapsed deterministically.

### Changed
- Nav canonicalisation runs as the final step of every regeneration.

## [0.7.0] — 2026-10-28

### Added
- 134,299 unique genomes indexed (GCA + GCF deduplicated).
- 98,138 genomes typed de novo with StaphScope v2.0.0.
- Country, isolation source, host, and collection year integrated as
  columns and filters on every page.
- Dual SCCmec callers (CGE and RPet) reported side by side with an
  agreement chart.
- Lineage catalogue of ~50 clonal complexes with live sample counts
  and one-click export.

## [0.6.0] — 2026-10-19

### Changed
- Typed an additional 10,000 GenBank (GCA) genomes, moving the typed
  set to 80,000 genomes.

### Fixed
- Collection bug in the SCCmec and MRSA tabs.

## [0.5.1] — 2026-10-17

### Fixed
- Column names normalised by stripping `ASM`/`PDT`/`_genomic.fna`
  suffixes from sample names.
- 9,971 duplicate rows collapsed (batch overlap): 80,124 rows →
  70,153 unique genomes.

## [0.5.0] — 2026-10-17

### Added
- Typing, gene annotations, and epidemiological metadata for 70,153
  public S. aureus genomes.
- Country, source, host, and collection year as queryable fields.

## [0.4] — 2026-10-15

### Added
- Typing coverage grew from 26,197 to 56,197 genomes (full RefSeq set
  plus the first three GenBank batches: 40K, 50K, 60K).
- Temporal Trends page with eight interactive charts and a year-range
  slider synced to URL parameters.
- Compare page: side-by-side comparison of two groups across four
  modes (CC vs CC, Country vs Country, Source vs Source, Year vs Year).
- Canonical 17-link navigation across every page.

### Changed
- MRSA consensus and SCCmec type now use the CGE caller everywhere
  (MRSA, Trends, Statistics, Index) for consistency across pages.

## Earlier releases

Versions before v0.4 (v0.3, v0.2.x, v0.2, v0.1)

- v0.2.2 — published 2026-10-10
- v0.2.1 — published 2026-10-10
- v0.2 — published 2026-10-09

Full Zenodo record: https://zenodo.org/records/ (search for
`bbeckley-hub/saurus`)
