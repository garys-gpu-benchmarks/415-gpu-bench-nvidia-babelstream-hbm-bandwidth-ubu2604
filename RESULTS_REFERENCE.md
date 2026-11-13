# Results: 415 BabelStream HBM Bandwidth

**Main goal:** Measure sustained BabelStream HBM bandwidth  
**Tools:** Compile babelstream.cu with nvcc; run bin/babelstream via collect_babelstream.py

Reference results measured by the maintainer on the system shown in each section (generator TEMPLATE_00_139 · recorded 2026-11-13). Your own runs write `results/RESULTS_ACTUAL.md` in the same format.

> Smoke runs use deliberately small sizes. They check that the workload installs and runs end to end; their numbers are not performance results. Baseline and extended are.

<!-- profile:smoke -->
## smoke

- **System:** 1× NVIDIA H100 PCIe (81559 MiB) · Intel(R) Xeon(R) Platinum 8352Y CPU @ 2.20GHz · Ubuntu 26.04.1 LTS · kernel 6.8.0-138-generic · driver 595.91.07
- **Run:** 2026-11-13T14:11:31Z · status **PASS** (exit 0)
- **Time (mm:ss):** setup 00:50 · benchmark 00:01 · whole run 01:03
- **Source:** run 415_20261113_141131
- **Command:** `bash run_benchmark.sh --smoke --device-id 0 --block-size 256 --array-size 67108864 --warmup-iters 1 --num-iterations 20`

| # | Metric | Result |
|---|---|---|
| 1 | Copy bandwidth (bandwidth_gb_s_copy) | 1838.926365 |
| 2 | Mul bandwidth (bandwidth_gb_s_mul) | 1836.254689 |
| 3 | Add bandwidth (bandwidth_gb_s_add) | 1898.326113 |
| 4 | Triad bandwidth (bandwidth_gb_s_triad) | 1898.490695 |
| 5 | Dot bandwidth (bandwidth_gb_s_dot) | 1963.688643 |
<!-- /profile:smoke -->
