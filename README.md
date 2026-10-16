# HTML ↔ PPT 双向技能：HTML 的颜值，PPT 的自由

两套开源免费的 AI Agent 技能，解决汇报演示的终极两难：**好看的不能改，能改的不好看**。

- **html-ppt-master** — 生成深色科技风交互式 HTML 演示（1280×720，单文件，浏览器直接打开）
- **ppt-html-master** — 把 HTML 演示 1:1 还原为可编辑的飞书幻灯片，可导出 PPTX

同一份内容，两个成品：版式、配色、图表、图片完全一致，不用手工重做第二遍。

## 目录结构

```
html-ppt-skills/
├── html-ppt-master/          # 生成端：HTML 演示
│   ├── SKILL.md              # 技能说明（含设计规范与工作流程）
│   ├── assets/template.html  # 页面模板骨架
│   └── references/
│       └── slide-templates.md  # 9 种页面模板
├── ppt-html-master/          # 还原端：HTML → 飞书幻灯片/PPTX
│   └── SKILL.md
├── LICENSE
└── README.md
```

## 使用方法

这两套是 Agent Skills 格式，放到你的 AI 助手 skills 目录即可：

```bash
cp -r html-ppt-master ~/.muse/skills/   # 或你的自定义 skills 目录
cp -r ppt-html-master ~/.muse/skills/
```

然后直接对 AI 说：

- 「做个 HTML 版 PPT」→ 调用 `html-ppt-master` 生成交互式演示
- 「把这个 HTML 转成可编辑 PPT」→ 调用 `ppt-html-master` 还原为飞书幻灯片

## 前置要求

- `html-ppt-master`：无依赖，有浏览器就能看。
- `ppt-html-master`：需要飞书开放平台 CLI（lark-cli）并完成 `config init`，且飞书应用开通文档与幻灯片写入权限。技能内的 lark-cli 命令、XML schema、校验规则以飞书开放平台文档为准。

## 设计规范（生成端）

- 画布固定 1280×720；色板禁止新增颜色（深色蓝图风：`#05060f` 背景 / `#663af3` 强调紫）
- 图表用内联 SVG 手绘，不转位图
- 9 种页面模板：封面 / 议程 / 指标矩阵 / 三列卡片 / 双图表 / 精炼列表 / 对比表格 / 战略卡片 / 结束页

## 还原原理（还原端）

不是截图贴图，而是**逐元素映射**：

1. **坐标换算**：1280×720 HTML 画布 → 960×540 飞书画布，统一 ×0.75
2. **设计系统映射**：色板、渐变、玻璃拟态一一对应
3. **图表原生嵌入**：SVG 以 embed 形式保留，不失真
4. **三重校验**：静态 lint → 整稿回读 → 逐页截图核对

## 开源协议

MIT License — 随便用，详见 [LICENSE](LICENSE)。

## 交流

豆包工作硬刚 Workbuddy 群：一起折腾 AI 提效。欢迎提 Issue 分享你用这套流程做出来的演示。
