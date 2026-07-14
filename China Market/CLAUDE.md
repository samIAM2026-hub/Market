# CLAUDE.md — China Market

中国 A 股板块 / 行业 / 风格 / ETF 研究。宏观交易者视角，**只投基金与 ETF**（不做个股择时）。
姊妹目录 `../US Market/` 用另一套配色，不要混用。

## 1. 现有文件

```text
China Market/
├── index.html                          # 主入口 · 当前主研报（10 章 · 2025-05 → 2026-04）
├── README.md                           # 面向人的目录说明（新增页面时更新 Dashboards 表）
└── pages/
    ├── guides/index_guide.html                    # A股指数体系交互式指南
    ├── guides/etf_allocation_guide.html           # 核心指数高流动性 ETF 配置指南
    ├── thematic/AI就业冲击_三图解读.html            # 主题研究
    ├── macro/沃什货币政策哲学_投资者手册.html        # 宏观 / 政策手册
    ├── company/SpaceX深度投资分析_2026-06.html      # 单公司深度
    └── archive/a_share_2025_research.html         # 2025-vintage 存档，不要覆盖
```

新页面按主题归入 `pages/` 下已有的五个子目录之一。**存档页只增不改** —— 保留旧版本作时序对照。

## 2. 页面骨架

所有 7 个页面共享同一套骨架，新建页面时照抄，不要另起炉灶：

```
<header class="topbar">        深蓝渐变 + 底部 3px 烫金线
  .brand-seal                  单个汉字印章（红底金边），如 "星"
  .brand-title / .brand-sub    中文标题 + 全大写英文副标题（letter-spacing 2px）
  .topbar-meta                 2–4 个 "标签：<b>值</b>" 元信息
<nav class="chapters">         sticky，top:71px
  .chapter-tab > .num          章节序号用中文数字：壹 贰 叁 肆 伍 陆 柒 捌 玖 拾
<main>
  section.chapter[id=ch1..N]   .ch-head > .ch-title(.ch-num + 文字) + .ch-en(英文小标)
    .tldr                      每章开头一句话结论（金色左边框）
    .kpi-grid > .kpi           数字卡
    table.research             深蓝表头；涨跌用 .perf-up / .perf-down / .perf-flat
    .two-col / .prose          正文
<footer>                       "· 主题 · 统计区间 · 更新于 YYYY-MM-DD · 宏观交易者专用 ·"
```

导航有两种写法，**新页面统一用 `data-target` 那种**（index.html 的写法），它带滚动高亮：
`.chapter-tab` 点击 → `document.getElementById(tab.dataset.target).scrollIntoView({behavior:'smooth'})`，
再用 scroll 监听给当前章节的 tab 加 `.active`。（`pages/guides/index_guide.html` 等用 `href="#ch1"` 的是早期写法。）

## 3. 配色（七个页面完全一致，逐字照抄）

```css
:root{
  --bg:#F7F4ED; --paper:#FFFFFF;
  --ink:#1A1A1A; --ink-2:#3D3D3D; --ink-3:#6B6B6B;
  --line:#E4DED1; --line-strong:#C8BFAE;
  --navy:#0E2A47; --navy-2:#143E66;
  --gold:#B08842; --gold-light:#D4B271;
  --up:#D7263D;   --up-soft:#FBE9EC;   --up-deep:#9E1A2D;   /* A股惯例：红涨 */
  --down:#1F8A47; --down-soft:#E7F5EC; --down-deep:#125F30; /* 绿跌 */
  --flat:#8A8A8A;
}
```

需要第四色时加 `--warm:#E27A3F`（guides 两页已用），高亮块用 `--highlight:#FFF7E0`。
**红涨绿跌是硬性约定**，与美股相反 —— 生成图表、表格、条形图时都要遵守。

## 4. 技术约束

- 自包含单文件 HTML，无构建步骤，浏览器直接打开。
- CDN 只用两个：`chart.js@4.4.1`（`cdn.jsdelivr.net/npm/chart.js@4.4.1/dist/chart.umd.min.js`）
  和 Google Fonts 的 `Noto Sans SC` + `Noto Serif SC`。
- 正文字体 Noto Sans SC，标题 / 数字 / 章节号用 `.serif`（Noto Serif SC）。
- **不要用负字距**（`letter-spacing` 为负会让中文挤在一起）。英文小标题用正字距 2–3px。
- 交互统一走原生 JS：tab 切换、Chart.js 横向条形图、模态框。无框架、无依赖。

## 5. 语言与内容规范

- **中文为主，英文为辅** —— 英文只用于副标题、指标名、ETF 代码、章节 EN 标签。
- ETF / 指数**必须带代码**（如 `沪深300 ETF(510300)`），指数名尽量与 `pages/guides/index_guide.html` 里的
  `INDEX_INFO` 键对齐 —— 主页有自动匹配脚本会把这些名称变成可点击的指数详情链接。
- **数据区间必须写死在页面上**：topbar 元信息 + footer 各写一次（如 `2025-05 → 2026-04`）。
- 标注数据来源与日期（Wind / 东方财富 / 券商研报）。原始 `.md` / `.docx` 素材不进仓库。
- 不提交账户信息、API key、券商对账单。

## 6. 每次新增 / 移动页面必做

1. 归入 `pages/<type>/`，文件名用中文标题 + ISO 日期后缀（`名称_YYYY-MM.html`）。
2. 在页面里加返回主页链接 `href="../../index.html"`（**当前只有 `index_guide.html` 有，其余 5 页缺失**，
   下次改动这些页面时顺手补上）。
3. 更新本目录 `README.md` 的 Dashboards 表格。
4. 更新仓库根 `../../index.html` 的卡片（China Market 目前在根页有 4 处链接：主入口、SpaceX、沃什、AI就业冲击）。
5. 移动文件后逐个 `href` 验证，注意相对路径深度是 `../../`。
