# Estrogen / sex-hormones and intracranial aneurysm, Mendelian randomization

Two-sample MR of sex-hormone and reproductive-timing exposures (age at natural
menopause, SHBG, bioavailable/total testosterone, age at menarche, estradiol) on
**intracranial aneurysm (IA)** and **aneurysmal SAH**, using public GWAS summary
statistics. Companion causal arm to the `estrogen-asah-dci` ICU pilot, immune to
the age/ascertainment confounding that limits observational ICU data.

**Gap addressed** (see `docs/adr/0001`): resolve the published SHBG direction-of-
effect conflict (Molenberg 2022 vs Tan/Wu 2025) and test *continuous* age at
natural menopause (Ruth 2021) against rupture-stratified Bakker 2020 outcomes
(UKB-excluded, to avoid sample overlap).

## Status

Primary analysis complete. The GWAS have been downloaded, instruments selected and
harmonized, and the full analysis plan run, including sensitivity, power, and a
passing positive control. What remains is optional extension work, not a blocker.

### Results (age at natural menopause -> aneurysmal SAH)

No protective effect. Random-effects IVW odds ratio 1.03 per year of later
menopause (95% CI 0.97 to 1.09), about 1.12 per standard deviation. 85 instruments,
mean F 98, Steiger 80/85 in the correct direction, MR-Egger intercept P 0.19,
MR-PRESSO global P 0.17, leave-one-out stable (1.01 to 1.04). Equivalence testing
excludes protection stronger than an odds ratio of 0.90 per standard deviation
(P 0.027) but cannot exclude the null or mild harm (P 0.53); power to detect an
odds ratio of 0.90 per standard deviation was 15%. Report the finding as a bound,
not as "no effect".

### Positive control (age at natural menopause -> breast cancer): PASSES

The identical pipeline recovers the established effect of later menopause on breast
cancer: weighted-median odds ratio 1.055 per year (95% CI 1.041 to 1.069), IVW
P 1.8e-25, 207 instruments (Michailidou 2017, GRCh37 build). This validates the
instruments, genome build, matching, and power, so the aSAH null is credible
evidence rather than a broken pipeline.

### Optional extensions (not blocking)

Multi-exposure MR (add SHBG and testosterone; multivariable MR to resolve the
Molenberg 2022 vs Tan/Wu 2025 SHBG conflict); proper r^2 LD clumping against a
1000G panel in place of the current distance clumping.

## Run

```bash
uv sync --extra dev
uv run pytest                       # estimator + harmonization + QC tests (no data)
python scripts/run_mr_full.py       # ANM -> aSAH, full QC + power + equivalence
python scripts/run_mr_poscontrol.py # positive control: ANM -> breast cancer
```

GWAS summary statistics are not committed (large / restricted); `sources.py` lists
exact provenance, `docs/gwas_access.md` explains how to fetch them, and `data/gwas/`
is git-ignored.

## License

Code: MIT. Uses only public, published GWAS summary statistics per their terms.
