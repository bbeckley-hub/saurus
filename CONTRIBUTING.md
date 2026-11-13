
# Contributing to SAURUS and ARGUS

Thank you for considering a contribution. SAURUS and the ARGUS
initiative are built by a small team, and every issue, correction, or
new species resource makes the platform more useful for the
surveillance community.

This guide covers:

1. Reporting bugs and data errors
2. Suggesting new features
3. Contributing code
4. Contributing a new ARGUS species resource
5. Joining the ARGUS initiative as a collaborator

---

## Before you start

Please read the [Code of Conduct](CODE_OF_CONDUCT.md). The short
version: be direct, be kind, credit others, keep disagreements about
the work.

For questions that are not bugs (e.g., "would this be useful for my
lab?"), open a
[GitHub Discussion](https://github.com/bbeckley-hub/saurus/discussions)
rather than an issue. Issues should be actionable.

---

## 1. Reporting bugs and data errors

SAURUS integrates data from multiple upstream sources. Some reports are
about the code, some about the data, and some about the pipeline that
generated both. Knowing which one you are reporting saves time.

### Code bugs (interface, CLI, fsspec)

Open an issue at the relevant repository:

| Repository | Report here |
|---|---|
| Web interface (saurus-db.org) | [bbeckley-hub/saurus/issues](https://github.com/bbeckley-hub/saurus/issues) |
| Command-line interface | [bbeckley-hub/saurus-cli/issues](https://github.com/bbeckley-hub/saurus-cli/issues) |
| fsspec plugin | [bbeckley-hub/saurus-fsspec/issues](https://github.com/bbeckley-hub/saurus-fsspec/issues) |

Include:

- What you expected to happen
- What happened instead
- The exact command or URL, if applicable
- Your browser or Python version
- A screenshot if the bug is visual

### Data errors (wrong typing, wrong metadata)

If you believe a genome is mistyped, has incorrect metadata, or is
missing from the collection, open an issue with the prefix `[data]`:

```
Title: [data] GCA_XXXXXXXXX.1 assigned to CC8 but appears to be CC5

Accession: GCA_XXXXXXXXX.1
Field: mlst_cc
Current value: CC8
Expected value: CC5
Evidence: [link to MLST profile, PubMLST query, or reference]
```

For metadata errors, include the BioSample accession and, if
available, the raw value you expect.

### Wrong typing from the upstream pipeline

Some typing calls come from StaphScope (the upstream pipeline). If you
believe the pipeline assigned a wrong ST, spa type, or SCCmec call,
open the issue in [bbeckley-hub/staphscope-typing-tool](https://github.com/bbeckley-hub/staphscope-typing-tool)
and tag it `[typing]`. These reports help improve both SAURUS and the
pipeline.

---

## 2. Suggesting new features

Open a discussion first, not an issue. Feature suggestions often
benefit from a short conversation about whether the feature fits the
project's scope, and discussions are the right place for that.

In the discussion, describe:

- The workflow or question you are trying to answer
- How you currently solve it (even if it is slow)
- What a good solution would look like
- Whether you are willing to contribute to the implementation

Feature requests without a concrete workflow are harder to prioritise.
"Add a filter by X" is less useful than "I am trying to find all
isolates from Y context to study Z, and currently I do it manually."

---

## 3. Contributing code

For small fixes (typos, documentation, one-line bugs), open a pull
request directly. For anything larger, open an issue first and
describe what you plan to do.

### Development setup

For the CLI:

```bash
git clone https://github.com/bbeckley-hub/saurus-cli.git
cd saurus-cli
pip install -e ".[dev]"
pytest -m "not network"
```

For the fsspec plugin:

```bash
git clone https://github.com/bbeckley-hub/saurus-fsspec.git
cd saurus-fsspec
pip install -e ".[dev]"
pytest -m "not network"
```

For the web resource:

```bash
git clone https://github.com/bbeckley-hub/saurus.git
cd saurus
# Data pipeline scripts are in scripts/
# Static site generators are in merged/
# See the README for the regeneration workflow
```

### Pull request guidelines

- Keep pull requests focused on one change
- Add a test if the change touches behaviour
- Update the CHANGELOG under the unreleased section
- Reference the issue the pull request resolves
- Describe what changed and why in the pull request body

A pull request that touches twenty files with no explanation will be
asked to split into smaller changes. A pull request that touches two
files with a clear description will be reviewed within a week.

### Review process

The maintainer reviews pull requests within 7 working days. If you do
not hear back, tag the pull request with a comment. Repeat pings within
7 days are not necessary and slow the review queue.

---

## 4. Contributing a new ARGUS species resource

ARGUS currently hosts SAURUS (*S. aureus*) and ECLIPSE (*E. coli*),
with resources for *A. baumannii*, *K. pneumoniae*, *P. aeruginosa*,
*E. faecium*, and *Enterobacter* spp. in planning.

Adding a new species resource requires four things:

### A species-optimized typing pipeline

The pipeline must produce per-sample summary tables that the SAURUS
generator scripts can consume without modification. If you have built
one for your species, open a discussion describing:

- The species and typing schemes
- The tools integrated
- Whether it is published, preprint, or in progress
- A link to the repository or container

### A genome collection

The collection needs to cover the public repository for that species,
with the same deduplication and accession accounting that SAURUS uses.
If you have already typed the collection, describe the method and the
final count.

### A metadata layer

Country, isolation source, host, and collection year extracted from
NCBI BioSample, with the same normalisation approach SAURUS uses. The
normalisation scheme can differ by species, but the fields should
match.

### A maintainer

Every ARGUS resource has its own DOI, release cycle, and community.
The person proposing the resource is expected to be its primary
maintainer for at least the first two release cycles. SAURUS and
ARGUS provide the technical foundation; the species community provides
the domain expertise and the ongoing maintenance.

If you have all four, open a discussion titled
`[ARGUS] <species> resource proposal` and describe the plan. The
maintainer will respond within 7 working days.

---

## 5. Joining ARGUS as a collaborator

If you want to contribute to an existing resource (SAURUS, ECLIPSE, or
a planned one), you can start by:

- Triaging issues (labelling, reproducing, closing duplicates)
- Writing documentation or tutorials
- Reviewing pull requests in your area of expertise
- Contributing species-specific curations to the lineage catalogue
- Running the pipeline on genomes you care about and reporting errors

If your contributions are sustained and you want to be listed as a
co-maintainer, open a discussion describing what you have contributed
and what you would like to maintain. Co-maintainer status is granted
based on sustained contribution, not on request alone.

---

## Recognition

Every contributor is credited in the following places:

- The `CONTRIBUTORS.md` file in each repository
- The Zenodo DOI for the release their contribution landed in
- The specific module documentation (e.g., "lineage catalogue curated
  by X, Y, Z")

If your contribution led to a scientific finding, we encourage you to
co-author the resulting paper. Concrete contributions to data curation,
validation, or method development qualify for co-authorship under the
ICMJE criteria.

---

## Questions

Open a discussion or write to brownbeckley94@gmail.com. A short,
specific question gets a faster answer than a broad one.

Thank you for contributing.
