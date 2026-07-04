# Freight Matching Agent

> Public-safe case study for an Agentic AI prototype in continuous freight-searching and logistics decision support.

## Interviewer Quick Read

This repository is not a raw code dump and not a production-system claim. It is a desensitized project write-up showing how I think about logistics Agent design:

- **Scenario:** continuous freight-searching in freight platform workflows.
- **Result:** Top 24 / 963, finalist award.
- **Core capability shown:** converting logistics tasks into agent state, tool-use steps, candidate evaluation, explanation, and human confirmation.
- **Positioning:** AI Agent + operations research + logistics decision intelligence.
- **Disclosure boundary:** no private competition data, no partner data, no hidden API keys, no personal contact information.

Official competition page: https://tianchi.aliyun.com/competition/entrance/532467/information

## Why This Problem Matters

Continuous freight-searching is a repeated decision problem under changing supply-demand information. A useful assistant should not only chat with users; it should help structure the decision process:

- identify what the user is trying to optimize;
- retrieve or reason over candidate freight information;
- compare options under business constraints;
- explain trade-offs in a way humans can verify;
- keep human confirmation in the loop before final action.

This is where my logistics and operations-research background is relevant. The Agent should not be presented as a generic LLM wrapper. It should behave like a workflow layer for logistics decisions.

## Public-Safe Agent Workflow

```text
User request
  -> intent recognition
  -> task decomposition
  -> state tracking
  -> tool / data query
  -> candidate generation
  -> rule-based or model-assisted evaluation
  -> explanation of trade-offs
  -> human confirmation
```

## What This Demonstrates

| Dimension | Public evidence |
|---|---|
| Logistics scenario understanding | continuous freight-searching, freight-matching objectives, repeated decision flow |
| Agent product thinking | task decomposition, state tracking, tool-use concept, result validation |
| OR-style decision thinking | candidate comparison, constraint awareness, trade-off explanation |
| Public communication | desensitized README, resume-ready summary, disclosure boundary |
| Competition signal | Top 24 / 963, finalist award |

## Current Public Contribution Scope

The public version uses conservative wording until screenshots and detailed responsibility boundaries are confirmed.

- Logistics scenario analysis and user workflow decomposition.
- Agent workflow design for continuous freight-searching tasks.
- Prompt and interaction design for task decomposition and result explanation.
- Demo organization and presentation materials.
- Public case-study writing with data and privacy boundaries.

## Demo Assets To Add

Add only sanitized screenshots or diagrams:

```text
assets/demo-home.png
assets/demo-workflow.png
assets/demo-result.png
assets/ranking-proof.png
```

Recommended sequence:

1. task input screen with private data removed;
2. workflow / state transition diagram;
3. final recommendation or explanation screen with synthetic examples;
4. ranking certificate or competition result screenshot.

## Tech Stack

Public technical details are intentionally limited until the team confirms what can be disclosed.

- LLM / Agent platform: to be documented after public-disclosure review.
- Backend / tools: to be documented after public-disclosure review.
- Frontend / demo: to be documented after public-disclosure review.
- Data: public, synthetic, or desensitized materials only.

## Privacy Boundary

This repository will not include:

- private competition data;
- business data or partner information;
- personal phone number, WeChat, or private email;
- API keys, tokens, cookies, or model-service credentials;
- claims that the prototype was a production system unless evidence is later approved.

## Resume Summary

中文简历保守版：

> 围绕连续找货场景，参与设计包含任务拆解、状态跟踪、工具调用和结果校验的 Agentic AI 原型，在满帮相关比赛中获得 24/963、入围奖。

英文简历保守版：

> Designed a public-safe case study for an Agentic AI prototype in continuous freight-searching, focusing on task decomposition, state tracking, tool-use workflow, result validation, and human-in-the-loop logistics decision support; finalist award, Top 24 / 963.

## What Still Needs Confirmation

- My exact responsibility split across requirements, prompt, workflow, frontend/backend, data, and presentation.
- Which demo screenshots can be publicly shown.
- Which model/platform/tool details are safe to disclose.
- Whether ranking proof can be added as an image.

## Roadmap

- [ ] Add sanitized workflow diagram.
- [ ] Add public-safe demo screenshots.
- [ ] Add ranking proof screenshot.
- [ ] Add confirmed tech stack after disclosure review.
- [ ] Add a short Chinese case-study section for recruiters.
