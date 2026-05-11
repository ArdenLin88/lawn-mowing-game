# Lawn Mowing Game · BACKLOG

> 由 `/design-consultation` 啟動的視覺重構工程。設計聖經：[DESIGN.md](DESIGN.md)。
> 修改任何 UI / 視覺前先讀 DESIGN.md。

## 已完成

### Phase 1 · 基礎重構（2026-05-07）
- [x] HTML head 載入 Pirata One + IM Fell English（Google Fonts）
- [x] CSS 全替換（body / canvas / wrapper / joystick / 升級 overlay / skill-card）→ 雕版暖色
- [x] 加 `const COLORS` 與 `const FONTS` 常數
- [x] gameLoop 包進 `document.fonts.ready.then(...)`
- [x] `ctx.font` 全替換 34 處（≥20px bold → Pirata One，其他 → IM Fell English）
- [x] 主背景 `#16261A` → bg、純白 → ink、純亮金 → xp、純黑 alpha → bg alpha
- [x] 開場綠 `#4CAF50` → xp、結算紅 → warning、擊殺綠 `#88FF88` → 骨粉
- [x] 背景格線綠 → muted alpha
- [x] **Bug fix**: HP bar 健康色從聖物金回到 `blood → warning` 兩階紅
- [x] **Bug fix**: Boss bar 厚度 22 → 36px

### Phase 2 · HUD + 升級選單（2026-05-07）
- [x] SKILL_POOL 8 個技能加 `rarity` 欄位（common × 3 / rare × 3 / legendary × 2）
- [x] showUpgradeMenu 動態加 rarity class + `.card-rarity` 標籤
- [x] CSS `.skill-card.rare`（雙線 + ❦）+ `.skill-card.legendary`（雙重外框 + ☠ ☠）
- [x] HP bar / 擊殺面板 / 右上面板 全改尖角 + woodblock offset shadow + 1px muted 邊框
- [x] 右上面板 boss time pulse、字色、技能格邊框 對齊雕版色
- [x] EXP 條改尖角 + 深→亮聖物金漸層（保留進度光感）+ ink alpha pulse
- [x] Boss bar 改 `blood → warning` 漸層 + 1px warning 尖角邊框 + 描邊文字（移除 shadowBlur）
- [x] 灰色殘色清理（`#888` `#aaa` `#E8E8DC`）

---

## 已完成（接續）

### 雙倍升級選項（Phase 2.5，2026-05-07）
**目的**：偶爾在升級選單出現「升 2 級」選項，降低初始難度。

- [x] `pickUpgradeOptions` 每次至多挑 1 張卡標記為 `bonusLevel: 2`
- [x] 機率：玩家等級 ≤ 3 時 20% / ≤ 7 時 10% / 之後 5%
- [x] `applySkill` 接收 `times` 參數，連續呼叫 N 次 apply
- [x] showUpgradeMenu 對 `bonusLevel: 2` 卡加 `.skill-card.double` class
- [x] CSS `.skill-card.double`：邊框 2px 亮聖物金 `#E8C44A` + 右上角「×2」徽章
- [x] DESIGN.md Decisions Log 補一條（記錄這個機制與機率規則）
- [x] 跟 rarity 正交：`.skill-card.rare.double` `.skill-card.legendary.double` 都 work

---

## 已完成（接續）

### Phase 2.5 追加優化項目（2026-05-08）
- [x] 大魔王太脆了, 起碼要增加5倍的血條（250 HP），死後會再復活一次（50% HP + 復活特效）.
- [x] 不同怪物的經驗應該要不同：骷髏+1 / 殭屍+3 / 弓箭手+4 / 精英+6 / 大魔王+50，浮動文字顏色按 XP 值區分.

### Phase 3 · 角色 + 敵人 + 特效（2026-05-08）
- [x] 騎士主角配色：藍色漸層 → cold-iron flat（`#6E7480`）+ 1px ink 邊 + 木刻偏移陰影
- [x] 骷髏（一般）：眼睛改鬼火青（`#5FA89C`），移除 shadowBlur
- [x] 殭屍：眼睛改血紅（blood 色系），移除 shadowBlur
- [x] 精英骷髏：全面重繪 → bone-meal flat + 暗紅披風 + 血紅眼睛
- [x] 弓箭手：骨粉主體 + xp-glow 弓（`#C8941A`）
- [x] 大魔王：blood 底色 + 1px ink 邊 + 聖物金王冠，全部移除 shadowBlur
- [x] 移除全部剩餘 `shadowBlur`（騎士眼、骨框 aura、進化公告、結算標題、XP球、鬼火球、boss 王冠）
- [x] 結算 victory glow：金光 RadialGradient → ink-bloom + 聖物金雙環圈
- [x] 寶箱經驗球：藍色 `#88CCFF` → xp-glow 系列（大寶石 #C8941A / 中 #A07010 / 小 #7A6A52）
- [ ] 受傷反饋：玩家 80ms desaturate pulse（取代任何全螢幕反白）
- [ ] 傷害數字：normal = blood + IM Fell italic 18px
- [ ] 爆擊數字：crit witchfire（`#5FA89C`）+ Pirata One 26px + 100ms 短閃
- [ ] 升級特效：中央 ink-bloom 800ms（取代 `#FFD700` RadialGradient 金光）
- [ ] 低血 (<30%)：螢幕邊緣 ember vignette 1Hz 脈動
- [ ] 屍體：oxblood ink-stain 5 秒淡出

### Phase 4 · 細節（2026-05-08 部分完成）
- [x] 殘色 grep 清理（`#333`、`#5A8A5A`、`#88CCFF`、`#FF4444`、`#FF8800`、`#FFD700`、`#aaa`、`#CC0000`、`#FF9800` 等）
- [x] 怪物 HP 條改設計系統色（blood → warning 兩階 + surface/ink 背景）
- [ ] 背景格線色再調（如有需要）
- [ ] 搖桿視覺實機微調
- [ ] 開場 / 結算字體位置/大小統一

## 待辦（下次接手）

---

## 設計決策（待 Phase 3 動工時 decide）

| 議題 | 選項 | 暫定方向 |
|------|------|---------|
| 騎士暖膚 vs 冷鐵的「臉部辨識感」| (a) 全冷鐵藍灰 (b) 加暗紅披風破單調 | (a)，DESIGN.md RISK 選項 |
| 骷髏動畫 idle bobbing 要不要保留 | DESIGN.md anti-slop 第 9 條：「角色不要無謂浮動」| 看實機，太靜可微保留 |
| 升級 ink-bloom 動畫時長 | 600 / 800 / 1200ms | 800ms |

---

## 下次怎麼接手

1. 在 `06_割草遊戲/` 路徑下開新 Claude 對話
2. 說「**繼續跑 BACKLOG**」或「**進 Phase 3**」
3. Claude 應自動讀本檔 + DESIGN.md + repo CLAUDE.md
4. 從進行中的「雙倍升級選項」未打勾處接，做完再進 Phase 3 第一項

## 重要檔案位置

- 設計聖經：[DESIGN.md](DESIGN.md)
- 預覽頁：[design-preview.html](design-preview.html)（不要 commit，看完可刪）
- repo 指令：[CLAUDE.md](CLAUDE.md)
- 主程式：[index.html](index.html)
