# phi-med-amr-reanalysis

Reanalysis pipeline for drug-identity vs. escalation-dynamics effects on antibiotic
resistance mutation pathway ordering (Φ_med framework).

Companion code for the manuscript **"Drug identity determines the temporal order of
competing adaptive pathways"**, submitted to *Proceedings of the Royal Society B*.

## Purpose

This notebook implements the statistical toolkit and data-loading/classification
pipeline used to reanalyse raw, publicly deposited supplementary datasets from six
independent experimental-evolution studies, in order to test whether the temporal
order of competing resistance-conferring mutation pathways (TARGET-first vs.
REGULATORY-first) is determined primarily by drug identity or by escalation
dynamics.

It accompanies the manuscript's Data, Code and Materials Availability statement and
is a self-contained, from-source-data rebuild of the described methodology:

- Earliest-crossing TARGET/REGULATORY classification protocol
- Fisher's exact test with Haldane–Anscombe corrected odds ratios
- Holm and Benjamini–Hochberg multiple-comparison correction
- A Beta-Binomial Bayes factor
- Ridge-penalised Cox proportional-hazards regression
- The Nelson–Aalen cumulative-hazard estimator

## Important caveats (please read before reusing)

- **This is an independent rebuild, not a transcription of the original analysis
  scripts** (those were not available at the time of writing). Every statistical
  function has been checked against synthetic data with known ground truth (see the
  "self-test" cells in Section 1.1).
- The `GENE_PANELS` definitions used for TARGET/REGULATORY classification
  (Section 3) were reconstructed from the manuscript text. This is the single most
  consequential researcher-degree-of-freedom in the pipeline and should be verified
  against the manuscript's Methods section before reuse.
- The Cox regression and Nelson–Aalen estimator are **custom NumPy/SciPy
  implementations**, built in an offline development environment without access to `lifelines`
  or `statsmodels`. Cross-checking against `lifelines.CoxPHFitter` /
  `lifelines.NelsonAalenFitter` is recommended before relying on these for
  publication-facing numbers.
- See Section 12 of the notebook ("Still not implemented / still missing data") for
  a full list of open items, including an unresolved clone-level co-occurrence claim
  (Cisneros-Mayoral et al.) and a minor unresolved discrepancy in the genotype
  complexity means for CEC-2/CEC-4 (does not affect any reported conclusion — the
  comparison is non-significant either way).

## Data availability

**No raw data are redistributed in this repository.** Only loader code that reads
locally-placed copies of the original authors' publicly deposited supplementary
files is included. Please obtain the source files directly from each original
publication using the table below.

| Study | File(s) used | Source | Status |
|---|---|---|---|
| Zlamal et al. 2021, *mBio* (CIP) | `mbio.00987-21-sd002.xlsx`, `-sd003.xlsx`, `-t0001.pdf` | Data Set S2, S3, Table 1 | Table 1 reproduced exactly, all 5 runs |
| Leyn et al. 2024, *NPJ Antimicrob Resist* (GP6) | `media-1.xlsx` (S1A, S1B) | Supplementary Table S1AB | Table 5 reproduced exactly, both organisms |
| Yu et al. 2025, *Microbiol Spectr* (fleroxacin) | `spectrum.02981-24-s0002.xlsx`, `-s0003.xlsx` | Supplementary Tables S1–S2 | ESM Table S2 reproduced exactly, 6/6 samples |
| Lindsey et al. 2013, *Nature* (rifampicin) | `41586_2013_BFnature11879_MOESM27_ESM.pdf` | Supplementary Table 2 | Transcription verified exact, 121/121 rows |
| Leyn et al. (triclosan) | `000553_2.xlsx`, curated `S6_*.csv` | Data Set S6 | Spot-checked against raw sheet, consistent |
| Kent et al. 2025, *Antimicrob Agents Chemother* (COL/TGC) | `aac.00809-25-s0002.xlsx` | Supplementary Tables S1–S14 | Table 6 reproduced exactly, all 6 sub-comparisons |
| Cisneros-Mayoral et al. 2022, *Mol Biol Evol* (ampicillin) | `MS_filt_all_mut.csv`, `SS_filt_all_mut.csv`, `AMP_transfer_reps.csv` | `github.com/ccg-esb-lab/evoAMP` (`main` branch) | Table 2 reproduced exactly (population-level); clone-level co-occurrence claim (Data Set S5) unverified |

Two additional supplementary files (`elife-47612-supp2.xlsx`,
`msab025_supplementary_data.pdf`) were checked and found to belong to an unrelated
study (erythromycin / AcrB-GFP efflux dynamics), not cited in this manuscript. No
loaders were written for them.

When citing or depositing this notebook, please link back to each original
publication's own supplementary-material page rather than re-hosting these files,
in line with standard practice and each publisher's terms of reuse.

## How to run

The notebook is designed to run in Google Colab or a local Jupyter environment.

1. Clone this repository.
2. Download the source supplementary files listed in the table above from each
   publisher (or the `evoAMP` GitHub repository for the Cisneros-Mayoral data) and
   place them in the working directory alongside the notebook.
3. Open `phi_med_reanalysis_pipeline.ipynb` (this notebook) and run all cells top to bottom.
4. For publication-facing numbers, consider installing `lifelines` and cross-checking
   the Cox regression / Nelson–Aalen results (see caveats above).

## License

Code is released under the MIT License (see `LICENSE`). This license applies only
to the analysis code in this repository, not to any third-party data files, which
remain subject to their original publishers' terms.

## Citation

If you use this code, please cite:

Okabe H. phi-med-amr-reanalysis: reanalysis pipeline for Φ_med (drug identity vs.
escalation dynamics in antibiotic-resistance pathway ordering), v1.0.0. Zenodo 2026.
doi:[10.5281/zenodo.21869413](https://doi.org/10.5281/zenodo.21869413)

The companion manuscript is available as a preprint:

Okabe H. Drug identity determines the temporal order of competing adaptive pathways
in antibiotic resistance evolution. Zenodo 2026.
doi:[10.5281/zenodo.21869202](https://doi.org/10.5281/zenodo.21869202)

## Contact

Hiroyuki Okabe ([@shirasagiakemi](https://github.com/shirasagiakemi))
