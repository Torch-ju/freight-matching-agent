# 清理报告

## 清理原则

1. 保留代码、官方数据、参考文献和关键提交包。
2. 删除本地运行生成物、重复中间包、pytest 临时目录和 scratch。
3. 删除含 key/API/RAM 字样的本地敏感文件。
4. 不修改官方 `demo/server`、`demo/simkit`、`demo/calc_monthly_income.py`。
5. 删除前确认目标路径位于项目根目录。

## 清理前主要体量

| 路径 | 文件数 | 目录数 | 体量 |
| --- | ---: | ---: | ---: |
| `demo/results` | 1720 | 311 | 9432.62 MB |
| `outputs` | 794 | 155 | 3785.60 MB |
| `scratch` | 9877 | 1754 | 11468.28 MB |
| `data` | 179 | 40 | 2161.97 MB |
| `Reference` | 1117 | 53 | 454.70 MB |
| `dist` | 145 | 8 | 16.47 MB |
| `memory-bank` | 1147 | 214 | 16.54 MB |

## 本次计划删除

- `demo/results/`
- `outputs/`
- `scratch/`
- 根目录 `.pytest_tmp_*`
- `.pytest_cache`
- `.tmp`
- `__pycache__`
- 根目录本地日志和 latest trace/profile 文件
- 根目录重复解压包与重复 zip
- `dist/submission/`
- `dist/` 中非 curated list 的 zip
- `docs/满帮AI-apiKey-5535083.csv`
- `Reference/钟佩芸的API RAM 账户.txt`
- `Reference/默认业务空间-apiKey-5548958.csv`

## 清理后状态

### 清理结果

- `demo/results/` 已删除
- `outputs/` 已删除
- `scratch/` 已删除
- 根目录所有 `.pytest_tmp_*`、`.pytest_cache`、`.tmp`、`__pycache__` 已删除
- 根目录本地 trace/log 和重复解压产物已删除
- `memory-bank/version-archive/` 已删除
- `dist/submission/` 已删除
- 根目录重复/中间 zip 已删除，仅保留 curated package 列表
- `docs/满帮AI-apiKey-5535083.csv` 已删除
- `Reference/钟佩芸的API RAM 账户.txt` 已删除
- `Reference/默认业务空间-apiKey-5548958.csv` 已删除

### 清理后体量

| 路径 | 文件数 | 目录数 | 体量 |
| --- | ---: | ---: | ---: |
| `demo/results` | 0 | 0 | 0 MB |
| `outputs` | 0 | 0 | 0 MB |
| `scratch` | 0 | 0 | 0 MB |
| `dist` | 13 | 0 | 2.16 MB |
| `data` | 179 | 40 | 2161.97 MB |
| `Reference` | 1115 | 53 | 454.70 MB |
| `memory-bank` | 60 | 2 | 1.19 MB |

## 二次数据瘦身（2026-06-24）

用户确认后，继续删除已确认重复或可外部复原的大文件：

- `data/data/20260608_cargo_dataset.jsonl`
- `data/demo_docs_release_20260608/demo/server/data/cargo_dataset.jsonl`
- `data/data/20260529_cargo_dataset.jsonl`
- `data/demo_docs_release_20260529/demo/server/data/cargo_dataset.jsonl`
- `data/data/20260509_cargo_dataset.jsonl`
- `data/demo_docs_release_20260509/demo/server/data/cargo_dataset.jsonl`
- `data/demo_docs_release_20260608.zip`
- `data/demo_docs_release_20260529.zip`
- `data/demo_docs_release_20260509.zip`

删除前已用 SHA256 抽查确认同版本 cargo 文件为重复副本。删除文件数 `9`，释放约 `2111.33 MB`。

二次瘦身后主要体量：

| 路径 | 体量 |
| --- | ---: |
| `.git` | 823.76 MB |
| `demo` | 600.47 MB |
| `Reference` | 454.70 MB |
| `data` | 50.54 MB |
| `dist` | 2.97 MB |

保留：

- `demo/server/data/cargo_dataset.jsonl`：当前 20260608 本地仿真运行副本。
- `data/司机偏好数据汇总/`：偏好泛化研究和合成测试素材。
- `Reference/`：参考文献目录。
- `.git/`：Git 历史和回溯能力。

### 保留的关键 zip

- `C_initial_upload_with_results_calendar_or_20260607.zip`
- `manbang_agent_route_b_official_rules_20260606_194447.zip`
- `manbang_agent_time_efficiency_near_score_freeze_20260615_232900.zip`
- `manbang_agent_submission_20260616_031414.zip`
- `manbang_agent_submission_20260616_085755.zip`
- `manbang_agent_submission_20260616_101311.zip`
- `manbang_agent_compiler_v2_timeout_guard_upload_local114856_20260616_214629.zip`
- `manbang_agent_compiler_v2_verifier_off_ablation_20260616_235000.zip`
- `manbang_agent_aggressive_v1_compiler_v2_verifier_off_20260617_000000.zip`
- `manbang_agent_aggressive_v2_local_runtime_ready_first_20260617_004326.zip`
- `manbang_agent_aggressive_v3_critical_verifier_20260617_005304.zip`
- `manbang_agent_aggressive_v4_dual_extractor_consensus_20260617_010206.zip`
- `manbang_agent_aggressive_v5_goal_pressure_high_profit_20260617_012028.zip`

### 复核结论

- 敏感文件名已从原始位置删除。
- 现存 `apiKey` 命中仅来自复盘/研究文档中的历史示例和说明，不是落盘密钥。
- 项目已从“大量冲榜残留”收敛到“代码 + 官方数据 + 参考文献 + 少量关键包 + 复盘文档”的状态。

### 验证

```text
D:\Anaconda\python.exe -m compileall -q src main.py demo\agent tests
passed

D:\Anaconda\python.exe -m pytest tests -q --basetemp=.tmp\pytest_final_review
301 passed, 2 skipped in 2.44s
```

其中 2 个 skipped 是 20260529 旧口径切换测试；赛后瘦身已删除历史大货源文件，测试在缺少旧数据时跳过。测试结束后，`.tmp`、`.pytest_cache` 和 `__pycache__` 已再次清理。
