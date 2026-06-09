# Reproducing the ENIGMA-OCD White-Matter × Symptom-Severity Analysis

A reproduction project testing whether diffusion-MRI (DTI) measures of white-matter
microstructure scale with **OCD symptom severity** (Yale–Brown Obsessive–Compulsive
Scale, 2nd ed.; Y-BOCS-II), in a single-site adult OCD sample.

This reproduces the **brain–symptom-severity** component of:

> Piras, F., Piras, F., Abe, Y., … Spalletta, G. (2021). White matter microstructure and
> its relation to clinical features of obsessive–compulsive disorder: Findings from the
> ENIGMA OCD Working Group. *Translational Psychiatry, 11*(1), 173.
> https://doi.org/10.1038/s41398-021-01276-z

**Author:** Oscar Delfín · Stanford Symbolic Systems, M.S. Candidate '26
**Context:** Psych 251 Reproduction Project (Professor Michael Frank, PhD) · June 2026

---

## Key finding

Across 15 hypothesis-driven cortico–striato–thalamo–cortical / posterior white-matter
bundles and four DTI metrics (FA, MD, RD, AD), **baseline Y-BOCS-II severity was not
significantly associated with white-matter microstructure** after false-discovery-rate
(FDR) correction — **0 of 90 tests** survived (minimum uncorrected *p* = .115; maximum
|partial *r*| = .23). This **replicates the ENIGMA-OCD null severity result**, consistent
with a trait- rather than state-marker interpretation. See the report/notebook for the
full limitations (no control group, severity-range restriction, modest power).

---

## Repository contents

| File | Description |
|------|-------------|
| `ocd_dti_enigma_reproduction.ipynb` | Main analysis notebook (intro → methods → results → discussion → provenance appendix). Recomputes everything from the dataset. |
| `ocd_dti_enigma_reproduction.html` | Rendered, read-only export of the notebook. |
| `ENIGMA_OCD_DTI_reproduction_report.pdf` | Formatted write-up (APA references). |
| `OCD_DTI_reproduction_summary.pptx` | Slide summary. |
| `figures/` | Generated figures (PNG). |
| `tables/` | Generated **aggregate** result tables (CSV) — group-level statistics only. |
| `requirements.txt` | Python dependencies. |
| `.gitignore` | Keeps the patient-level dataset out of the repository. |

---

## Data availability

**The dataset is *not* included in this repository and will not be committed to it.**
The analysis uses individual-level clinical data from a single-site rTMS trial for OCD;
the specific study and source laboratory are withheld to protect participant
confidentiality. The data are not publicly available and are subject to institutional
review board (IRB) approval and a data-use agreement. Access requests should be directed
to the data-holding laboratory.

Only **de-identified, group-level** outputs (the figures and the tables in `tables/`) are
shared here. No participant identifiers appear in any file in this repository.

---

## Setup & reproduction

Using conda (recommended):

```bash
conda create -n ocd -c conda-forge python=3.11 numpy pandas scipy statsmodels matplotlib jupyter ipykernel
conda activate ocd
```

Or with pip:

```bash
pip install -r requirements.txt
```

Then:

```bash
jupyter lab        # or: jupyter notebook
```

Open `ocd_dti_enigma_reproduction.ipynb`, make sure the kernel points at the `ocd`
environment, place the dataset CSV in the repo root, and **Run All**. The first code cell
("Setup") will install any missing packages automatically.

---

## Methods (summary)

- **Outcome:** baseline Y-BOCS-II total severity (plus obsession/compulsion subscales).
- **Predictors:** FA (primary), MD, RD, AD for 15 CSTC/posterior bundles.
- **Model:** `DTI metric ~ Y-BOCS-II + age + sex` (OLS), mirroring ENIGMA's age + sex adjustment.
- **Effect size:** partial correlation (*r*ₚ) with 95% CIs (Fisher *z*).
- **Multiple comparisons:** Benjamini–Hochberg FDR per metric/severity family.
- **Note on faithfulness:** ENIGMA tested severity at the between-site meta-regression level;
  this single-site study uses the more direct subject-level regression. The design is
  cross-sectional and observational, like ENIGMA.

## Reproducibility / provenance

The notebook's appendix prints a **SHA-256 fingerprint** of the exact CSV used and runs
live assertions that re-derive the headline numbers from source (no participant
identifiers are printed). If the assertions pass, every reported figure and table value is
reproducible from the data.

---

## citation

Piras, F., Piras, F., Abe, Y., Agarwal, S. M., Anticevic, A., Ameis, S., Arnold, P., Banaj, N., Bargalló, N., Batistuzzo, M. C., Benedetti, F., Beucke, J. C., Boedhoe, P. S. W., Bollettini, I., Brem, S., Calvo, A., Cho, K. I. K., Ciullo, V., Dallaspezia, S., Dickie, E., … Spalletta, G. (2021). White matter microstructure and its relation to clinical features of obsessive-compulsive disorder: findings from the ENIGMA OCD Working Group. Translational psychiatry, 11(1), 173. https://doi.org/10.1038/s41398-021-01276-z

## ethics

This work is a course reproduction project and is not
a substitute for the original peer-reviewed findings.
