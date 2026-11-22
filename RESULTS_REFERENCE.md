# Results: 415 BabelStream HBM Bandwidth

**Main goal:** Measure sustained BabelStream HBM bandwidth  
**Tools:** Compile babelstream.cu with nvcc; run bin/babelstream via collect_babelstream.py

Reference results from the validation run on the system shown in each section (recorded 2026-11-22). Your own runs write `results/RESULTS_ACTUAL.md` in the same format.

> Smoke runs use deliberately small sizes. They check that the workload installs and runs end to end; their numbers are not performance results. Baseline and extended are.

<!-- profile:smoke -->
## smoke

- **System:** 1× NVIDIA H100 80GB HBM3 (81559 MiB) · Intel(R) Xeon(R) Platinum 8468 · Ubuntu 26.04.1 LTS · kernel 6.8.0-149-generic · driver 595.112.07
- **Run:** 2026-11-22T14:41:54Z · status **PASS** (exit 0)
- **Time (mm:ss):** setup 01:03 · benchmark 00:02 · whole run 01:10
- **Source:** run 415_20261122_144154
- **Command:** `bash run_benchmark.sh --smoke --device-id 0 --block-size 256 --array-size 67108864 --warmup-iters 1 --num-iterations 20`

| # | Metric | Result |
|---|---|---|
| 1 | Copy bandwidth (bandwidth_gb_s_copy) | 2914.773169 |
| 2 | Mul bandwidth (bandwidth_gb_s_mul) | 2912.926072 |
| 3 | Add bandwidth (bandwidth_gb_s_add) | 3103.70182 |
| 4 | Triad bandwidth (bandwidth_gb_s_triad) | 3103.768842 |
| 5 | Dot bandwidth (bandwidth_gb_s_dot) | 2780.469832 |
<!-- /profile:smoke -->
