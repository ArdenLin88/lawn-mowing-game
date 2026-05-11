# Design System — Lawn Mowing Game

> **Visual Thesis**: 一頁 1480 年的羊皮紙手稿，墨水未乾，騎士只是疲憊的鐵人，骷髏不停從紙裡長出來。

## Product Context
- **What this is**: Top-down hack-and-slash roguelite (Vampire Survivors-like). 騎士主角 vs 骷髏大軍，計時生存 + 升級選擇。
- **Who it's for**: 行動裝置與桌機玩家，碎片時間打 3-10 分鐘一局。
- **Space/industry**: 暗黑奇幻 ARPG / Roguelike。同類: Vampire Survivors, Brotato, Hades, Diablo IV, Darkest Dungeon。
- **Project type**: 單檔 HTML5 Canvas 遊戲 (vanilla JS, ~2900 lines)，部署於 Vercel。
- **Repo**: [ArdenLin88/lawn-mowing-game](https://github.com/ArdenLin88/lawn-mowing-game)

---

## Aesthetic Direction

- **Direction**: **Engraved Woodcut × Witchlight**（雕版 × 鬼火）
- **Decoration level**: Intentional — HUD 與技能卡有手繪木刻邊飾，但動作畫面中央乾淨
- **Mood**: 沉默、凝重、虔誠帶有不祥感。玩家應感到「打開了一本不該翻的書」。**不是** epic / 不是 hype / 不是 cyberpunk。
- **Reference influences**:
  - Hans Holbein《死神之舞》木刻畫（Dance of Death, 1538）── 平面、線條、骷髏與騎士並陳
  - Albrecht Dürer 銅版畫《騎士、死神與惡魔》(Knight, Death and the Devil, 1513)
  - Mike Mignola《Hellboy》pen & ink 漫畫風（Hades 的視覺源頭之一）
  - Darkest Dungeon 暖羊皮紙色調（避免 dead gray/black）

**核心洞察**：Canvas 2D 的「平面 / 鋒利邊緣 / 線條本位」是限制 → 但木刻版畫天生就是這個語言。`ctx.fillRect` + `ctx.strokeText` 是 1480 年印刷工的原生工具。**揚長避短**。

---

## Typography

### Fonts
| Role | Font | 用途 | 來源 |
|------|------|------|------|
| **Display** | `Pirata One` | 標題、升級橫幅、傷害數字、結算畫面 | [Google Fonts](https://fonts.google.com/specimen/Pirata+One) |
| **Body** | `IM Fell English` | HUD 標籤、技能描述、tooltip、選單文字 | [Google Fonts](https://fonts.google.com/specimen/IM+Fell+English) |
| **Code/Debug** | `Courier New` (system) | hex 值、debug overlay | system |

### 載入方式（HTML head）
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=IM+Fell+English:ital@0;1&family=Pirata+One&display=swap" rel="stylesheet">
```

### Canvas 字體字串
```javascript
ctx.font = '64px "Pirata One", cursive';        // 標題
ctx.font = '32px "Pirata One", cursive';        // 中標 / 升級數字
ctx.font = 'italic 18px "IM Fell English", serif'; // body 強調
ctx.font = '16px "IM Fell English", serif';     // 一般 body
ctx.font = '14px "IM Fell English", serif';     // HUD 標籤 / 小字
```

### Scale
| Level | Size | Use |
|-------|------|-----|
| Display | 56-64px | 開場標題、結算 |
| H1 | 40px | 升級畫面標題 |
| H2 | 28-32px | 大魔王名 / 章節 |
| H3 | 22px | 技能卡名稱 |
| Body+ | 18px | 強調 body |
| Body | 16px | 一般文字 |
| UI | 14px | HUD 數值 / 標籤 |
| Caption | 12px | 稀有度標籤 / 小字 |
| Mono | 12px | hex / debug |

### 字體紀律
- **永不**用 Inter / Roboto / Arial / Helvetica / Open Sans 作主字體
- **永不**用 Comic Sans / Papyrus / Lobster / Impact
- 字體載入完成前用 `serif` fallback (不要 sans-serif，會風格不一致)

---

## Color

- **Approach**: **Restrained**（配給制）— 80% 畫面只有 bg + ink + muted。彩色是聖物，不亂用。

### Palette · 10 stops

| Token | Hex | 中文名 | 用途 |
|-------|-----|--------|------|
| `--bg` | `#1A1612` | 羊皮夜 | 主背景。**永不**用純黑 (#000)。 |
| `--surface` | `#2A231C` | 羊皮陰影 | 卡片、面板、選單底色 |
| `--ink` | `#E8DCC4` | 橡膽墨 | **所有文字、線條、邊框**。**永不**用純白 (#FFF)。 |
| `--muted` | `#7A6A52` | 蝕紙黃 | 次要文字、停用狀態、格線、副框 |
| `--hero` | `#6E7480` | 冷鐵 | 騎士主角（冷藍灰，不是金色） |
| `--enemy` | `#D4C8A8` | 骨粉 | 骷髏（暖灰，不是死白） |
| `--blood` | `#7B1A1A` | 牛血 | HP 條、傷害數字、屍跡。乾血色不是純紅。 |
| `--xp-glow` | `#C8941A` | 聖物金 | XP、升級、稀有貨幣、buff 外環 |
| `--crit` | `#5FA89C` | 鬼火青 | 爆擊、魔法、debuff 外環 |
| `--warning` | `#C44B1A` | 灰燼橘 | 低血 (<30%) 邊緣 vignette |

### 配色規則
- 任何畫面 ≥ 80% 像素只能用 `bg + surface + ink + muted` 四色
- 飽和色（hero / enemy / blood / xp-glow / crit / warning）只在語義時刻出現
- 一個畫面同時最多 3 種飽和色（除 boss 戰場景）
- **永不用紫色 (#A0XX以紫到 #FFXX 紫)** — 紫色是 generic-fantasy-asset-pack syndrome 的萬用 tell

### Day Mode (Vellum, 可選)
作為彩蛋 / accessibility 模式：bg=#E8DCC4, ink=#1A1612, surface=#D4C8A8, hero=#4A4F58, enemy=#5C5444。其他飽和色不變。

---

## Spacing

- **Base unit**: 8px（觸控友善）
- **Inline tight**: 4px（標籤對數值內距）
- **Density**: 中世紀手稿般偏密

### Scale
| Token | Px | Use |
|-------|----|----|
| 2xs | 2 | 邊框內距 |
| xs | 4 | 標籤對數值 |
| sm | 8 | HUD 元素間距 |
| md | 16 | 卡片內距 / 段落間距 |
| lg | 24 | section 間距 |
| xl | 32 | 大 section 間距 |
| 2xl | 48 | 開場頁 / 結算 |

---

## Layout

- **Canvas 解析度**: 1100 × 600 (16:9 接近比例 1.83)
- **行動橫向**：CSS 拉滿 vw/vh，移除 border 與 box-shadow
- **HUD 定位**：四角錨點（左上：等級/擊殺/計時、右上：HP、底部：EXP 條 + 操作提示、底部兩側：搖桿）
- **Boss 血條**：螢幕頂部置中
- **升級選單**：螢幕中央 modal，3 張橫排卡片
- **邊框**：1-2px sharp `--muted`，**永遠尖角**，**永不**圓角 > 2px

### 階層原則
透過「**反相 + 線條密度 + 字體大小**」三件事建立階層 — **不靠顏色發光**。重要資訊用反相羊皮紙面板（淺底深字）：與所有暗黑奇幻遊戲反過來，反而醒目。

---

## Motion

- **Approach**: **Minimal-functional** — woodblock 印刷不會動，但允許 snap-cuts。
- **Easing**: 多用 `linear` 或極短 `ease-out`，**避免** `ease-in-out` 的「軟」感

### Duration
| Type | ms | Use |
|------|----|----|
| micro | 50-100 | 爆擊閃 / 受傷反應 |
| short | 150-250 | 數字飛字 / 卡片切換 |
| medium | 400-700 | 升級 ink-bloom |
| long | 1500-2000 | 開場 / 結算 |

### Effect Spec
| Event | Effect |
|-------|--------|
| 一般傷害 | 數字 `IM Fell English` italic 18px, color blood, 上飄 30px / 800ms / fade |
| 爆擊 | 數字 `Pirata One` 26px, color crit, 100ms 短閃 + 上飄 40px / 1200ms |
| 治療 | 數字 `IM Fell English` 18px, color xp-glow, 上飄 / fade |
| Miss | 字 `MISS`, color enemy, 上飄 / fade |
| 升級 | 中央 ink-bloom（暗墨擴散圓 800ms）→ 收回時 xp-glow 環圈 + 文字 `ASCEND` |
| 低血 (<30%) | 螢幕邊緣 ember vignette `--warning`，1Hz 脈動 |
| 屍體 | 不留血池粒子。留 oxblood ink-stain（橢圓污跡，5 秒淡出）|
| XP 進度 | xp-glow 沿條流動，**不要** neon glow |
| 鏡頭震動 | 不超過 4px / 80ms（爆擊 + 大魔王重擊） |

### 不允許的動效
- ❌ 持續 floating bobbing animation（玩家、敵人不要無謂上下浮動）
- ❌ Neon RGB 拖曳尾跡
- ❌ 螢幕全反白超過 80ms
- ❌ Gaussian blur / shadowBlur

---

## Iconography

- **武器圖示**：黑色剪影 + ink 描邊 1px，仿 Holbein woodcut 武器（劍、斧、鏈枷、戰鎚、十字弓）
- **技能圖示**：用 hand-coded canvas path 預烘焙簡單形狀；**不用** emoji，**不用** vector flat
- **buff/debuff badges**：薄圓 + 1px ink 邊框 + 線描符號；buff 外環 xp-glow，debuff 外環 crit
- **稀有度系統**（重點 RISK）：**用線條密度而非顏色**
  - **Common**：細線單框
  - **Rare**：雙線框 + 角落 ❦ 渦旋裝飾
  - **Legendary**：雙骷髏龕框 ☠ ☠ + 雙重外框（聖徒 niche）

---

## Canvas Implementation Notes

> 這段是 canvas 遊戲特有，非典型 web design system 內容。

### Hex 值在 Canvas
直接用 hex string 即可：`ctx.fillStyle = '#7B1A1A';`

### 仿 Woodblock 偏移陰影
不要 `shadowBlur`。改成：先畫一個 2px 偏移的 surface 矩形作陰影底，再畫主矩形。
```javascript
// 偏移木刻陰影
ctx.fillStyle = 'rgba(26, 22, 18, 0.6)';
ctx.fillRect(x + 2, y + 2, w, h);
ctx.fillStyle = '#2A231C';
ctx.fillRect(x, y, w, h);
ctx.strokeStyle = '#7A6A52';
ctx.lineWidth = 1;
ctx.strokeRect(x, y, w, h);
```

### 受傷視覺反饋（取代 60ms 全螢幕反相）
1. 玩家 sprite 80ms `globalAlpha = 0.5` desaturate pulse
2. 螢幕邊緣 ember vignette 強度 +20% / 200ms

### 文字描邊（Canvas）
為了讓 ink 字在飽和色上仍清晰，重要文字用 stroke-then-fill：
```javascript
ctx.lineWidth = 3;
ctx.strokeStyle = '#1A1612';
ctx.strokeText(text, x, y);
ctx.fillStyle = '#E8DCC4';
ctx.fillText(text, x, y);
```

### 字體載入時機
Google Fonts 非同步，遊戲開場前用 `document.fonts.ready` 等載入完才開始繪製，否則第一秒會 fallback 成 serif。

```javascript
await document.fonts.ready;
// 然後 startGame()
```

---

## Anti-Slop Rules（lint 等級）

違反 = 必改。

1. **NO purple anywhere ever** — 紫色 = generic asset-pack tell
2. **NO border-radius > 2px** — 全部尖角
3. **NO shadowBlur / drop-shadow blur** — 偏移實心矩形仿 woodblock
4. **NO emoji icons in HUD** — 用 hand-coded path 線條符號
5. **NO neon glow particles** — 升級用 ink-bloom，XP 用 gold sparkle
6. **NO #FFFFFF / #000000** — 用 ink (#E8DCC4) / bg (#1A1612)
7. **NO 飽和色任意混用** — 飽和色只能從 blood / xp / crit / warning 四選一
8. **NO sans-serif body** — IM Fell English 為主，fallback `serif`
9. **NO smooth bobbing animation** — 角色不要無謂浮動
10. **NO gradient buttons / cards** — flat color + 1px border + offset shadow

---

## Decisions Log

| Date | Decision | Rationale |
|------|----------|-----------|
| 2026-05-07 | Initial design system created (v1.0) | 由 `/design-consultation` 建立。研究參考 Hades / Diablo IV / Darkest Dungeon / Vampire Survivors，外加 Claude 子代理人獨立提案綜合。核心洞察：Canvas 2D 平面性原生對應木刻版畫，揚長避短。 |
| 2026-05-07 | 採用 Engraved Woodcut × Witchlight 方向 | 平衡了業界共識（暗黑奇幻護照色）與差異化（冷鐵騎士、骨粉骷髏、鬼火爆擊、線條密度稀有度）。 |
| 2026-05-07 | 字體 Pirata One + IM Fell English | 都是 Google Fonts，canvas 渲染清晰，period-appropriate，皆有 ink-bleed 不規則感。 |
| 2026-05-07 | 升級選單加「雙倍升級」機制（Phase 2.5） | 降低初始難度。每次升級至多 1 張卡標記為 `bonusLevel: 2`。機率隨等級遞減：Lv ≤3 20% / ≤7 10% / 之後 5%。視覺：2px 亮聖物金 `#E8C44A` 邊框 + 1px 聖物金 outer outline + 右上角 ×2 徽章。跟 rarity 正交（可疊 maxed / rare / legendary）。 |

---

## How to Update This Doc

更動視覺決策時：
1. 在這份 DESIGN.md 對應 section 修改
2. 在 Decisions Log 加一行（日期、決定、原因）
3. 預覽頁 [`design-preview.html`](design-preview.html) 同步更新（或刪除重生）
4. 對應改 [`index.html`](index.html) 的 canvas 繪製代碼

當有衝突時：以 DESIGN.md 為準。**先改文件，再改代碼。**
