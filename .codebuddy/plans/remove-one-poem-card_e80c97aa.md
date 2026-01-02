---
name: remove-one-poem-card
overview: 从西湖诗词展示模块中删除1首诗词，保留9首
todos:
  - id: locate-poem-data
    content: 使用 [subagent:code-explorer] 定位西湖诗词数据文件
    status: completed
  - id: remove-poem
    content: 从诗词数据列表中删除1首诗词，保留9首
    status: completed
    dependencies:
      - locate-poem-data
  - id: verify-display
    content: 验证前端页面正确展示剩余9首诗词
    status: completed
    dependencies:
      - remove-poem
---

## Product Overview

对现有的西湖诗词展示模块进行调整，从当前展示的诗词列表中移除1首诗词，确保最终保留9首诗词展示。

## Core Features

- 从西湖诗词数据源中移除指定的1首诗词
- 确保前端页面正确展示剩余的9首诗词
- 保持诗词卡片的展示样式和交互逻辑不变

## Tech Stack Selection

基于现有项目结构，使用当前技术栈进行修改（无需引入新技术）

## Tech Architecture

### System Architecture

此任务属于数据层和展示层的轻微修改：

- 数据层：修改诗词数据配置文件
- 展示层：验证前端渲染结果

### Module Division

- **数据配置模块**：存储西湖诗词列表的JSON或配置文件
- **展示组件模块**：诗词卡片展示组件

### Data Flow

诗词数据文件 → 前端组件读取 → 渲染诗词卡片列表

## Implementation Details

### Core Directory Structure

仅展示需要修改或查看的文件：

```
project-root/
├── src/
│   ├── data/
│   │   └── poems.ts        # 诗词数据配置文件（待修改）
│   └── components/
│       └── PoemCard.tsx    # 诗词卡片组件（验证用）
```

### Key Code Structures

**诗词数据结构**：定义单首诗词的基本信息

```typescript
interface Poem {
  id: string;
  title: string;
  author: string;
  content: string;
}
```

**修改策略**：

1. 定位包含10首诗词的数据文件
2. 删除1首指定的诗词条目
3. 保存文件并验证渲染效果

### Technical Implementation Plan

1. **问题陈述**：需要从西湖诗词展示中移除1首诗词
2. **解决方案**：直接编辑诗词数据源文件，删除目标诗词对象
3. **关键技术**：TypeScript数据结构操作
4. **实施步骤**：

- 使用 [subagent:code-explorer] 定位诗词数据文件
- 分析当前诗词列表，确定需要删除的诗词
- 从数组中移除该诗词对象
- 保存文件并验证展示效果

5. **测试策略**：检查前端页面确认诗词卡片数量为9首

## Agent Extensions

### SubAgent

- **code-explorer**
- Purpose: 搜索和定位项目中包含西湖诗词数据的文件
- Expected outcome: 找到存储10首诗词的配置文件路径和内容