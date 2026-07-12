# 最终技术路线总结

## 最终系统分层

```text
官方 SimulationApiPort
  -> get_driver_status / query_cargo / query_decision_history / model_chat_completion
  -> HybridPolicy
  -> Preference compiler
  -> Driver progress ledger
  -> ServiceNode / ServicePlan
  -> take_order / wait / reposition
```

## 有复用价值的模块

### 偏好编译器

路径：`src/preferences/`

价值：

- 把偏好拆成 `time_window_task`、`location_task`、`quantity_goal`、`carryover_goal`、`quantity_limit`、`avoidance_rule`、`score_rule`、`advisory`。
- 用 ledger 表达“已完成多少、还差多少、是否超限”。
- 用 Rule DSL 把偏好转成可执行 price delta、resource requirement 和 trace。

问题：

- hidden preference 覆盖不足。
- LLM 输出与本地规则的冲突合并过复杂。
- 后期功能堆叠太快，平台反馈不足。

建议：

- 以后先把 IR 层稳定下来，再接 runtime。
- 每个 effect family 都要有 synthetic hidden-style 测试。
- LLM 只输出语义字段，禁止输出最终 rule id、metric key 和动作。

### ServicePlan

路径：`src/planning/service_node.py`、`src/planning/service_plan_optimizer.py`

价值：

- 统一真实货源、等待、空驶和偏好虚拟任务。
- 允许多个服务节点形成短 horizon 路线。
- 支持 resource requirement，避免同一目标在一个 plan 内重复加分。

问题：

- 路线搜索仍偏启发式，不是完整优化器。
- 目标压力和高毛利之间的平衡依赖若干默认参数。
- 计划层对 hidden 偏好错误非常敏感；解析错了，优化越强越会放大错误。

建议：

- 先保证偏好约束正确，再提高 plan aggressiveness。
- 对每个计划输出分解：毛利、距离成本、偏好收益/风险、目标压力。

### 参数实验 runner

路径：`scripts/run_parameter_experiments.py`

价值：

- 能自动跑参数组合并输出 `summary.csv`、`leaderboard.csv`、`best_trial.json`。
- 避免手工调参记录混乱。

问题：

- 本地 demo 参数最优不一定平台最优。
- 部分参数早期没有真正接入 runtime，出现过 unsupported 参数误读风险。

建议：

- runner 必须记录 unsupported params。
- 本地最好只能作为候选，不作为平台泛化证明。

## 失败链路

最终失败链路可以概括为：

```text
隐藏自然语言偏好
  -> LLM/local parser 未稳定覆盖
  -> canonical DSL 不完整或错误
  -> ledger/runtime 无法正确赋分
  -> ServicePlan 追错目标或漏目标
  -> 平台高偏好罚分
  -> 本地高净利无法转化为平台高分
```

## 重要负经验

### 不要用本地公开罚分低证明 hidden 泛化强

本地 `preference_penalty=3000/8000` 并不代表隐藏集能低罚分。平台 `45300/168300/208300` 已证明公开 demo 覆盖不足。

### 不要让 verifier 全量重写

LLM verifier 可能修正错误，也可能引入过度解释。更合理的方式是 critical-missing-only verifier：只有 source coverage 缺关键义务、dry-run 不可执行、local/model 冲突时才触发。

### 不要把执行压力当成解析修复

V5 的 goal pressure high-profit 是合理的执行层实验，但它只能解决“解析对了但没完成”的问题。如果解析错了，执行压力会加速错误。

## 后续研究方向

1. 自然语言偏好编译器 benchmark。
2. Preference IR 到 executable DSL 的可验证转换。
3. 在线决策中约束、目标、收益的统一资源账本。
4. 多 LLM consensus 的低频偏好解析，而不是每步动作 LLM。
5. 用 paraphrase 和 adversarial preference 生成器做 hidden-style 泛化测试。
