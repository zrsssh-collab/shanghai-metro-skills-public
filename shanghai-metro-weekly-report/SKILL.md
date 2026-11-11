---
name: shanghai-metro-weekly-report
description: Write concise Shanghai metro wireless-network weekly reports and one-page专题周报 from verified optimization evidence, preserving the requested reporting format and exact statistical口径.
---

# Shanghai Metro Weekly Report

Use this skill for weekly reports,专题周报, progress updates, and leadership-ready summaries of Shanghai metro wireless optimization. Do not use it for a full root-cause investigation unless the user also asks for complaint analysis.

## Default deliverable

Write in concise Chinese with a leadership-readable, low-AI tone. Prefer this compact one-page format:

1. **问题描述/问题背景**
2. **问题分析/排查情况**
3. **优化措施及效果/优化进展**
4. **后续计划**

Use short paragraphs, compact bullets, and exact line/section/station/cell names. Keep the report brief unless the user asks for a full report. Read [references/report-template.md](references/report-template.md) for the fill-in pattern.

## Working context and inputs

Use supplied project materials and verified examples when available. Common topics include PCI冲突、乒乓治理、高负荷/扩容、弱覆盖、跨场景CA、VoNR及专题材料。 Treat filenames and prior wording as reference, not as proof. Before writing, identify the reporting period, scope, source files, and missing evidence.

Minimum checklist:

- Reporting period, line/section/station, direction, work item and current status.
- Before/after values with identical statistical windows and denominators.
- Exact optimization action, owner/maintenance dependency, completion time and residual issue.
- Source report, workbook, signaling or road-test evidence; note missing or mismatched data.

If a value or closure status is unavailable, say so explicitly; never silently fill it from an older period.

## Writing rules

- Preserve the original statistical口径. Never combine different time windows, early/late busy periods, or incompatible definitions without labeling them.
- Use before→after values, delta or percentage-point change, and name the remaining risk. If conditions differ, state that the comparison needs same-condition revalidation.
- Replace vague “路段9—14” labels with actual section names when known. Flag inconsistent cell names or route ownership before finalizing.
- Describe optimization actions concretely: expansion, load balancing, RF/antenna adjustment, PCI, CIO/TTT, power, CA, maintenance repair, or construction dependency.
- Keep confirmed facts separate from interpretation. Do not claim closure when evidence only shows a temporary change or a plan.
- Use charts only when they clarify a before/after or section comparison. Keep one-page Word-style output compact when requested; default to black Microsoft YaHei text and clean tables.
- Mask IMSI, MSISDN and other personal identifiers in leadership output.

## Evidence and structure

Prefer exact signaling, KPI/KQI, road-test, configuration, and closure records over narrative summaries. Cite the source period beside key numbers. For technical topics, retain the user's established terms such as PRB, users, CQI, RSRP/SINR, TCP retransmission, VoNR, RRC rebuild, RAR Timeout, PCI, A3/A6/CIO/TTT.

## Final report template

**专题标题**

**问题描述/背景：** 时间、线路/路段、用户感知或指标异常。

**问题分析/排查情况：** 关键小区/场景、核心数据、信令或路测证据；区分已确认与待核实。

**优化措施及效果/进展：** 已实施动作、前后指标、效果口径、未闭环事项。

**后续计划：** 责任方向、下一步动作、验证指标和完成条件。

End with one concise sentence stating the current conclusion and remaining risk.
