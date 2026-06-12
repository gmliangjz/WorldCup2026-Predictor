<p align="center">
  <img src="docs/banner.png" alt="2026 World Cup Predictor" width="720">
</p>

<h1 align="center">2026 World Cup Predictor</h1>
<p align="center">
  <em>Single-file HTML · 48-team full simulation · champagne-gold poster export</em><br>
  <em>单文件 HTML · 48 队完整模拟 · 香槟金海报分享</em>
</p>

<p align="center">
  <b>No signup</b> · <b>Full 48-team 2026 format</b> · <b>Shareable champion poster</b>
</p>

<p align="center">
  <a href="https://gmliangjz.github.io/WorldCup2026-Predictor/"><img src="https://img.shields.io/badge/demo-live-success?style=flat-square"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-blue?style=flat-square"></a>
  <img src="https://img.shields.io/badge/build-single--file-orange?style=flat-square">
  <img src="https://img.shields.io/badge/i18n-English%20%2B%20中文-purple?style=flat-square">
  <img src="https://img.shields.io/badge/backend-none-success?style=flat-square">
</p>

<p align="center">
  <a href="https://gmliangjz.github.io/WorldCup2026-Predictor/"><b>🌐 Live Demo</b></a> ·
  <a href="#english">English</a> ·
  <a href="#中文">中文</a>
</p>

<p align="center"><sub>⚠️ Unofficial fan-made project · not affiliated with FIFA or the FIFA World Cup™ · 非官方粉丝作品，与 FIFA 无关</sub></p>

<p align="center">
  <img src="docs/demo.gif" alt="Champion reveal — gold path + confetti celebration" width="720">
</p>

<p align="center">
  <img src="docs/screenshot-poster.png" alt="Champion share poster" width="320">
</p>

<p align="center">
  <img src="docs/screenshot-bracket.png" alt="Knockout bracket (dark mode)" width="760">
</p>

<p align="center">
  <img src="docs/screenshot-leaderboard.png" alt="Top scorers & assists" width="760">
</p>

---

## English

A single-file HTML simulator for the 2026 FIFA World Cup. Predict from the group stage to the final, watch the champion reveal with confetti, then export a deep-forest-green + champagne-gold "champion poster" to share.

**No npm install, no build pipeline, no backend** — just open `index.html`.

### ✨ Features

- **All 48 teams under the FIFA 2026 format**: 12 groups × 4 + 8 best-third advancement, with the new H2H-first tie-breaker
- **528 real players**: 48 teams × 11, classified into 8 positions (ST / W / AM / CM / DM / FB / CB / GK)
- **Strength-tier engine + upset cap**: 5 strength tiers with auto-weighted scoring; prevents unrealistic blowouts like "Saudi 5-1 Brazil"
- **Position-weighted goals**: strikers score, attacking mids assist — matches real on-pitch roles
- **Manual / semi-auto / full random**: type every score, click to randomize one match, or randomize everything at once
- **Top scorers + assists**: auto-tallied from your predictions, top 20 with Wikipedia headshots
- **Champion path reveal**: after the final, R32 → Final lights up progressively in gold + a confetti burst
- **Champagne-gold share poster**: 1080×1620 PNG, deep-forest-green base + champagne gold, with a 5-tier original tagline
- **Bilingual i18n**: one-tap toggle covering UI, team names, player names, and taglines
- **Light / dark theme**: follows the system or toggles manually
- **localStorage autosave**: close the browser, your prediction stays
- **Responsive**: mobile / 1080p / desktop breakpoints
- **Live scoring vs real results**: now that the cup is underway, the app pulls real scores from ESPN's public JSON feed (no key, fetched client-side) and grades your bracket in real time
- **Core engine runs offline**: the simulation is pure front-end with no backend; the poster/confetti use 2 CDNs (html2canvas / canvas-confetti), and photos/flags are fetched at runtime (Wikipedia / FlagCDN)

### 🚀 Quick Start

```bash
# 1. Clone
git clone https://github.com/gmliangjz/WorldCup2026-Predictor.git

# 2. Open index.html, or serve it statically
cd WorldCup2026-Predictor
python -m http.server 8000   # or: npx serve
```

Or just open the **[Live Demo](https://gmliangjz.github.io/WorldCup2026-Predictor/)**.

### 🛠 Tech Stack

| Layer | Tool |
|---|---|
| Core | HTML / CSS / Vanilla JS (no framework) |
| Poster render | [html2canvas](https://html2canvas.hertzen.com/) 1.4.1 |
| Celebration | [canvas-confetti](https://github.com/catdad/canvas-confetti) |
| Player photos | Wikipedia REST API |
| Flags | [FlagCDN](https://flagcdn.com/) |
| QR code | hand-rolled CSS-grid QR matrix |

### 📐 Algorithm

**Strength tiers** (`STRENGTH`, 1–5):
```
Tier 5: France / Spain / Argentina / England / Portugal / Brazil / Germany
Tier 4: Netherlands / Belgium / Croatia / Morocco / Uruguay / Colombia / Japan
Tier 3: USA / Mexico / Canada / Switzerland / Korea / Sweden / Türkiye … (20 teams)
Tier 2: Saudi Arabia / Qatar / Egypt / Bosnia / Panama … (11 teams)
Tier 1: Haiti / Curaçao / Cape Verde
```

**Score sampling** (`rnd`):
- Base probability table `WW = [0,0,0,0,1,1,1,1,1,1,2,2,2,2,3,3,4,5]` (mostly 0–2 goals, occasionally 3–5)
- Strength-delta weighting: `boostP = |Δ| × 0.20`, `nerfP = |Δ| × 0.12`
- Knockout forces a decisive result; the group stage allows draws

**Upset cap** (`applyUpsetCap`, knockout only):
- When a weak team (≥ 2-tier gap) wins, the scoreline is rewritten to 1-0 / 2-0 / 2-1
- Keeps the upset alive while avoiding unrealistic blowouts

**Group ranking** (`rankGroup`) under the 2026 FIFA rules:
1. Points → 2. **H2H points** (changed from 2022!) → 3. H2H goal difference → 4. H2H goals → 5. overall GD → 6. overall goals

> ⚠️ FIFA reordered the 2026 tie-breakers, moving head-to-head ahead of overall goal difference — the key change from 2022.

### 📊 Scoring (live during the tournament)

This isn't just for fun — real results stream in from ESPN's public feed and your bracket is scored against reality as the cup unfolds:

| Correct call | Points |
|---|---|
| Group result (W/D/L direction) | 3 |
| Exact group scoreline (bonus) | +2 |
| Team correctly reaching R16 | 5 / team |
| Team correctly reaching QF | 8 / team |
| Team correctly reaching SF | 12 / team |
| Team correctly reaching Final | 16 / team |
| Correct 3rd place | 15 |
| Correct runner-up | 20 |
| **Correct champion** | **30** |

> Real results are fetched client-side from ESPN's public scoreboard API (no key, CORS-open) into `ACTUAL_RESULTS`, then `scorePrediction()` grades your bracket — group matches slot-by-slot, knockout rounds by which teams actually advanced. Scores update every time you open the page.

### 📝 Champion Taglines (Original Tribute)

Each champion tier triggers an original Chinese commentary-style tagline, with a parallel English version. **These are original tributes to the Chinese sports-broadcasting tradition — not quotations from any specific commentator.**

| Tier | Champions | English | 中文 |
|---|---|---|---|
| **Traditional Powerhouse** | FR / ES / AR / EN / PT / BR / DE | *Down from the mountain heights I came, yet saw no soul approaching.* | *我自山峰而下，犹未见来人。* |
| **Golden Generation** | NL / BE / HR / MA / UY / CO / JP | *For a generation that lived in the word 'almost' — 'almost' ends tonight.* | *「差一点」是这一代人最熟悉的三个字……* |
| **Dark Horse** | USA / Switzerland / Norway … | *The greatness of football lies precisely in its refusal to bow to any ranking…* | *足球的伟大之处，正是它不肯臣服于任何排行榜……* |
| **Underdog Legend** | SA / QA / EG / Bosnia / Panama … | *Ninety minutes silenced every prediction…* | *他们用九十分钟，让所有的预言安静下来……* |
| **Fairy Tale** | Haiti / Curaçao / Cape Verde | *Names that never appeared in any forecast…* | *这些从未出现在任何冠军预测里的名字……* |

### 🗺 Roadmap

- [x] Full 48-team FIFA 2026 format
- [x] 528-player roster + 8-position classification
- [x] Strength tiers + upset cap
- [x] Champagne-gold share poster (1080×1620)
- [x] 5 original champion taglines
- [x] Bilingual + light/dark themes
- [x] Shareable prediction URL (friends scan to see yours)
- [x] Prediction history (last 5)
- [x] Live result scoring via ESPN's public API (shipped on matchday 2)
- [ ] Pre-tournament squad refresh (2026)
- [ ] PWA support (add to home screen)

### 🙏 Credits

- Flags: [FlagCDN](https://flagcdn.com/) (CC0)
- Player photos: Wikipedia REST API
- Poster rendering: [html2canvas](https://html2canvas.hertzen.com/) by [niklasvh](https://github.com/niklasvh)
- Celebration: [canvas-confetti](https://github.com/catdad/canvas-confetti) by [catdad](https://github.com/catdad)
- Player rosters: snapshot of 2024-2025 national-team squads (refreshed before 2026 kick-off)
- Commentary: **original tribute to Chinese sports broadcasting**, not any specific commentator's work

### 📄 License

MIT — see [LICENSE](LICENSE). Third-party assets (flags, photos, taglines): [NOTICE](NOTICE.md).

---

## 中文

一个用单文件 HTML 实现的 2026 FIFA 世界杯预测器。从小组赛模拟到决赛，决赛揭晓时金色路径逐轮点亮 + 五彩礼花，最后导出一张深墨绿 + 香槟金的"冠军预测海报"用于分享。

**没有 npm install，没有 build pipeline，没有后端**——双击 `index.html` 就能跑。

### ✨ 功能特性

- **48 队完整 FIFA 2026 新赛制**：12 组 × 4 队 + 8 个三档晋级，按 FIFA 2026 官方的 H2H 优先 tie-breaker 规则
- **528 名球员真实花名册**：48 队 × 11 人，含 8 档位置分类（中锋 / 边锋 / 前腰 / 中前卫 / 后腰 / 边卫 / 中卫 / 门将）
- **强度档位 + 冷门上限算法**：5 档球队强度，强弱差额自动加权；防止"沙特 5-1 巴西"这种不真实大比分爆冷
- **位置加权进球分布**：中锋多进球、攻中多助攻——按真实足球场上分工
- **手动 / 半自动 / 全随机**：你的预测你做主，每场比分可以全手填、点几下随机、或者一键随机全部
- **射手榜 + 助攻榜**：自动统计你预测中的进球者，前 20 名带球员头像（Wikipedia API）
- **冠军路径动画**：决赛揭晓后，从 32 强到决赛逐轮金色高亮 + 五彩纸屑庆祝
- **香槟金分享海报**：1080×1620 PNG，深墨绿底 + 香槟金，五档对应五段原创解说词
- **中英双语 i18n**：右上角一键切换，UI / 球队名 / 球员名 / 文案全套双语
- **浅色 / 深色主题**：跟随系统或手动切换
- **localStorage 自动存档**：关闭浏览器不丢预测
- **响应式适配**：移动端 / 1080p / 桌面三段断点
- **真实赛果实时计分**：开赛后自动拉取真实比分（ESPN 公开 JSON 接口，免 key、纯前端 fetch），实时给你的预测打分
- **核心引擎可离线**：模拟逻辑纯前端、无后端；海报与庆祝用 2 个 CDN（html2canvas / canvas-confetti），球员头像与国旗在运行时走外部资源（Wikipedia / FlagCDN）

### 🚀 快速开始

```bash
# 1. 克隆
git clone https://github.com/gmliangjz/WorldCup2026-Predictor.git

# 2. 双击 index.html，或用任意静态服务器
cd WorldCup2026-Predictor
python -m http.server 8000   # 或：npx serve
```

或直接访问 **[Live Demo](https://gmliangjz.github.io/WorldCup2026-Predictor/)**。

### 🛠 技术栈

| 类别 | 工具 |
|---|---|
| 核心 | HTML / CSS / Vanilla JS（无框架） |
| 海报渲染 | [html2canvas](https://html2canvas.hertzen.com/) 1.4.1 |
| 庆祝效果 | [canvas-confetti](https://github.com/catdad/canvas-confetti) |
| 球员头像 | Wikipedia REST API |
| 国旗资源 | [FlagCDN](https://flagcdn.com/) |
| 二维码 | 纯 CSS Grid 自制 QR matrix |

### 📐 算法说明

**强度档位**（`STRENGTH`，1-5 档）：
```
5 档：法/西/阿/英/葡/巴/德
4 档：荷/比/克/摩/乌/哥/日
3 档：美/墨/加/瑞士/韩/瑞典/土等 20 队
2 档：沙/卡/埃/波黑/巴拿马等 11 队
1 档：海地/库拉索/佛得角
```

**比分采样**（`rnd` 函数）：
- 基础概率表 `WW = [0,0,0,0,1,1,1,1,1,1,2,2,2,2,3,3,4,5]`（多数 0-2 球，偶尔 3-5 球）
- 强弱差额加权：`boostP = |Δ| × 0.20`、`nerfP = |Δ| × 0.12`
- 淘汰赛强制非平局；小组赛允许平局

**冷门上限**（`applyUpsetCap`，仅淘汰赛）：
- 当弱队（实力差 ≥ 2 档）赢球，比分会被改写成 1-0 / 2-0 / 2-1
- 保留冷门概率，但避免"沙特 5-1 巴西"这种不真实场景

**小组赛排名**（`rankGroup`）按 FIFA 2026 新规：
1. 积分 → 2. **H2H 积分**（与 2022 不同！）→ 3. H2H 净胜球 → 4. H2H 进球 → 5. 总净胜球 → 6. 总进球

> ⚠️ FIFA 在 2026 改了 tie-breaker 顺序，把 H2H 移到总净胜球之前。这是与 2022 规则的关键差异。

### 📊 计分机制（赛中实时）

预测不只是娱乐——真实比分从 ESPN 公开接口实时流入，你的预测随赛事推进自动对照打分：

| 命中项 | 得分 |
|---|---|
| 小组赛胜 / 平 / 负方向正确 | 3 |
| 小组赛比分完全正确（额外加成） | +2 |
| 正确把球队送进 16 强 | 5 / 队 |
| 正确把球队送进 8 强 | 8 / 队 |
| 正确把球队送进 4 强 | 12 / 队 |
| 正确把球队送进决赛 | 16 / 队 |
| 季军命中 | 15 |
| 亚军命中 | 20 |
| **冠军命中** | **30** |

> 真实赛果由前端直接从 ESPN 公开 scoreboard 接口拉取（免 key、CORS 开放）填入 `ACTUAL_RESULTS`，再由 `scorePrediction()` 打分——小组赛逐场对照，淘汰赛按实际晋级球队集合计算。每次打开页面自动刷新。

### 📝 五档冠军解说词（原创致敬）

每档冠军对应一段原创结束语，致敬中国体育解说的诗化传统。**请注意：这些是原创仿写，不是任何具体解说员作品的引用。**

| 档位 | 冠军候选 | 中文 | English |
|---|---|---|---|
| **传统豪门** | 法/西/阿/英/葡/巴/德 | *我自山峰而下，犹未见来人。* | *Down from the mountain heights I came, yet saw no soul approaching.* |
| **黄金一代** | 荷/比/克/摩/乌/哥/日 | *「差一点」是这一代人最熟悉的三个字……* | *For a generation that lived in the word 'almost' — 'almost' ends tonight.* |
| **黑马之路** | 美/瑞士/挪威等 | *足球的伟大之处，正是它不肯臣服于任何排行榜……* | *The greatness of football lies precisely in its refusal to bow to any ranking…* |
| **冷门传说** | 沙/卡/埃/波黑/巴拿马等 | *他们用九十分钟，让所有的预言安静下来……* | *Ninety minutes silenced every prediction…* |
| **人间童话** | 海地/库拉索/佛得角 | *这些从未出现在任何冠军预测里的名字……* | *Names that never appeared in any forecast…* |

### 🗺 路线图

- [x] 完整 48 队 FIFA 2026 赛制
- [x] 528 球员花名册 + 8 档位置分类
- [x] 强度档位 + 冷门上限算法
- [x] 香槟金分享海报（1080×1620）
- [x] 5 档原创冠军解说词
- [x] 中英双语 + 浅/深主题
- [x] 分享 URL 携带预测 state（朋友扫码看你的预测）
- [x] 历史预测记录（保存最近 5 次）
- [x] 接入真实赛果实时计分（ESPN 公开接口，开赛第 2 天上线）
- [ ] 2026 临开赛球员名单更新
- [ ] PWA 支持（加到主屏幕）

### 📄 License

MIT — 详见 [LICENSE](LICENSE)。第三方素材（旗帜 / 头像 / 解说词）声明见 [NOTICE](NOTICE.md)。

---

<p align="center">⚽ Made for football fans, written with care.</p>
