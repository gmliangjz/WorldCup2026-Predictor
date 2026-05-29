<p align="center">
  <img src="docs/banner.png" alt="2026 World Cup Predictor" width="720">
</p>

<h1 align="center">2026 World Cup Predictor</h1>
<p align="center">
  <em>单文件 HTML · 48 队完整模拟 · 香槟金海报分享</em><br>
  <em>Single-file HTML · 48-team full simulation · champagne-gold poster export</em>
</p>

<p align="center">
  <a href="https://worldcup-jizhengliang.netlify.app/"><img src="https://img.shields.io/badge/demo-live-success?style=flat-square"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-blue?style=flat-square"></a>
  <img src="https://img.shields.io/badge/build-single--file-orange?style=flat-square">
  <img src="https://img.shields.io/badge/i18n-中文%20%2B%20English-purple?style=flat-square">
  <img src="https://img.shields.io/badge/dependencies-2%20CDN-lightgrey?style=flat-square">
</p>

<p align="center">
  <a href="https://worldcup-jizhengliang.netlify.app/"><b>🌐 Live Demo</b></a> ·
  <a href="#中文">中文</a> ·
  <a href="#english">English</a>
</p>

<p align="center">
  <img src="docs/screenshot-poster.png" alt="Champion poster" width="280">
  <img src="docs/screenshot-bracket.png" alt="Knockout bracket" width="280">
  <img src="docs/screenshot-leaderboard.png" alt="Top scorers" width="280">
</p>

---

## 中文

一个用单文件 HTML 实现的 2026 FIFA 世界杯预测器。从小组赛模拟到决赛，自动统计射手榜和助攻榜，最后导出一张深墨绿 + 香槟金的"冠军预测海报"用于分享。

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
- **零外部依赖（除 2 个 CDN）**：html2canvas + canvas-confetti，单文件离线也能跑

### 🚀 快速开始

```bash
# 1. 克隆
git clone https://github.com/<your-username>/worldcup-2026-predictor.git

# 2. 双击 index.html，或用任意静态服务器
python -m http.server 8000
# 或
npx serve
```

或直接访问 **[Live Demo](https://worldcup-jizhengliang.netlify.app/)**。

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

### 📝 五档冠军解说词（原创致敬）

每档冠军对应一段原创结束语，致敬中国体育解说的诗化传统。**请注意：这些是原创仿写，不是任何具体解说员作品的引用。**

| 档位 | 冠军候选 | 中文 | English |
|---|---|---|---|
| **传统豪门** | 法/西/阿/英/葡/巴/德 | *我自山峰而下，犹未见来人。* | *Down from the mountain heights I came, yet saw no soul approaching.* |
| **黄金一代** | 荷/比/克/摩/乌/哥/日 | *「差一点」是这一代人最熟悉的三个字……* | *For a generation that lived in the word 'almost' — 'almost' ends tonight.* |
| **黑马之路** | 美/瑞士/挪威等 | *足球的伟大之处，正是它不肯臣服于任何排行榜……* | *The greatness of football lies precisely in its refusal to bow to any ranking…* |
| **冷门传说** | 沙/卡/埃/波黑/巴拿马等 | *他们用九十分钟，让所有的预言安静下来……* | *Ninety minutes silenced every prediction…* |
| **人间童话** | 海地/库拉索/佛得角 | *这些从未出现在任何冠军预测里的名字……* | *Names that never appeared in any forecast…* |

### 🙏 致谢

- 国旗资源：[FlagCDN](https://flagcdn.com/)（CC0）
- 球员头像：Wikipedia REST API
- 海报渲染：[html2canvas](https://html2canvas.hertzen.com/) by [niklasvh](https://github.com/niklasvh)
- 庆祝效果：[canvas-confetti](https://github.com/catdad/canvas-confetti) by [catdad](https://github.com/catdad)
- 球员数据：截至 2024-2025 国家队大名单 snapshot（2026 开赛前会更新）
- 解说词文案：**原创致敬中国体育解说传统**，非任何具体解说员作品引用

### 🗺 路线图

- [x] 完整 48 队 FIFA 2026 赛制
- [x] 528 球员花名册 + 8 档位置分类
- [x] 强度档位 + 冷门上限算法
- [x] 香槟金分享海报（1080×1620）
- [x] 5 档原创冠军解说词
- [x] 中英双语 + 浅/深主题
- [ ] 分享 URL 携带预测 state（朋友扫码看你的预测）
- [ ] 历史预测记录（保存最近 5 次）
- [ ] 2026 临开赛球员名单更新
- [ ] PWA 支持（加到主屏幕）
- [ ] 接入真实赛果 API（2026 开赛后）

### 📄 License

MIT — 详见 [LICENSE](LICENSE)。

---

## English

A single-file HTML simulator for the 2026 FIFA World Cup. Predict from group stage to final, generate a champagne-gold champion poster, share with friends.

**No npm install, no build pipeline, no backend** — just open `index.html`.

### ✨ Features

- **All 48 teams under FIFA 2026 format**: 12 groups × 4 teams + 8 best-third advancement, with the new H2H-first tie-breaker rule
- **528 real player roster**: 48 teams × 11 players, classified into 8 positions (ST / W / AM / CM / DM / FB / CB / GK)
- **Strength-tier engine + upset cap**: 5-tier team strength with auto-weighted scoring; prevents unrealistic blowouts like "Saudi 5-1 Brazil"
- **Position-weighted goal distribution**: strikers score, attacking mids assist — matches real football roles
- **Manual / semi-auto / full random**: every score input is yours to control, or one-click randomize everything
- **Top scorers + assists**: leaderboard tallies your predictions, top 20 with Wikipedia headshots
- **Champion path reveal**: post-final animation lights up R32 → Final progressively in gold + confetti
- **Champagne-gold share poster**: 1080×1620 PNG, deep-forest-green base + champagne gold, 5-tier original commentary
- **Bilingual i18n**: full Chinese / English toggle covering UI, team names, player names, and tagline
- **Light / dark theme**: follows system or manual toggle
- **localStorage persistence**: close the browser, predictions remain
- **Responsive**: mobile / 1080p / desktop breakpoints

### 🚀 Quick Start

Open `index.html`. That's it. Or:

```bash
git clone https://github.com/<your-username>/worldcup-2026-predictor.git
cd worldcup-2026-predictor
python -m http.server 8000   # or: npx serve
```

Or visit the **[Live Demo](https://worldcup-jizhengliang.netlify.app/)**.

### 🛠 Tech Stack

Plain HTML / CSS / Vanilla JS + 2 CDN libraries:
- [html2canvas](https://html2canvas.hertzen.com/) — poster screenshot
- [canvas-confetti](https://github.com/catdad/canvas-confetti) — celebration burst

Resources from Wikipedia REST API (player photos) and FlagCDN (flags).

### 📐 Algorithm

See [中文 § 算法说明](#📐-算法说明) for a detailed breakdown. TL;DR:
- Each team gets a 1-5 strength tier
- Score sampling uses a fixed probability table with strength-delta boost / nerf
- Knockout upsets (≥ 2-tier difference) get capped to realistic scorelines (1-0 / 2-0 / 2-1)
- Group ranking follows the **2026 FIFA tie-breaker** (H2H before goal difference — different from 2022!)

### 📝 Champion Taglines (Original Tribute)

Each champion tier triggers an original Chinese commentary-style tagline, with parallel English version. **These are original tributes to Chinese sports-broadcasting tradition — not quotations from any specific commentator.**

See the table in [中文 § 五档冠军解说词](#-五档冠军解说词原创致敬).

### 🙏 Credits

- Flags: [FlagCDN](https://flagcdn.com/) (CC0)
- Player photos: Wikipedia REST API
- Poster rendering: [html2canvas](https://html2canvas.hertzen.com/)
- Celebration: [canvas-confetti](https://github.com/catdad/canvas-confetti)
- Player rosters: snapshot of 2024-2025 national team squads (will be refreshed before 2026 kick-off)
- Commentary: **original tribute to Chinese sports broadcasting**, not any specific commentator's work

### 📄 License

MIT — see [LICENSE](LICENSE).

---

<p align="center">⚽ Made for football fans, written with care.</p>
