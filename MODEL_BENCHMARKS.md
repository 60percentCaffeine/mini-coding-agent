# Model Benchmark Results

Human TL;DR:

- openai/gpt-chat-latest is the fastest at 3.4s and pretty capable, but most expensive ($0.012 for 1 prompt)
- other models are cheaper but 2x+ slower

---

Date: 2026-06-19

Benchmark prompt:

> How many files are there in this folder

Workspace: `/root/mini-coding-agent on iSH`

Conditions:

- Agent: `mini-coding-agent`
- API: OpenRouter chat completions
- `max_steps=0` (unlimited)
- `max_new_tokens=0` (unset)
- Each successful run made 2 model calls and 1 tool call.
- Cost is the sum of OpenRouter `usage.cost` values reported on each model call.
- “off” means the `reasoning` request field was omitted.

## Summary, sorted by wall time

| Rank | Model | Reasoning | Time | Cost | Reasoning tokens | Total tokens |
|---:|---|---:|---:|---:|---:|---:|
| 1 | `openai/gpt-chat-latest` | xhigh | 3.39s | $0.012106 | 0 | 2823 |
| 2 | `qwen/qwen3.5-397b-a17b` | minimal | 6.73s | $0.002019 | 35 | 3209 |
| 3 | `deepseek/deepseek-v4-flash` | off | 7.21s | $0.000425 | 125 | 2960 |
| 4 | `qwen/qwen3.7-plus` | minimal | 9.77s | $0.001368 | 226 | 3276 |
| 5 | `qwen/qwen3.7-max` | off | 9.79s | $0.004942 | 230 | 3280 |
| 6 | `qwen/qwen3.7-max` | xhigh | 10.31s | $0.004913 | 222 | 3272 |
| 7 | `qwen/qwen3.7-plus` | off | 10.60s | $0.001436 | 279 | 3329 |
| 8 | `deepseek/deepseek-v4-flash` | minimal | 12.12s | $0.000385 | 763 | 3630 |
| 9 | `qwen/qwen3.7-plus` | xhigh | 12.17s | $0.001504 | 332 | 3382 |
| 10 | `deepseek/deepseek-v4-pro` | off | 12.84s | $0.002911 | 319 | 3177 |
| 11 | `deepseek/deepseek-v4-flash` | xhigh | 13.09s | $0.000398 | 1030 | 3952 |
| 12 | `deepseek/deepseek-v4-pro` | minimal | 13.55s | $0.006437 | 464 | 3279 |
| 13 | `qwen/qwen3.5-397b-a17b` | off | 13.93s | $0.002221 | 158 | 3196 |
| 14 | `qwen/qwen3.7-max` | minimal | 14.09s | $0.005918 | 471 | 3540 |
| 15 | `~openai/gpt-mini-latest` | xhigh | 15.24s | $0.006410 | 915 | 3671 |
| 16 | `qwen/qwen3.5-397b-a17b` | xhigh | 45.42s | $0.002518 | 160 | 3200 |

## Full results

| Model | Label | Reasoning | Time | Cost | Prompt tokens | Completion tokens | Total tokens | Reasoning tokens | Cached tokens | Tool | Answer |
|---|---|---:|---:|---:|---:|---:|---:|---:|---:|---|---|
| `deepseek/deepseek-v4-flash` | previous default config | xhigh | 13.09s | $0.000398 | 2860 | 1092 | 3952 | 1030 | 1244 | run_shell | There are 7 files in the current folder (root of the workspace). |
| `deepseek/deepseek-v4-flash` | DeepSeek V4 Flash | off | 7.21s | $0.000425 | 2792 | 168 | 2960 | 125 | 0 | list_files | There are 7 files in this folder. |
| `deepseek/deepseek-v4-flash` | DeepSeek V4 Flash | minimal | 12.12s | $0.000385 | 2792 | 838 | 3630 | 763 | 678 | list_files | There are 7 files in this folder (and 4 subdirectories). The files are: .gitignore, EXAMPLE.md, install.sh, LICENSE, mini_coding_agent.py... |
| `deepseek/deepseek-v4-pro` | DeepSeek V4 Pro | off | 12.84s | $0.002911 | 2792 | 385 | 3177 | 319 | 0 | list_files | There are 7 files in the root folder: .gitignore, EXAMPLE.md, install.sh, LICENSE, mini_coding_agent.py, pyproject.toml, and README.md. |
| `deepseek/deepseek-v4-pro` | DeepSeek V4 Pro | minimal | 13.55s | $0.006437 | 2792 | 487 | 3279 | 464 | 0 | list_files | There are 7 files in the workspace root (plus 4 directories). |
| `openai/gpt-chat-latest` | OpenAI GPT Chat Latest | xhigh | 3.39s | $0.012106 | 2696 | 127 | 2823 | 0 | 1152 | list_files | There are 7 files in the folder shown: - .gitignore - EXAMPLE.md - install.sh - LICENSE - mini_coding_agent.py - pyproject.toml - README.... |
| `qwen/qwen3.5-397b-a17b` | Qwen3.5 397B A17B (Reasoning) | xhigh | 45.42s | $0.002518 | 2943 | 257 | 3200 | 160 | 0 | list_files | There are 7 files in this folder: - .gitignore - EXAMPLE.md - install.sh - LICENSE - mini_coding_agent.py - pyproject.toml - README.md (P... |
| `qwen/qwen3.5-397b-a17b` | Qwen3.5 397B A17B | off | 13.93s | $0.002221 | 2943 | 253 | 3196 | 158 | 0 | list_files | There are 7 files in this folder: 1. .gitignore 2. EXAMPLE.md 3. install.sh 4. LICENSE 5. mini_coding_agent.py 6. pyproject.toml 7. READM... |
| `qwen/qwen3.5-397b-a17b` | Qwen3.5 397B A17B | minimal | 6.73s | $0.002019 | 2943 | 266 | 3209 | 35 | 1536 | list_files | There are 7 files in this folder (not counting directories): 1. .gitignore 2. EXAMPLE.md 3. install.sh 4. LICENSE 5. mini_coding_agent.py... |
| `qwen/qwen3.7-max` | Qwen3.7 Max | xhigh | 10.31s | $0.004913 | 2943 | 329 | 3272 | 222 | 0 | list_files | There are 7 files in this folder: 1. .gitignore 2. EXAMPLE.md 3. install.sh 4. LICENSE 5. mini_coding_agent.py 6. pyproject.toml 7. READM... |
| `qwen/qwen3.7-max` | Qwen3.7 Max | off | 9.79s | $0.004942 | 2943 | 337 | 3280 | 230 | 0 | list_files | There are 7 files in this folder: 1. .gitignore 2. EXAMPLE.md 3. install.sh 4. LICENSE 5. mini_coding_agent.py 6. pyproject.toml 7. READM... |
| `qwen/qwen3.7-max` | Qwen3.7 Max | minimal | 14.09s | $0.005918 | 2943 | 597 | 3540 | 471 | 0 | list_files | There are 7 files in this folder: 1. `.gitignore` 2. `EXAMPLE.md` 3. `install.sh` 4. `LICENSE` 5. `mini_coding_agent.py` 6. `pyproject.to... |
| `qwen/qwen3.7-plus` | Qwen3.7 Plus | xhigh | 12.17s | $0.001504 | 2943 | 439 | 3382 | 332 | 0 | list_files | There are 7 files in this folder: 1. .gitignore 2. EXAMPLE.md 3. install.sh 4. LICENSE 5. mini_coding_agent.py 6. pyproject.toml 7. READM... |
| `qwen/qwen3.7-plus` | Qwen3.7 Plus | off | 10.60s | $0.001436 | 2943 | 386 | 3329 | 279 | 0 | list_files | There are 7 files in this folder: 1. .gitignore 2. EXAMPLE.md 3. install.sh 4. LICENSE 5. mini_coding_agent.py 6. pyproject.toml 7. READM... |
| `qwen/qwen3.7-plus` | Qwen3.7 Plus | minimal | 9.77s | $0.001368 | 2943 | 333 | 3276 | 226 | 0 | list_files | There are 7 files in this folder: 1. .gitignore 2. EXAMPLE.md 3. install.sh 4. LICENSE 5. mini_coding_agent.py 6. pyproject.toml 7. READM... |
| `~openai/gpt-mini-latest` | OpenAI GPT Mini Latest | xhigh | 15.24s | $0.006410 | 2696 | 975 | 3671 | 915 | 0 | list_files | There are 7 files in the folder. |

## Per-model comparison

### `deepseek/deepseek-v4-flash`

| Reasoning | Time | Cost | Reasoning tokens | Notes |
|---:|---:|---:|---:|---|
| xhigh | 13.09s | $0.000398 | 1030 | previous baseline |
| off | 7.21s | $0.000425 | 125 | vs xhigh: -5.88s, +$0.000027 |
| minimal | 12.12s | $0.000385 | 763 | vs xhigh: -0.97s, -$0.000013 |

### `deepseek/deepseek-v4-pro`

| Reasoning | Time | Cost | Reasoning tokens | Notes |
|---:|---:|---:|---:|---|
| off | 12.84s | $0.002911 | 319 |  |
| minimal | 13.55s | $0.006437 | 464 |  |

### `openai/gpt-chat-latest`

| Reasoning | Time | Cost | Reasoning tokens | Notes |
|---:|---:|---:|---:|---|
| xhigh | 3.39s | $0.012106 | 0 | previous baseline |

### `qwen/qwen3.5-397b-a17b`

| Reasoning | Time | Cost | Reasoning tokens | Notes |
|---:|---:|---:|---:|---|
| xhigh | 45.42s | $0.002518 | 160 | previous baseline |
| off | 13.93s | $0.002221 | 158 | vs xhigh: -31.48s, -$0.000297 |
| minimal | 6.73s | $0.002019 | 35 | vs xhigh: -38.69s, -$0.000500 |

### `qwen/qwen3.7-max`

| Reasoning | Time | Cost | Reasoning tokens | Notes |
|---:|---:|---:|---:|---|
| xhigh | 10.31s | $0.004913 | 222 | previous baseline |
| off | 9.79s | $0.004942 | 230 | vs xhigh: -0.52s, +$0.000030 |
| minimal | 14.09s | $0.005918 | 471 | vs xhigh: +3.78s, +$0.001005 |

### `qwen/qwen3.7-plus`

| Reasoning | Time | Cost | Reasoning tokens | Notes |
|---:|---:|---:|---:|---|
| xhigh | 12.17s | $0.001504 | 332 | previous baseline |
| off | 10.60s | $0.001436 | 279 | vs xhigh: -1.57s, -$0.000068 |
| minimal | 9.77s | $0.001368 | 226 | vs xhigh: -2.40s, -$0.000136 |

### `~openai/gpt-mini-latest`

| Reasoning | Time | Cost | Reasoning tokens | Notes |
|---:|---:|---:|---:|---|
| xhigh | 15.24s | $0.006410 | 915 | previous baseline |

## Observations

- Fastest overall in these runs: `openai/gpt-chat-latest` at 3.39s, but it was also the most expensive tested run at $0.012106.
- Best non-OpenAI speed observed: `qwen/qwen3.5-397b-a17b` with minimal reasoning at 6.73s and $0.002019.
- Best cheap fast option observed: `deepseek/deepseek-v4-flash` with reasoning off at 7.21s and $0.000425.
- The previous default config (`deepseek/deepseek-v4-flash` with xhigh reasoning) was cheap but slower: 13.09s and $0.000398.
- `~openai/gpt-mini-latest` under xhigh reasoning was slower than expected because it spent many tokens on reasoning.

## Raw result files used

- `/tmp/mca_bench_results.json`
- `/tmp/mca_reasoning_bench_results.json`
