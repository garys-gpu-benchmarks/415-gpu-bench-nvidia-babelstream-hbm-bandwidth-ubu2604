# SPEC.md: "The Human How"; Exact technical requirements, environment setup, implementation details, etc.

## Execution Description

Builds src/babelstream.cu (FP64 device arrays) and runs scripts/collect_babelstream.py. device_id, array_size, block_size, warmup_iters, and num_iterations come from yaml. dtype is recorded in CSV but the CUDA kernel always uses double. kernels Copy/Mul/Add/Triad/Dot all run; there is no per-kernel time or percent-of-peak column Sweep dimensions: device_id, dtype, block_size, array_size, kernels, warmup_iters, num_iterations, output_format.

## Parameters

| Parameter | CLI Flag | Tested Values | Default | Description |
| --- | --- | --- | --- | --- |
| device_id | `--device-id` | smoke=0, baseline=0, extended=0 | 0 | From Parameter list; see Execution Description With Parameters. |
| dtype | `--dtype` | smoke=FP64, baseline=FP64, extended=FP64 | FP64 | From Parameter list; see Execution Description With Parameters. |
| block_size | `--block-size` | smoke=256, baseline=256, extended=256 | 256 | From Parameter list; see Execution Description With Parameters. |
| array_size | `--array-size` | smoke=1048576, baseline=268435456, extended=536870912 | 268435456 | From Parameter list; see Execution Description With Parameters. |
| kernels | `--kernels` | smoke=Copy,Mul,Add,Triad,Dot, baseline=Copy,Mul,Add,Triad,Dot, extended=Copy,Mul,Add,Triad,Dot | Copy,Mul,Add,Triad,Dot | From Parameter list; see Execution Description With Parameters. |
| warmup_iters | `--warmup-iters` | smoke=1, baseline=2, extended=5 | 2 | From Parameter list; see Execution Description With Parameters. |
| num_iterations | `--num-iterations` | smoke=2, baseline=30000, extended=35550 | 30000 | From Parameter list; see Execution Description With Parameters. |
| output_format | `--output-format` | smoke=csv, baseline=csv, extended=csv | csv | From Parameter list; see Execution Description With Parameters. |

## Invocation

```bash
Compile babelstream.cu with nvcc; run bin/babelstream via collect_babelstream.py
```

## Raw Output Format

BabelStream stdout parsed into raw_results.csv. Each kernel row and the summary row carry all five bandwidth columns

check,device_id,array_size,dtype,block_size,status,bandwidth_gb_s_copy,bandwidth_gb_s_mul,bandwidth_gb_s_add,bandwidth_gb_s_triad,bandwidth_gb_s_dot
Copy,0,16777216,fp64,256,ok,4200,4100,4300,4250,3000

## Metrics

- **#1: Copy bandwidth** — stored as `bandwidth_gb_s_copy`.
- **#2: Mul bandwidth** — stored as `bandwidth_gb_s_mul`.
- **#3: Add bandwidth** — stored as `bandwidth_gb_s_add`.
- **#4: Triad bandwidth** — stored as `bandwidth_gb_s_triad`.
- **#5: Dot bandwidth** — stored as `bandwidth_gb_s_dot`.

## Framework

Builds src/babelstream.cu (FP64 device arrays) and runs scripts/collect_babelstream.py. device_id, array_size, block_size, warmup_iters, and num_iterations come from yaml. dtype is recorded in CSV but the CUDA kernel always uses double.

## Installation and Execution Summary

Compile src/babelstream.cu with nvcc and run bin/babelstream once over FP64 device arrays, parse Copy/Mul/Add/Triad/Dot bandwidth lines, and replicate those five values onto kernel-labeled CSV rows, to measure HBM bandwidth. yaml dtype is recorded but does not switch the kernel off FP64

## Platform Portability

- **AMD (primary):** ```bash
Compile babelstream.cu with nvcc; run bin/babelstream via collect_babelstream.py
```
- **NVIDIA:** Native NVIDIA CUDA workload. Execute on the stated Ubuntu release with the host NVIDIA driver and CUDA userspace. ROCm porting notes do not apply.

## Model Context Protocols

- **Active:** None

## Execution-Loop Validation Contract

EXECUTION CHAIN: `run_benchmark.sh` ➔ raw output ➔ `scripts/parse_results.py` ➔ `results/benchmark.db` ➔ `scripts/validate_results.py`

This benchmark uses a lightweight, SQLite-integrated execution loop for result validation. All validation is performed by `scripts/validate_results.py`.

### Validation script usage

```bash
export BENCHMARK_PYTHON=/usr/bin/python3.13  # optional; select the installed interpreter

# After a live run:
".venv/bin/python" scripts/validate_results.py --db results/benchmark.db

# CI / no-GPU path (seeds fixture and validates it):
".venv/bin/python" scripts/validate_results.py --seed-fixture --quiet

# Override DB path via environment variable:
BENCHMARK_DB=tests/fixtures/benchmark.db \
  ".venv/bin/python" scripts/validate_results.py
```

### Run artifact contract

BabelStream stdout parsed into raw_results.csv. Each kernel row and the summary row carry all five bandwidth columns

check,device_id,array_size,dtype,block_size,status,bandwidth_gb_s_copy,bandwidth_gb_s_mul,bandwidth_gb_s_add,bandwidth_gb_s_triad,bandwidth_gb_s_dot
Copy,0,16777216,fp64,256,ok,4200,4100,4300,4250,3000

```bash
bash run_benchmark.sh --help
bash run_benchmark.sh --profile smoke --validate
bash run_benchmark.sh --profile baseline --validate
bash run_benchmark.sh --profile extended --validate
```
`run_benchmark.sh --help` prints usage and exits. The harness calls `scripts/ensure_setup.sh` when `.setup_state` is absent.

### Required integrity checks (built into `validate_results.py`)

1. Latest run exists and `runs.status = 'ok'`.
2. `run.error_message` is NULL.
3. `started_at` and `finished_at` are valid ISO-8601 UTC strings.
4. All required aggregate metrics in `runs` are non-NULL and finite.
5. All required aggregate metrics are physically sensible (positive values). Builds src/babelstream.cu (FP64 device arrays) and runs scripts/collect_babelstream.py. device_id, array_size, block_size, warmup_iters, and num_iterations come from yaml. dtype is recorded in CSV but the CUDA kernel always uses double.
6. At least 2 sample rows exist for the latest `run_id` (sweep coverage).
7. No sample has `status = 'error'`.
8. Builds src/babelstream.cu (FP64 device arrays) and runs scripts/collect_babelstream.py. device_id, array_size, block_size, warmup_iters, and num_iterations come from yaml. dtype is recorded in CSV but the CUDA kernel always uses double.

### Baseline / Threshold configuration (`config/benchmark_config.yaml`)

Expected ranges and gates live in `config/benchmark_config.yaml` under `baselines:` or `thresholds:`. To update them, edit that file — never edit validation code directly.

Threshold key suffixes encode comparison direction when `thresholds:` is present: `_min` → observed value must be ≥ threshold. `_max` → observed value must be ≤ threshold. Informational `baselines:` ranges are not pass/fail gates.
