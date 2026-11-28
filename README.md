# SAURUS — source release

Staphylococcus aureus Unified Resource for Universal Surveillance:
the complete pipeline state behind the live SAURUS site, shipped as a
checkpoint release. Every large file is a `.gz` seed; clone, restore,
regenerate — or type new genomes and extend it.

## Start here

| You want to... | Read first |
|---|---|
| Regenerate the site exactly as shipped | merged/README.md |
| Type new genomes on an HPC and add a batch | HPC_scripts/README.md |
| Find which script to rerun when a number is off | scripts/README.md |
| Understand the shipped batches | batches/README.md |
| Edit or redeploy the site | docs/README.md |

## Repo map

    HPC_scripts/   typing lane: download + StaphScope 2.1.0 (PBS/Torque)
    batches/       14 checkpoint batches, .tsv.gz seeds (134,160 genomes)
    merged/        merged tables (.gz seeds) + all site generators
    scripts/       pipeline in locked order + restore_seeds.sh
    docs/          the generated site (GitHub Pages root)
    images/        banner

## Two quick paths

Fresh regeneration of the shipped state:

    bash scripts/restore_seeds.sh
    bash scripts/Regenerate_all.sh ~/saurus/merged
    # or step-by-step: 01_merge_modules.sh -> gen_all.sh ->
    # Regenerate_gzipped.sh -> rebuild_bulk_zip.sh

Adding new genomes:

    HPC_scripts lane -> batches/batch_new/ -> 01_merge_modules.sh ->
    metadata lane (new accessions only) -> Regenerate_all.sh

## Provenance and honesty

- Typing: StaphScope 2.1.0, Singularity 3.6.4, PBS/Torque.
- Gene annotations: Shelenkov et al. (2025), keyed by GCA accessions;
  static inputs, never regenerated.
- The CLI master table (mrsa_all.tsv) is built by saurus-cli v0.4.0 and
  copied back into merged/ for packaging (two-lane model).
- Gene-page search vocabulary derives from the curated freq tables
  (174/26/177) at build time; an unmatched-gene warning is a tripwire
  and should never appear.
- Exported accession lists are not independently validated against
  published studies; treat them as retrievals from the underlying
  accessions, not as curated epidemiological sets.
- Headline counts: 134,160 typed genomes; 174/26/177 curated genes
  (351,692/1,136,550/224,924 rows); MRSA 80,220-80,224 depending on
  definition; 133 countries plotted; SRA 22,322 (16.6%).

## Citation

Beckley B, Amarh V. StaphScope. BMC Genomics. 2026;27:261.
doi:10.1186/s12864-026-12609-x
Gene data: Shelenkov A, Mikhailova Y. BMC Genomic Data (2025).
Data bundle: doi:10.5281/zenodo.24568725 (saurus-data v1.1.0)
