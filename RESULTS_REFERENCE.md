# Results: 415 BabelStream HBM Bandwidth

**Main goal:** Measure sustained BabelStream HBM bandwidth  
**Tools:** Compile babelstream.cu with nvcc; run bin/babelstream via collect_babelstream.py

Reference results measured by the maintainer on the system shown in each section (generator TEMPLATE_00_138 · recorded 2026-11-12). Your own runs write `results/RESULTS_ACTUAL.md` in the same format.

> Smoke runs use deliberately small sizes. They check that the workload installs and runs end to end; their numbers are not performance results. Baseline and extended are.

<!-- profile:smoke -->
## smoke

- **System:** 1× NVIDIA H100 80GB HBM3 (81559 MiB) · Intel(R) Xeon(R) Platinum 8470 · Ubuntu 26.04.1 LTS · kernel 6.8.0-147-generic · driver 595.91.07
- **Run:** 2026-11-12T23:03:36Z · status **PASS** (exit 0)
- **Time (mm:ss):** setup 00:36 · benchmark 00:02 · whole run 00:47
- **Source:** run 415_20261112_230336
- **Command:** `bash run_benchmark.sh --smoke --device-id 0 --block-size 256 --array-size 67108864 --warmup-iters 1 --num-iterations 20`

| # | Metric | Result |
|---|---|---|
| 1 | Copy bandwidth (bandwidth_gb_s_copy) | 2916.039776 |
| 2 | Mul bandwidth (bandwidth_gb_s_mul) | 2914.646545 |
| 3 | Add bandwidth (bandwidth_gb_s_add) | 3104.094367 |
| 4 | Triad bandwidth (bandwidth_gb_s_triad) | 3102.640196 |
| 5 | Dot bandwidth (bandwidth_gb_s_dot) | 2793.107115 |
<!-- /profile:smoke -->
