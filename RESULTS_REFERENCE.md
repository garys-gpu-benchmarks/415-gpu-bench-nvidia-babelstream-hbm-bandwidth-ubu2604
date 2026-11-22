# Results: 415 BabelStream HBM Bandwidth

**Main goal:** Measure sustained BabelStream HBM bandwidth  
**Tools:** Compile babelstream.cu with nvcc; run bin/babelstream via collect_babelstream.py

Reference results from the validation run on the system shown in each section (recorded 2026-11-22). Your own runs write `results/RESULTS_ACTUAL.md` in the same format.

> Smoke runs use deliberately small sizes. They check that the workload installs and runs end to end; their numbers are not performance results. Baseline and extended are.

<!-- profile:smoke -->
## smoke

- **System:** 1× NVIDIA H100 80GB HBM3 (81559 MiB) · Intel(R) Xeon(R) Platinum 8468 · Ubuntu 26.04.1 LTS · kernel 6.8.0-149-generic · driver 595.112.07
- **Run:** 2026-11-22T11:14:18Z · status **PASS** (exit 0)
- **Time (mm:ss):** setup 00:38 · benchmark 00:01 · whole run 00:46
- **Source:** run 415_20261122_111418
- **Command:** `bash run_benchmark.sh --smoke --device-id 0 --block-size 256 --array-size 67108864 --warmup-iters 1 --num-iterations 20`

| # | Metric | Result |
|---|---|---|
| 1 | Copy bandwidth (bandwidth_gb_s_copy) | 2916.35654 |
| 2 | Mul bandwidth (bandwidth_gb_s_mul) | 2915.216321 |
| 3 | Add bandwidth (bandwidth_gb_s_add) | 3103.654051 |
| 4 | Triad bandwidth (bandwidth_gb_s_triad) | 3105.741577 |
| 5 | Dot bandwidth (bandwidth_gb_s_dot) | 2793.258047 |
<!-- /profile:smoke -->
