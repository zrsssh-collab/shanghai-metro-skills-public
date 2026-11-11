---
name: shanghai-metro-complaint-analysis
description: Analyze Shanghai metro wireless-network complaints from time/location, PS, user-plane, KQI/KPI, SPD, cell, radio, mobility, uplink, TCP and DNS evidence; produce a concise leadership-ready report.
---

# Shanghai Metro Complaint Analysis

Use this skill for a Shanghai metro wireless-network complaint when the user expects a technical root-cause analysis, evidence-backed diagnosis, and corrective actions. Do not use it for generic telecom explanations or voice-only complaint templates.

## Default deliverable

Write in a concise, leadership-ready tone. Mirror the user's requested language; when the source material and request are Chinese, use Chinese headings and prose. Unless the user asks for another format, use exactly this top-level structure:

1. **问题现象**
2. **问题分析**
3. **解决方案**

Use short paragraphs and bullets. Put the conclusion first when useful, then the supporting evidence. Keep observed facts separate from hypotheses and recommendations. For a fuller fill-in template, read [references/report-template.md](references/report-template.md).

## Working context and inputs

Inspect the supplied attachments and project files first. Relevant inputs may include:

- SPD logs and configuration or alarm exports.
- KQI/KPI workbooks for the complaint period and affected cells.
- PS historical session records and user-plane records.
- Related reports, signaling traces, road-test logs, and cell-mapping files.

Open relevant files inside archives and inspect every workbook sheet before drawing conclusions; do not rely on filenames alone. Treat filenames and contents as evidence, not as proof of causality. Before analysis, make an input checklist and note missing or unreadable files. Continue with the available records rather than assuming any example input exists.

Minimum checklist:

- Complaint time window, exact station/section/location, direction/platform/train context, symptom and affected service.
- PS historical session records and user-plane records aligned to the complaint time.
- KQI/KPI slices for the same period and cells.
- SPD lock/free-state logs and any SPD configuration or alarm records.
- Exact serving/neighbor cell IDs and names, with mapping source and timestamp.
- RSRP, RSRQ, SINR, CQI and any coverage/quality counters.
- Handover events and parameters: A3/A6, CIO, TTT, execution/result and failure cause.
- Uplink evidence: interference, PUSCH SINR, UE transmit power, path loss and related counters.
- TCP evidence (retransmission, RTT, resets, throughput) and DNS evidence (query/response, timeout, resolver path).

If a field is unavailable, say so explicitly and lower confidence; do not silently fill it from assumptions.

Run basic data-quality checks before joining records: sheet/file coverage and row counts, representative samples, duplicate rows, timestamp/timezone consistency, gaps around the complaint window, and mismatched cell or session keys. Join on stable keys (for example subscriber/session plus timestamp and cell), not loose proximity alone. Compare each metric with an explicit baseline, threshold or control period before calling it abnormal. Flag conflicts instead of choosing a value silently. Mask IMSI/MSISDN and other subscriber identifiers in leadership-facing output unless the user explicitly requires the raw identifier.

## Analysis order

1. **Fix the timeline and location.** Normalize timestamps and timezone, then map each record to the complaint interval. Use only provided cell mappings/names; preserve them exactly in the report.
2. **Reconstruct the session.** Join PS history, user-plane records and KQI/KPI by subscriber/session, time and cell. Identify the first degradation, continuity breaks and recovery point.
3. **Check network state.** Compare SPD lock/free state, service/neighbor cells, alarms and configuration around the event. Explain whether a lock or missing neighbor is observed or merely suspected.
4. **Assess radio conditions.** Trend RSRP, RSRQ, SINR and CQI, and distinguish coverage weakness, quality/interference degradation and capacity symptoms. Use synchronized samples rather than one isolated value.
5. **Assess mobility.** Verify serving-to-neighbor sequence, A3/A6 reports, CIO/TTT, handover attempt/execution/completion and failure causes. Attribute a mobility issue only when event evidence supports it.
6. **Assess uplink separately.** Check interference, PUSCH SINR, UE power and path loss together. A high UE power or path loss alone is not proof of uplink interference.
7. **Assess transport and DNS as separate layers.** Correlate TCP symptoms with radio/session evidence. Keep DNS as its own possible layer unless timing and packet-level evidence show that DNS caused the user-visible symptom; do not fold DNS into a radio conclusion by default.
8. **Rank causes and actions.** State the most supported cause, alternatives, confidence and the smallest next check that would discriminate between them.

## Evidence rules

- Prefer, in order: time-aligned raw signaling/user-plane/trace records; exact cell and configuration/alarm records; synchronized KQI/KPI counters; aggregated reports; user description and terrain/distance intuition.
- Label claims as **事实/观测** (directly present in a record), **推断/假设** (interpretation requiring validation), or **待核实** (missing decisive evidence).
- Use confidence language: **高置信度** when multiple independent, time-aligned sources agree; **中置信度** when the pattern is consistent but one decisive field is missing; **低置信度/待核实** when based mainly on indirect or incomplete evidence.
- Never infer an interval, handover relation or coverage boundary from a cell name, station name or geometric distance alone. Use measured timestamps, serving/neighbor records or an explicit mapping.
- Never copy voice-domain templates into a data-service complaint. Keep the analysis centered on PS/user-plane behavior and the measured failure mode.
- Do not rename or “clean up” supplied cell names, IDs or mappings; quote the source label and identify the source file/time.
- Avoid causal verbs such as “导致” unless the evidence supports temporal and technical linkage. Otherwise use “与…同时出现”“支持…可能性” or “尚不能确认”.

## Technical interpretation prompts

Use these as checks, not automatic diagnoses:

- **SPD:** verify lock/free state and timing against service/neighbor changes; a lock record is stronger than a name-based inference.
- **Radio:** interpret RSRP with RSRQ/SINR/CQI and user-plane impact. Poor quality with adequate RSRP points toward interference/quality; all metrics weak points toward coverage or blockage, subject to corroboration.
- **Mobility:** require an observed event sequence and parameters before attributing failure to A3/A6, CIO or TTT. Distinguish measurement/reporting, decision, execution and completion failures.
- **Uplink:** jointly inspect interference, PUSCH SINR, UE power and path loss; state which component is observed and which is inferred.
- **TCP/DNS:** report DNS query/response and TCP behavior separately from RAN findings. A DNS timeout is not evidence of radio root cause without a synchronized causal chain.

## Final report template

Use this compact template unless the user requests a different format (the detailed version is in `references/report-template.md`):

**问题现象**
- 时间/地点/方向：…
- 用户感知与业务：…
- 影响范围与复现情况：…

**问题分析**
- **事实/观测：** …（来源、时间、服务/邻区、关键数值）
- **链路复盘：** PS/用户面 → SPD/小区 → 无线 → 切换 → 上行 → TCP/DNS
- **主要原因（置信度）：** …
- **备选原因/待核实：** …
- **证据缺口：** …

**解决方案**
- 立即措施：…
- 参数/网络优化：…（明确 A3/A6/CIO/TTT、邻区、SPD 或上行项）
- 验证方案：…（时间窗、指标、成功标准）
- 后续预防：…

End with a one-sentence conclusion that separates what is confirmed from what still needs verification.
