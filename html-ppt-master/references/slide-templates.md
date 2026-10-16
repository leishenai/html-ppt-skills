# 幻灯片模板参考

9 种内置页面模板。生成时根据内容类型选择对应模板，直接复制 HTML 片段替换内容。

---

## T01 · Cover Hero（封面）

**适用**：开场封面、章节封面、主题页。

**结构**：全屏背景图 + 底部渐变遮罩 + 大标题 + 底部元数据栏。

```html
<section class="slide s-cover-hero active" data-slide="0">
  <img class="cover-hero-bg" src="images/cover.jpg" alt="封面图">
  <div class="cover-hero-content stagger">
    <span class="kicker">Executive Briefing · 高管汇报</span>
    <div class="h-display">主标题<br>第二行<br>第三行</div>
    <p class="lead">副标题/简介文字，控制在 2-3 行。</p>
  </div>
  <div class="cover-hero-meta">
    <span>指标一<strong>数值</strong></span>
    <span>指标二<strong>数值</strong></span>
    <span>指标三<strong>数值</strong></span>
  </div>
</section>
```

**要点**：背景图用 `object-fit:cover` 铺满；`.h-display` 最多 3 行；meta 栏放 2-4 个关键数字。

---

## T02 · Agenda（议程/目录）

**适用**：目录页、议程页、章节导航。

**结构**：左侧标题区 + 右侧编号列表（序号/名称/英文）。

```html
<section class="slide s-agenda" data-slide="1">
  <div class="agenda-side stagger">
    <span class="kicker">00 / Agenda</span>
    <h1 class="h-1">六大核心议题</h1>
    <p class="lead">引导语，说明本次内容框架。</p>
  </div>
  <div class="agenda-list stagger">
    <div class="agenda-item">
      <span class="idx">01</span>
      <span class="name">议题名称</span>
      <span class="en">English Name</span>
    </div>
    <!-- 重复 agenda-item，建议 4-8 条 -->
  </div>
</section>
```

**要点**：列表最多 8 条（max-height 582px）；序号用两位数字。

---

## T19 · Metric Matrix（指标矩阵）

**适用**：核心数据展示、KPI 总览、行业规模数据。

**结构**：顶部标题区 + 4 列指标网格（数值/标签/变化/来源）。

```html
<section class="slide s-metrics" data-slide="2">
  <div class="dense-head stagger">
    <div>
      <span class="kicker">01 / Section</span>
      <h1 class="h-1">页面主标题</h1>
    </div>
    <p class="lead">右侧引导文字。</p>
  </div>
  <div class="metrics-grid stagger">
    <div class="metric-cell">
      <span class="metric-value">1.2<b>万亿</b></span>
      <span class="metric-label">指标说明</span>
      <span class="metric-delta up">↑ 同比增长40%</span>
      <span class="source">来源：xxx</span>
    </div>
    <!-- 重复 metric-cell，4 的倍数：4/8/12 -->
  </div>
</section>
```

**要点**：`.metric-value` 中 `<b>` 包裹单位（万亿/%/+）；`.metric-delta` 用 `up`(绿) 或 `down`(红)；8 个指标为最佳密度。

---

## T04 · Grid Lines（三列卡片）

**适用**：行业/领域/场景分类展示，带图片或纯文字。

**结构**：顶部标题 + 3 列卡片（编号/名称/英文/图片/描述/强调标签）+ 底部统计行。

```html
<section class="slide s-lines" data-slide="3">
  <div class="lines-head stagger">
    <div>
      <span class="kicker">02 / Section</span>
      <h1 class="h-1">页面主标题</h1>
    </div>
    <p class="lead">引导文字。</p>
  </div>
  <div class="lines-grid stagger">
    <div class="line-cell">
      <span class="num">01</span>
      <div class="name">分类名称</div>
      <div class="en">English</div>
      <img class="cell-img" src="images/x.jpg" alt="配图">
      <div class="desc">描述文字。</div>
      <div class="accent">关键数据/标签</div>
    </div>
    <!-- 3 个 line-cell -->
  </div>
  <div class="stagger" style="display:flex;gap:48px;padding:0 8px;">
    <div style="display:flex;align-items:center;gap:12px;">
      <span style="font-size:32px;font-weight:200;color:#663af3;font-family:'JetBrains Mono',monospace;">-28%</span>
      <span style="font-size:13px;color:#c7d3ea;">说明<br>两行</span>
    </div>
    <!-- 底部统计 2-4 组 -->
    <div style="margin-left:auto;font-size:11px;color:#6b7280;font-style:italic;align-self:center;">数据来源：xxx</div>
  </div>
</section>
```

**要点**：固定 3 列；无图时给 `.desc` 加 `style="margin-top:48px"` 保持视觉平衡；底部统计行可选。

---

## T17 · Chart（双图表）

**适用**：数据可视化页，左右两个 SVG 图表。

**结构**：顶部标题 + 左右两个图表面板（标题/副标题/SVG 图表区）。

```html
<section class="slide s-chart" data-slide="4">
  <div class="chart-head stagger">
    <div>
      <span class="kicker">03 / Section</span>
      <h1 class="h-1">页面主标题</h1>
    </div>
    <p class="lead">引导文字。</p>
  </div>
  <div class="chart-grid stagger">
    <div class="chart-panel">
      <div class="chart-cap">
        <span class="chart-title">CHART TITLE</span>
        <span class="chart-subtitle">图表副标题</span>
      </div>
      <div class="chart-area">
        <svg viewBox="0 0 420 240" preserveAspectRatio="xMidYMid meet">
          <!-- 手绘 SVG 图表：折线/柱状/饼图/条形 -->
          <!-- 配色：主色 #663af3，辅助 #e87b52/#64748b -->
          <!-- 文字色 #6b7280(轴) #c7d3ea(标签) #d8ecf8(高亮) -->
        </svg>
      </div>
    </div>
    <!-- 第二个 chart-panel -->
  </div>
  <div class="stagger" style="display:flex;justify-content:space-between;font-size:11px;color:#6b7280;font-style:italic;padding:0 8px;">
    <span>左图来源：xxx</span>
    <span>右图来源：xxx</span>
  </div>
</section>
```

**要点**：SVG viewBox 固定 `0 0 420 240`；用内联 `<defs><linearGradient>` 做渐变填充；坐标轴用 `rgba(186,215,247,0.1)` 虚线。

---

## T06 · Refine List（精炼列表）

**适用**：要点详解、趋势分析、逐条论据。

**结构**：左侧标题区 + 右侧编号列表（大数字标签/标题/描述/来源）。

```html
<section class="slide s-refine" data-slide="5">
  <div class="refine-left stagger">
    <span class="kicker">04 / Section</span>
    <h1 class="h-1">页面主标题</h1>
    <p class="lead">引导文字。</p>
  </div>
  <div class="refine-list stagger">
    <div class="refine-item">
      <span class="idx"><b>50.23%</b> · 应用率</span>
      <div>
        <div class="h">要点标题</div>
        <div class="d">详细描述文字。<span class="source">— 来源</span></div>
      </div>
    </div>
    <!-- 重复 refine-item，建议 3-6 条 -->
  </div>
</section>
```

**要点**：`.idx` 中 `<b>` 放核心数字，后面跟 `· 标签`；最多 6 条（max-height 582px）。

---

## T21 · Comparison（对比表格）

**适用**：方案对比、前后对比、多维度比较。

**结构**：顶部标题 + 对比表格（维度列 + 2 个比较列）+ 底部来源。

```html
<section class="slide s-comparison" data-slide="6">
  <div class="dense-head stagger">
    <div>
      <span class="kicker">05 / Section</span>
      <h1 class="h-1">页面主标题</h1>
    </div>
    <p class="lead">引导文字。</p>
  </div>
  <div class="compare-table stagger">
    <div class="cmp-row cmp-header">
      <span class="cmp-dim">维度</span>
      <span>方案A</span>
      <span class="cmp-highlight">方案B（推荐）</span>
    </div>
    <div class="cmp-row">
      <span class="cmp-dim">维度名</span>
      <span>A 的值 <span class="cmp-tag warn">标签</span></span>
      <span class="cmp-highlight">B 的值 <span class="cmp-tag ok">标签</span></span>
    </div>
    <!-- 重复 cmp-row，建议 4-7 行 -->
  </div>
  <div class="stagger" style="display:flex;justify-content:space-between;font-size:11px;color:#6b7280;font-style:italic;padding:0 8px;">
    <span>来源说明</span>
  </div>
</section>
```

**要点**：推荐列加 `cmp-highlight`；标签用 `cmp-tag` + `warn`(橙)/`risk`(红)/`ok`(绿)/`info`(紫)。

---

## T03 · Brand（品牌/战略卡片）

**适用**：战略维度、能力框架、组织升级、品牌主张。

**结构**：左侧标题+3个统计数字 + 右侧卡片列表（编号/标签/标题/描述/徽章）。

```html
<section class="slide s-brand" data-slide="7">
  <div class="brand-left stagger">
    <span class="kicker">06 / Section</span>
    <h1 class="h-1">页面主标题</h1>
    <p class="lead">引导文字。</p>
    <div class="brand-stats">
      <div><div class="k">-28%</div><div class="lbl">标签<br>两行</div></div>
      <div><div class="k">+22%</div><div class="lbl">标签</div></div>
      <div><div class="k">500万</div><div class="lbl">标签</div></div>
    </div>
  </div>
  <div class="brand-cards stagger">
    <div class="brand-card">
      <div>01</div>
      <div>
        <div class="tag">分类标签</div>
        <div class="title">卡片标题</div>
        <div class="desc">卡片描述。</div>
      </div>
      <div class="badge">徽章</div>
    </div>
    <!-- 重复 brand-card，建议 3-5 张 -->
  </div>
</section>
```

**要点**：左侧统计固定 3 个；右侧卡片 3-5 张（max-height 582px）；`.badge` 放层级/类型标签。

---

## T08 · Closing（结束/行动页）

**适用**：结尾页、总结页、行动建议页。

**结构**：左右分栏 — 左侧宣言区（大标题+副标题+署名），右侧行动要点（编号列表+底部引导）。

```html
<section class="slide s-close" data-slide="8">
  <div class="close-left">
    <div class="chrome-min">
      <span>09 / Closing</span>
      <span>Action Plan</span>
    </div>
    <div class="manifesto stagger">
      <div class="meta">Key Takeaway</div>
      <h2>宣言主标题<br>第二行</h2>
      <div class="sub">副标题文字。</div>
    </div>
    <div class="sig">
      <span>基于 xxx 体系</span>
      <span>2026年9月</span>
    </div>
  </div>
  <div class="close-right">
    <div class="chrome-min">
      <span>行动建议</span>
      <span>3 Priorities</span>
    </div>
    <div class="takeaways stagger">
      <div class="take-item">
        <div class="num">01</div>
        <div>
          <h3>行动标题</h3>
          <p>行动描述。</p>
        </div>
      </div>
      <!-- 重复 take-item，建议 2-4 条 -->
    </div>
    <div class="foot">→ 下一步：xxx</div>
  </div>
</section>
```

**要点**：此页自动隐藏顶部/底部 chrome 栏；`.manifesto h2` 最多 2 行；右侧 take-item 2-4 条。

---

## 通用规则

1. **data-slide**：从 0 开始递增，第一张加 `active` 类。
2. **stagger**：需要错峰入场动画的容器加 `class="stagger"`，子元素自动依次淡入。
3. **页码**：底部 `pageNum` 自动更新，只需改总页数 `/ XX`。
4. **图片**：本地图片放 `images/` 目录，用相对路径引用；无图时删除 `<img>` 标签。
5. **颜色**：不要新增颜色变量，只用已有色板。强调色统一 `#663af3`。
6. **字体**：数字/代码/标签用 `JetBrains Mono`（已在对应 class 中设置），正文用系统无衬线。
7. **内容密度**：每个模板有 max-height 限制，条目数不要超过建议上限，否则内容被裁剪。
