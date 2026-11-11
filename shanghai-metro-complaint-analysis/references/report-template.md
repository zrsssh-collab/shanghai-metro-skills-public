# Shanghai Metro Complaint Analysis Report Template

Use source labels and exact cell names/IDs as supplied. Replace bracketed text; remove sections that genuinely do not apply, but keep missing evidence visible.

## 1. 问题现象

- **投诉时间：** [YYYY-MM-DD HH:MM:SS–HH:MM:SS, timezone]
- **位置/方向：** [station, platform/section, direction, train context; source]
- **用户感知：** [slow/no service/disconnect/timeout and affected app or service]
- **影响范围：** [subscriber/session/cell/time scope; recurrence]

## 2. 问题分析

### 2.1 事实与证据

| 时间 | 记录/来源 | serving/neighbor cell（原名） | 观察到的事实 | 对业务的对应影响 |
|---|---|---|---|---|
| [time] | [PS/user-plane/KQI/SPD/trace] | [exact labels] | [raw value/event with unit and baseline] | [impact or none] |

### 2.2 分层复盘

- **PS/用户面：** [session setup, continuity, throughput, retransmission, resets]
- **SPD/小区状态：** [lock/free, service/neighbor, alarms/config]
- **无线：** [RSRP, RSRQ, SINR, CQI; coverage vs quality interpretation]
- **切换：** [A3/A6, CIO, TTT; report/decision/execution/completion and cause]
- **上行：** [interference, PUSCH SINR, UE power, path loss]
- **TCP：** [RTT, retransmission, resets, throughput]
- **DNS：** [query/response, timeout, resolver path; keep separate unless causal evidence]

### 2.3 原因判断

- **主要原因（置信度：高/中/低）：** [claim]
  - 事实依据：[…]
  - 因果链：[…]
- **备选原因/待核实：** [claim and the discriminating check]
- **不支持的推断：** [e.g., no interval inferred from cell name/distance]
- **证据缺口：** [missing file, timestamp, mapping, or counter]

## 3. 解决方案

1. **立即措施：** [mitigation, owner and target time]
2. **RAN/参数优化：** [exact cell/neighbor, SPD state, A3/A6/CIO/TTT or uplink item; owner/ETA]
3. **传输/DNS follow-up（如适用）：** [separate action; owner/ETA]
4. **验证方案：** [repeat route/time, sample size, metric threshold, pass/fail and owner]
5. **预防与闭环：** [monitoring, alert, mapping/config hygiene; review date]

**结论：** [One sentence: confirmed finding(s), confidence, and what remains to verify.]
