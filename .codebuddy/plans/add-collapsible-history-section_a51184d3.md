---
name: add-collapsible-history-section
overview: 为西湖历史文化部分设计可折叠的展示模块，默认折叠状态，平滑流畅的折叠/展开动画
design:
  architecture:
    framework: react
    component: shadcn
  styleKeywords:
    - Modern Minimalism
    - Smooth Animation
    - Card Design
  fontSystem:
    fontFamily: PingFang SC
    heading:
      size: 24px
      weight: 600
    subheading:
      size: 18px
      weight: 500
    body:
      size: 15px
      weight: 400
  colorSystem:
    primary:
      - "#1890FF"
      - "#40A9FF"
    background:
      - "#FFFFFF"
      - "#F5F5F5"
    text:
      - "#262626"
      - "#595959"
    functional:
      - "#52C41A"
      - "#FF4D4F"
      - "#FAAD14"
todos:
  - id: create-history-types
    content: 创建历史内容类型定义接口
    status: completed
  - id: build-collapsible-component
    content: 实现可折叠历史模块组件结构
    status: completed
    dependencies:
      - create-history-types
  - id: integrate-motion-animation
    content: 集成 Framer Motion 实现折叠/展开动画
    status: completed
    dependencies:
      - build-collapsible-component
  - id: design-content-layout
    content: 设计文字和图片内容的展示布局
    status: completed
    dependencies:
      - build-collapsible-component
  - id: add-interaction-feedback
    content: 添加按钮交互和视觉反馈效果
    status: completed
    dependencies:
      - integrate-motion-animation
---

## Product Overview

为西湖历史文化部分设计可折叠的展示模块，默认折叠状态，支持平滑流畅的折叠/展开动画交互。

## Core Features

- 默认折叠的历史文化展示模块
- 点击触发平滑的折叠/展开动画
- 完整展示内容包括文字介绍和历史图片等多媒体元素

## Tech Stack

- Frontend framework: React + TypeScript
- Styling: Tailwind CSS
- Animation: Framer Motion（用于平滑的折叠/展开动画）

## Tech Architecture

### System Architecture

- 采用组件化设计，将可折叠历史模块封装为独立组件
- 使用条件渲染结合高度动画实现流畅的折叠效果
- 组件内部管理折叠状态，通过 props 接收历史文化内容

### Module Division

- **CollapsibleHistoryModule**: 主组件，包含折叠逻辑和动画控制
- **HistoryContent**: 内容展示子组件，负责渲染文字和图片内容

### Data Flow

用户点击折叠按钮 → 触发状态切换 → Framer Motion 执行高度动画 → 内容区域平滑展开/收起

## Implementation Details

### Core Directory Structure

```
project-root/
├── src/
│   ├── components/
│   │   ├── CollapsibleHistory/
│   │   │   ├── index.tsx          # 主组件文件
│   │   │   └── CollapsibleHistory.tsx  # 可折叠历史模块实现
│   └── types/
│       └── history.ts             # 历史内容类型定义
```

### Key Code Structures

**HistoryContent 接口**: 定义历史文化内容的数据结构

```typescript
interface HistoryContent {
  title: string;
  description: string;
  images: Array<{
    url: string;
    caption?: string;
  }>;
}
```

**CollapsibleHistory 组件**: 实现可折叠交互的核心组件

```typescript
// 组件签名
const CollapsibleHistory: React.FC<{ content: HistoryContent }> = ({ content }) => {
  const [isExpanded, setIsExpanded] = useState(false);
  
  // 使用 Framer Motion 的 AnimatePresence 实现平滑过渡
  return (
    <div className="collapsible-history">
      <motion.div
        initial={false}
        animate={{ height: isExpanded ? 'auto' : 60 }}
        transition={{ duration: 0.3, ease: 'easeInOut' }}
      >
        {/* 历史内容 */}
      </motion.div>
      <button onClick={() => setIsExpanded(!isExpanded)}>
        {isExpanded ? '收起' : '展开'}
      </button>
    </div>
  );
};
```

### Technical Implementation Plan

1. **实现折叠状态管理**: 使用 React useState 管理展开/收起状态
2. **集成 Framer Motion**: 使用 motion.div 和 AnimatePresence 实现高度平滑动画
3. **设计内容布局**: 合理组织文字介绍和历史图片的展示结构
4. **优化交互体验**: 添加适当的过渡效果和视觉反馈

### Integration Points

- 组件接收 HistoryContent 数据作为 props
- 支持自定义样式覆盖以适应不同页面的设计风格
- 图片使用懒加载优化性能

## Design Style

采用现代简约风格，结合流畅的微交互动画。可折叠模块默认展示标题和简要预览，点击后平滑展开展示完整内容。使用卡片式设计，配合阴影和圆角营造层次感。

## Page Planning

### 历史文化详情页

- **顶部导航栏**: 包含页面标题和返回按钮
- **可折叠历史模块**: 核心功能区域
- **标题预览区**: 显示历史文化标题和简短摘要（默认可见）
- **可展开内容区**: 包含详细文字介绍和历史图片（点击展开显示）
- **折叠/展开按钮**: 位于模块底部，带有箭头图标指示当前状态

### 单页块设计规则

- **标题预览区**: 使用卡片头部样式，包含标题（大号字体）和2行预览文字
- **可展开内容区**: 使用 overflow-hidden 控制高度，展开时展示完整内容；图片采用网格布局（2列）
- **交互反馈**: 按钮悬停时颜色加深，点击时有轻微缩放动画；展开/收起时长约300ms
- **响应式设计**: 移动端图片改为单列显示，折叠按钮始终固定在模块底部