# Estrogen / sex-hormones and intracranial aneurysm — Mendelian randomization

Two-sample MR of sex-hormone and reproductive-timing exposures (age at natural
menopause, SHBG, bioavailable/total testosterone, age at menarche, estradiol) on
**intracranial aneurysm (IA)** and **aneurysmal SAH**, using public GWAS summary
statistics. Companion causal arm to the `estrogen-asah-dci` ICU pilot — immune to
the age/ascertainment confounding that limits observational ICU data.

**Gap addressed** (see `docs/adr/0001`): resolve the published SHBG direction-of-
effect conflict (Molenberg 2022 vs Tan/Wu 2025) and test *continuous* age at
natural menopause (Ruth 2021) against rupture-stratified Bakker 2020 outcomes
(UKB-excluded, to avoid sample overlap).

## Status

Scaffold + validated estimator core. Implemented and unit-tested: IVW, MR-Egger
(pleiotropy intercept), weighted median, Cochran's Q, allele harmonization —
checked against synthetic instruments with a known causal effect. Next: fetch the
GWAS (`sources.py`) into `data/gwas/`, select/clump instruments, run the SAP.

## Run

```bash
uv sync --extra dev
uv run pytest          # estimator + harmonization tests (no data needed)
```

GWAS summary statistics are not committed (large / restricted); `sources.py` lists
exact provenance and `data/gwas/` is git-ignored.

## License

Code: MIT. Uses only public, published GWAS summary statistics per their terms.
