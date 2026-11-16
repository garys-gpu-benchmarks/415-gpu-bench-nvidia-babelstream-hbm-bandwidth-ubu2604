# Results: 415 BabelStream HBM Bandwidth

**Main goal:** Measure sustained BabelStream HBM bandwidth  
**Tools:** Compile babelstream.cu with nvcc; run bin/babelstream via collect_babelstream.py

Reference results measured by the maintainer on the system shown in each section (generator TEMPLATE_00_143 · recorded 2026-11-16). Your own runs write `results/RESULTS_ACTUAL.md` in the same format.

> Smoke runs use deliberately small sizes. They check that the workload installs and runs end to end; their numbers are not performance results. Baseline and extended are.

<!-- profile:smoke -->
## smoke

- **System:** 1× NVIDIA H100 NVL (95830 MiB) · AMD EPYC 9374F 32-Core Processor · Ubuntu 26.04.1 LTS · kernel 6.8.0-138-generic · driver 595.91.07
- **Run:** 2026-11-16T19:31:21Z · status **PASS** (exit 0)
- **Time (mm:ss):** setup 00:30 · benchmark 00:02 · whole run 00:37
- **Source:** run 415_20261116_193121
- **Command:** `bash run_benchmark.sh --smoke --device-id 0 --block-size 256 --array-size 67108864 --warmup-iters 1 --num-iterations 20`

| # | Metric | Result |
|---|---|---|
| 1 | Copy bandwidth (bandwidth_gb_s_copy) | 3296.938935 |
| 2 | Mul bandwidth (bandwidth_gb_s_mul) | 3294.689202 |
| 3 | Add bandwidth (bandwidth_gb_s_add) | 3626.669931 |
| 4 | Triad bandwidth (bandwidth_gb_s_triad) | 3626.146995 |
| 5 | Dot bandwidth (bandwidth_gb_s_dot) | 2620.907833 |
<!-- /profile:smoke -->
