# China Market · 中国A股板块与行业研究

宏观交易者视角的中国 A 股板块、行业、风格、ETF 研究 — 只投基金 / ETF。
姊妹目录：`../US Market/`（美股 + 全球宏观）。

## Project Structure

```text
.
├── CLAUDE.md         # 建页规范（骨架 / 配色 / 语言约定）
├── README.md
├── index.html        # 主入口 · 当前主研报（10 章 · 交互式）
└── pages/            # 所有其他内容页，按类型分组
    ├── China Recap/  # 每日 A 股复盘（自动化任务生成，按日期存档）
    ├── guides/       # 交互式指南（A股指数体系、ETF 配置）
    ├── thematic/     # 主题研究（AI 就业冲击 …）
    ├── macro/        # 宏观 / 政策手册（沃什货币政策哲学 …）
    ├── company/      # 单公司深度（SpaceX …）
    └── archive/      # 存档 vintage 研报（a_share_2025_research）
```

内容页均为自包含单文件 HTML。`index.html` 保留在根目录作为主入口，其余页面位于 `pages/` 下两级，
因此回链主页使用 `../../index.html`。命名沿用中文标题 / kebab-case，日期用 ISO `YYYY-MM`。

## Dashboards

| 入口 | 内容 | 数据期 | 状态 |
|------|------|--------|------|
| **[index.html](index.html)** | A 股板块、行业回报与轮动分析（10 章 · 交互式） | **2025-05 → 2026-04** 滚动 12 个月 | **当前主版本** |
| [pages/China Recap/A股每日市场复盘报告_2026-07-15.html](pages/China%20Recap/A股每日市场复盘报告_2026-07-15.html) | A股每日市场复盘（9 章 · 自动化任务每个交易日生成） | 2026-07-15 | 每日 |
| [pages/guides/index_guide.html](pages/guides/index_guide.html) | A股指数体系交互式指南 | — | 参考 |
| [pages/guides/etf_allocation_guide.html](pages/guides/etf_allocation_guide.html) | A股核心指数高流动性 ETF 配置指南 | — | 参考 |
| [pages/thematic/AI就业冲击_三图解读.html](pages/thematic/AI就业冲击_三图解读.html) | AI 的就业冲击 · 全图通俗解读 | — | 主题 |
| [pages/macro/沃什货币政策哲学_投资者手册.html](pages/macro/沃什货币政策哲学_投资者手册.html) | 凯文·沃什的货币政策哲学 · 投资者手册 | — | 宏观 |
| [pages/company/SpaceX深度投资分析_2026-06.html](pages/company/SpaceX深度投资分析_2026-06.html) | SpaceX 深度投资分析 | 2026-06 | 公司 |
| [pages/archive/a_share_2025_research.html](pages/archive/a_share_2025_research.html) | 中国A股基金与ETF组合投资研究报告（10 章 · 交互式） | 2025 全年快照 + 2026 H1 监测点 | 存档（vintage） |

### 当前主版本 (`index.html`) 涵盖

1. **主要指数表现统计** — 7 大指数 12 月涨幅（创业板 +100.9%、科创 50 +89.3%、深证成指 +56.7% …）+ Chart.js 横向条形图
2. **申万 / 中信一级行业排行** — 强势 / 弱势 tab 切换，自绘条形 + 主题驱动卡
3. **热门主题与概念板块** — 11 行主题表（含 ↑↑↑/↓↓ 涨幅符号）+ 趋势 vs 情绪判断
4. **风格与因子表现** — 大盘/小盘、成长/价值、高股息、动量、估值、风险偏好 6 张因子卡
5. **行业轮动的宏观逻辑** — 周期 / 政策 / 流动性 / 海外 4 个维度
6. **ETF 与基金配置视角** — 宽基 / 行业 / 主题 三 tab 切换，25 只 ETF 含代码
7. **行业配置框架** — 5 类（核心 / 景气上行 / 低估修复 / 高波动 / 回避）含色条 + pill
8. **未来 3–12 个月展望** — 8 大方向（高配 / 标配 / 观察 / 低配）含逻辑 + 风险
9. **风险监控指标** — 20 项，周 / 月 / 季 三频率切换
10. **结论** — 6 段总结卡 + 印章

### 存档版本 (`pages/archive/a_share_2025_research.html`)

基于 2025 全年总结文档生成的早期版本（9 章正文 + 第 拾 章 2026 H1 监测点）。保留作为 2025-vintage 快照与时序对照参考。

## 数据来源

- **主版本**：`A股市场过去一年板块、行业回报与分析.md`（统计区间 2025-05 → 2026-04，原始引用 Wind、东方财富、券商研报等）
- **存档**：`中国A股市场研究.md` + `A股ETF投资研究报告生成.docx`（2025 全年口径）

## Tech

页面使用 CDN 加载 Chart.js 与 Noto Sans / Serif SC，无构建步骤。直接在浏览器打开 `index.html` 即可使用。
中式金融配色 — 红涨绿跌、深蓝顶栏、烫金分隔。
