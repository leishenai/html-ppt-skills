---
name: ppt-html-master
description: 将 html-ppt-master 生成的深色科技风 HTML 演示文稿 1:1 还原为可编辑的飞书幻灯片（在线 Slides + PPTX 导出）。当用户提供 html-ppt-master 输出的 .html 文件并要求"转成PPT""还原成幻灯片""做成可编辑PPT"时使用。覆盖9种页面模板（封面/议程/指标矩阵/三列卡片/双图表/精炼列表/对比表格/战略卡片/结束页）的坐标换算、图片迁移、SVG图表嵌入、逐页XML编写与静态校验全流程。
---

# PPT HTML Master — HTML 演示文稿转飞书幻灯片

将 `html-ppt-master` 生成的 1280×720 深色科技风 HTML 演示文稿，1:1 还原为 960×540 可编辑飞书幻灯片，保留原版式、配色、图表、图片和文字。

## 前置依赖

需要飞书开放平台 CLI（lark-cli）并完成 `config init`，且飞书应用开通文档与幻灯片写入权限。本 skill 只补充 HTML→PPT 转换的特定知识，所有 lark-cli 命令、XML schema、校验规则以飞书开放平台文档为准。

## 核心工作流程

### 1. 解析源 HTML

完整读取 HTML 文件，识别每页使用的模板 class（`s-cover-hero` / `s-agenda` / `s-metrics` / `s-lines` / `s-chart` / `s-refine` / `s-comparison` / `s-brand` / `s-close`），提取每页的：
- 文字内容（标题、正文、标签、数据）
- 图片引用路径（`<img src>`）
- SVG 图表内容（`<svg>` 内联）
- 装饰元素（渐变背景、光晕、分隔线）

### 2. 坐标换算

HTML 画布 1280×720 → 飞书画布 960×540，**所有坐标和尺寸统一乘以 0.75**：

```
飞书 x = HTML x × 0.75
飞书 y = HTML y × 0.75
飞书 width = HTML width × 0.75
飞书 height = HTML height × 0.75
字号 = HTML font-size × 0.75（取整）
```

字号换算参考：HTML 72px→飞书54px，56px→42px，48px→36px，32px→24px，24px→18px，16px→12px，14px→10px，12px→9px。

### 3. 图片迁移

将 HTML 引用的所有本地图片复制到工作目录，用 `lark-cli slides +media-upload` 逐个上传获取 `file_token`，写入 XML 的 `<img src>`。

注意：HTML 中 CSS 背景图（`background-image: url(...)`）需要提取为独立 `<img>` 元素，放在对应位置作为底层背景。

### 4. 逐页编写 XML

按页序逐页编写单页 `<slide>` XML，每页存为独立文件（如 `slide-01.xml`）。编写要点见下方「9种页面模板还原要点」。

### 5. 单页静态校验

每页写入前必须跑 XML lint，`error_count` 必须为 0 才能写入。

### 6. 逐页写入飞书

```bash
lark-cli slides +create --title "演示文稿标题"   # 首次创建0页空白
lark-cli slides +add-slide --presentation $PID --slide @slide-01.xml
```
一页校验通过就写一页，不要攒完整份再统一校验。

### 7. 全文回读校验

全部写入后回读全文，确认 `slide_count` 等于预期页数、`error_count=0`。逐页核对关键文本和元素是否齐全。

### 8. 导出 PPTX 并交付

```bash
lark-cli drive +export --token $PID --doc-type slides --file-extension pptx --output-dir .
```

同时交付：在线幻灯片链接 + 本地 PPTX 文件路径。

## 设计系统映射

html-ppt-master 的色板直接映射为飞书 XML 的 rgba 颜色：

| 角色 | HTML 色值 | 飞书 XML |
|------|-----------|----------|
| 画布背景 | `#05060f` | `rgba(5,6,15,1)` |
| 卡片背景 | `#0a0b14` | `rgba(10,11,20,1)` |
| 主强调紫 | `#663af3` | `rgba(102,58,243,1)` |
| 标题文字 | `#d8ecf8` | `rgba(216,236,248,1)` |
| 次标题 | `#d1e4fa` | `rgba(209,228,250,1)` |
| 正文 | `#c7d3ea` | `rgba(199,211,234,1)` |
| 次要文字 | `#9da7ba` | `rgba(157,167,186,1)` |
| 注释/来源 | `#6b7280` | `rgba(107,114,128,1)` |
| 上升/正面 | `#4ade80` | `rgba(74,222,128,1)` |
| 下降/风险 | `#f87171` | `rgba(248,113,113,1)` |
| 警告 | `#e87b52` | `rgba(232,123,82,1)` |

玻璃拟态卡片：用 `rgba(186,214,247,0.03)` 填充 + `rgba(186,215,247,0.1)` 1px 边框模拟。

**CSS 渐变文字不支持**：HTML 中 `-webkit-background-clip: text` 的渐变标题，在飞书中用纯色 `rgba(216,236,248,1)` 近似。

## 9种页面模板还原要点

### 封面 s-cover-hero
- 全屏背景图 `<img>` 铺满 960×540，放在最底层
- 大标题字号 42-54px，`letterSpacing="-1"` 营造质感
- 底部数据栏用 3 列等宽布局，每列含大数字 + 标签

### 议程 s-agenda
- 左右分栏，每项结构：序号（紫色等宽字体）+ 标题（加粗）+ 英文标签（次要色，全大写）

### 指标矩阵 s-metrics
- 4列×2行卡片网格，每张卡片：大数字（紫色 28-32px）+ 指标名 + 描述 + 底部趋势标签

### 三列卡片 s-lines
- 3列等宽卡片，每列含：标签 + 标题 + 描述 + 配图，底部通栏统计数据带

### 双图表 s-chart
- 左右两个图表区，SVG 图表用 `<embed>` 内联嵌入，**必须保留 `xmlns` 和 `viewBox`**

### 精炼列表 s-refine
- 5项纵向列表，每项含：序号（紫色大号）+ 标题（加粗）+ 描述

### 对比表格 s-comparison
- 用 `<table>` 标准表格结构，表头行必须设背景色和加粗白字

### 战略卡片 s-brand
- 左右分栏：左侧文字区 + 右侧卡片区；右侧卡片含序号 + 维度标签 + 标题 + 描述 + 徽章

### 结束页 s-close
- 左右分栏沉浸式布局，**不显示全局 chrome**（顶部品牌栏和底部页码）

## 全局 Chrome 还原

除结束页外，每页包含顶部品牌栏（左侧品牌名 + 右侧日期）与底部页码栏（`01 / 09` 格式，当前页紫色高亮）。

## 常见问题

- `text_may_overflow_shape`：单行文字太宽 → 加宽 `width` 并多留余量
- `bbox_overlap`：元素区域重叠 → 调整坐标错开，序号列与标题列留 ≥15px 间隙
- `shape_out_of_canvas`：装饰元素负坐标 → 删掉或移到画布内
