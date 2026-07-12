# 数据集与产物清单

## 应保留的数据资产

### 官方赛题数据

路径：

- `data/demo_docs_release_20260509/`
- `data/demo_docs_release_20260529/`
- `data/demo_docs_release_20260608/`
- `demo/server/data/`：保留当前 20260608 本地运行所需数据副本

用途：

- 官方规则、接口、demo server 和必要公开数据版本存档。
- 后续研究复现实验口径。

处理结论：

- 保留展开后的官方资料目录和当前本地运行数据。
- 赛后清理已删除 release zip 和重复 cargo 数据副本，避免同一大文件多处占用磁盘。
- 历史 20260509/20260529 大货源文件已删除；如需完整复原旧公开包，应从原始发布包或外部归档重新获取。

### 司机偏好公开汇总

路径：

- `data/司机偏好数据汇总/`

用途：

- 只用于开发期归纳通用 effect family 和合成测试。
- 禁止在 `src/` 或 `demo/agent/` 运行时读取。

处理结论：保留。

### 参考文献

路径：

- `Reference/`

用途：

- 偏好理解、自然语言优化、司机-订单匹配、动态调度和在线评估研究素材。

处理结论：保留文献目录；删除本地 key/API/RAM 账户文件。

## 应保留的提交包

`dist/` 中只建议保留这些包：

| 包 | 意义 |
| --- | --- |
| `manbang_agent_route_b_official_rules_20260606_194447.zip` | 早期平台已知最好锚点 |
| `C_initial_upload_with_results_calendar_or_20260607.zip` | 20260607 本地主线锚点 |
| `manbang_agent_time_efficiency_near_score_freeze_20260615_232900.zip` | 2026-06-15 23:43 平台最好对应线 |
| `manbang_agent_submission_20260616_085755.zip` | 回滚到平台最好代码线 |
| `manbang_agent_submission_20260616_101311.zip` | 平台最好线 + trial_006 查询参数 |
| `manbang_agent_submission_20260616_031414.zip` | compiler 高罚分负例包 |
| `manbang_agent_compiler_v2_timeout_guard_upload_local114856_20260616_214629.zip` | 本地 114856、平台 6309 的关键对照包 |
| `manbang_agent_compiler_v2_verifier_off_ablation_20260616_235000.zip` | verifier-off ablation |
| `manbang_agent_aggressive_v1_compiler_v2_verifier_off_20260617_000000.zip` | 最后五包 V1 |
| `manbang_agent_aggressive_v2_local_runtime_ready_first_20260617_004326.zip` | 最后五包 V2 |
| `manbang_agent_aggressive_v3_critical_verifier_20260617_005304.zip` | 最后五包 V3 |
| `manbang_agent_aggressive_v4_dual_extractor_consensus_20260617_010206.zip` | 最后五包 V4 |
| `manbang_agent_aggressive_v5_goal_pressure_high_profit_20260617_012028.zip` | 最后五包 V5 |

其余时间戳 zip 基本是中间构建，可删除。

## 可删除的生成产物

### 本地仿真结果

路径：`demo/results/`

赛后价值：

- 体量巨大。
- 关键结果已写入复盘文档。
- 后续如需重新分析，应重新运行或从保留包复现。

处理结论：删除。

### 参数实验输出

路径：`outputs/`

关键保留信息：

```json
{
  "trial_id": "trial_006",
  "net_income": 108923.34,
  "gross_income": 156019.89,
  "cost": 44096.55,
  "distance_km": 29397.7,
  "preference_penalty": 3000.0,
  "total_tokens": 65725,
  "MANBANG_CARGO_QUERY_BATCH_K": "40",
  "MANBANG_CARGO_QUERY_EXTRA_BATCH_K": "50",
  "MANBANG_CARGO_QUERY_MAX_EXTRA_BATCHES": "60",
  "MANBANG_CARGO_QUERY_MIN_SLACK_MINUTES": "10"
}
```

处理结论：删除原始输出目录，保留上面的摘要。

### scratch

路径：`scratch/`

用途：历史实验、临时恢复、旧 artifact 和中间分析。

处理结论：删除。关键结论已进入 `memory-bank/` 和本目录复盘文档。

### 重复大货源数据

路径：

- `data/data/20260608_cargo_dataset.jsonl`
- `data/demo_docs_release_20260608/demo/server/data/cargo_dataset.jsonl`
- `data/data/20260529_cargo_dataset.jsonl`
- `data/demo_docs_release_20260529/demo/server/data/cargo_dataset.jsonl`
- `data/data/20260509_cargo_dataset.jsonl`
- `data/demo_docs_release_20260509/demo/server/data/cargo_dataset.jsonl`
- `data/demo_docs_release_20260608.zip`
- `data/demo_docs_release_20260529.zip`
- `data/demo_docs_release_20260509.zip`

处理结论：已删除，释放约 `2111.33 MB`。当前保留 `demo/server/data/cargo_dataset.jsonl` 作为 20260608 本地运行数据副本。

### pytest 临时目录

路径：根目录 `.pytest_tmp_*`、`.pytest_cache`、`.tmp`

处理结论：删除。

## 不应删除的代码资产

- `src/`
- `demo/agent/`
- `tests/`
- `scripts/`
- `docs/docs/`
- `docs/superpowers/skills/manbang-preference-generalization/`
- `main.py`
- `README.md`
- `AGENTS.md`

这些文件仍是项目可运行、可研究、可复盘的核心。
