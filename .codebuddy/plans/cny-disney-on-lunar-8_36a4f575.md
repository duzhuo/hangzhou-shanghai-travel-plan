---
name: cny-disney-on-lunar-8
overview: 将行程中迪士尼日调整为农历正月初八（2月24日），并与原正月初八的外滩·南京路日对调，保证日历总览与Day 5/Day 6内容一致。
todos:
  - id: scan-html-sections
    content: 使用[subagent:code-explorer]定位总览与Day5/6区块
    status: completed
  - id: swap-day-blocks
    content: 对调Day5迪士尼与Day6外滩整块内容
    status: completed
    dependencies:
      - scan-html-sections
  - id: swap-date-lunar-labels
    content: 同步对调2/23正月初七与2/24正月初八标注
    status: completed
    dependencies:
      - swap-day-blocks
  - id: update-calendar-overview
    content: 对调日历总览两天条目并校对标题
    status: completed
    dependencies:
      - swap-date-lunar-labels
  - id: fix-anchors-and-toc
    content: 修正目录/锚点/跳转文本与Day编号一致
    status: completed
    dependencies:
      - update-calendar-overview
  - id: global-consistency-check
    content: 使用[subagent:code-explorer]全局检索核对迪士尼/外滩日期
    status: completed
    dependencies:
      - fix-anchors-and-toc
  - id: final-preview
    content: 本地打开HTML快速目视检查排版与连贯性
    status: completed
    dependencies:
      - global-consistency-check
---

## Product Overview

对现有《杭州上海春节自驾游计划.html》进行行程日期对调：将“上海迪士尼”调整到农历正月初八（2月24日），并与原正月初八的“外滩·南京路”日互换，确保“日历总览”与 Day 5/Day 6 的内容、日期与标题完全一致。

## Core Features

- Day 5 与 Day 6 行程整日对调（含公历日期、农历日期、标题与对应内容块）
- 日历总览中的两天条目同步对调，展示一致
- 保持页面内导航/锚点/目录（如存在）与对调后的 Day 编号和内容一致
- 版式不变：仅更新文本与对应区块顺序，视觉呈现连续自然

## Tech Stack

- 单文件静态页面：HTML（原文件结构保持不变）

## Implementation Notes

- 仅修改目标文件：`/Users/MrDu/CodeBuddy/20260102145713/杭州上海春节自驾游计划.html`
- 修改范围聚焦于：日历总览（overview/calendar）区块与 Day 5/Day 6 两个日程区块（含标题与日期行）
- 验收标准：页面中所有出现的“2月23日/正月初七”“2月24日/正月初八”与“迪士尼 / 外滩·南京路”的对应关系一致

## Agent Extensions

### SubAgent

- **code-explorer**
- Purpose: 在单个大型 HTML 中快速定位“日历总览”“Day 5/Day 6”相关区块、锚点与重复文本位置
- Expected outcome: 输出需要对调/替换的精确片段位置清单，确保修改不遗漏且全局一致