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
- [x] 大魔王太脆了, 起碼要增加5倍的血條（250 HP），死後會再復活一次（50% HP + 復活特效）
- [x] 不同怪物的經驗應該要不同：骷髏+1 / 殭屍+3 / 弓箭手+4 / 精英+6 / 大魔王+50，浮動文字顏色按 XP 值區分

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
- [x] **受傷反饋**：玩家 invincible 閃爍（0.4 alpha pulse），取代全螢幕反白
- [x] **傷害數字**：改用 `IM Fell English italic 18px`，顏色 blood（移除 Arial）
- [x] **爆擊數字**：15% 爆擊率，`Pirata One 26px` + crit 青（`#5FA89C`）+ ⚡ 前綴
- [x] **升級特效**：中央 ink-bloom 800ms（暗墨擴散圓 + xp-glow 雙環圈）
- [x] **低血 (<30%)**：螢幕邊緣 ember vignette，~1Hz 脈動（radialGradient warning 色）
- [x] **屍體 ink-stain**：bloodDecal 5 秒淡出（300 frames），上限 150 個

### Phase 4 · 細節（2026-05-08 部分完成）
- [x] 殘色 grep 清理（`#333`、`#5A8A5A`、`#88CCFF`、`#FF4444`、`#FF8800`、`#FFD700`、`#aaa`、`#CC0000`、`#FF9800` 等）
- [x] 怪物 HP 條改設計系統色（blood → warning 兩階 + surface/ink 背景）

### Bug 修正（2026-05-21）
- [x] **B1**：`resetGame()` 補 `bossRevived = false`（第二局大魔王不再跳過復活）
- [x] **B2**：浮動文字字體 Arial → IM Fell English（設計系統違規修正）
- [x] **B3**：大魔王登場時機修正：`10800` → `18000` frames（確認 5 分鐘登場）
- [x] **B4**：`floatTexts` 加 `maxLife` 欄位，透明度計算不再硬編碼 50

### 效能優化（2026-05-21）
- [x] **E1**：`circleCollide` 改平方距離比較，移除 `Math.sqrt` 開銷
- [x] **E2**：背景格線 + 草葉改 offscreen canvas 預烘焙，每幀只 `drawImage` 一次
- [x] **E4**：`aliveEnemyCount` 全域快取，HUD 不再每幀 `enemies.filter()`
- [x] **E5**：`bloodDecals` 上限 150，超過 FIFO 丟棄最舊的

### 程式碼品質（2026-05-21）
- [x] **C1**：大魔王復活/死亡 particles 的 `radius` → `size`（與繪製迴圈一致，修正不可見粒子 bug）
- [x] **G3**：速度殘影顏色 `#88FFCC` → `COLORS.crit`（回歸設計系統）

---

## 待辦

### Phase 4 · 細節（剩餘）
- [ ] 背景格線色再調（如有需要）
- [ ] 搖桿視覺實機微調
- [ ] 開場 / 結算字體位置/大小統一

---

## 🧙 Phase 5 · 法師角色系統（✅ 完成 2026-05-21）

> 目標：讓玩家可在開場選擇騎士或法師，兩者使用同一場景但攻擊手感完全不同。

### 角色設定
| 屬性 | 騎士（現有） | 法師（新增） |
|------|------------|------------|
| 攻擊方式 | 刀刃扇形（近戰） | 魔法彈（遠程，點擊/搖桿方向） |
| 基礎血量 | 5 HP | 3 HP（更脆） |
| 基礎移速 | 3.2 | 2.8（稍慢） |
| 特色 | 全方位覆蓋、近身強 | 彈幕爆發、需要走位 |
| 繪製風格 | 冷鐵板甲 + 血紅斗篷 | 骨粉長袍 + xp-glow 法杖 |

### 法師技能池（全新設計）
| 技能 | 描述 | 稀有度 |
|------|------|--------|
| 🔮 魔彈加速 | 彈速 +15% | common |
| ❄️ 冰霜穿透 | 魔彈穿透 1 個敵人 | rare |
| 🌀 散射 | 每次發射 +1 顆彈 | rare |
| 🌊 冰牆 | 每 8 秒召喚減速結界 | legendary |
| 💀 靈魂汲取 | 擊殺回血 1 | rare |
| ⚡ 連鎖閃電 | 命中後彈射到鄰近敵人 | legendary |

### 武器進化（法師專屬）
| 進化名 | 條件 | 效果 |
|--------|------|------|
| 🌌 虛空爆裂 | 魔彈加速 Lv3 + 散射 Lv3 | 爆炸範圍 +100px，穿透無限 |
| 🧊 永凍術 | 冰霜穿透 Lv3 + 冰牆 Lv3 | 減速效果翻倍，敵人移速降 60% |

### 實作步驟
- [x] 開場選角畫面（2 張卡片：騎士 / 法師，雕版風格）
- [x] `currentCharacter` 全域 + 條件切換 `player.draw()` / `player.update()`
- [x] 法師本體繪製（長袍橢圓 + 法杖 + xp-glow 魔法球 aura）
- [x] 魔法彈系統（獨立 `magicBolts[]` 陣列，pierce hitSet + chain lightning + soul drain）
- [x] 冰牆系統（`iceWalls[]`，CD 480 frames，敵人進入範圍自動減速）
- [x] 法師技能池 `MAGE_SKILL_POOL`（只在選法師時出現，pickUpgradeOptions 分支）
- [x] 法師武器進化條件（`MAGE_EVOLUTION_DEFS`，checkEvolutions 分支）
- [x] `drawCharSelectScreen()` + `_drawCharCard()` + 角色圖示（`_drawKnightIcon` / `_drawMageIcon`）
- [x] `goToCharSelect()` ← gameover/victory 按 R 或點擊都跳這裡
- [x] `checkCharSelectClick()` ← 座標縮放偵測，支援桌面 + 觸控
- [x] `resetGame()` 角色分支（法師：HP=3, speed=2.8, bladeRadius=0, 法師陣列清空）
- [x] `gameLoop` 法師更新/繪製（`updateMagicBolts/updateIceWalls/drawIceWalls/drawMagicBolts`）
- [x] 事件監聽更新（R→選角、1 選騎士、2 選法師、canvas click 縮放修正、touchend 支援）
- [ ] HUD 差異（法師顯示 MP 條取代護甲，騎士顯示 HP 條）← 未來可選做

---

## 🗡️ Phase 6 · 盜賊角色系統（✅ 完成 2026-05-21）

> 玩法核心：瞬間爆發 + 閃避，高風險高報酬，殺怪有「連殺獎勵」機制。

### 角色設定
| 屬性 | 騎士（現有） | 法師（Phase 5） | 盜賊（新增） |
|------|------------|--------------|------------|
| 攻擊方式 | 刀刃扇形（近戰） | 魔法彈（遠程） | 匕首投擲 + 瞬間爆發（近+中） |
| 基礎血量 | 5 HP | 3 HP | 4 HP |
| 基礎移速 | 3.2 | 2.8 | 4.2（最快） |
| 特色 | 穩定覆蓋 | 彈幕節奏 | 閃避連殺、連殺獎勵疊加 |
| 繪製風格 | 冷鐵板甲 | 骨粉長袍 | 深色皮甲 + blood 頭巾 + 雙刃 |

### 核心機制：連殺計數器
- 每 2 秒內連續擊殺 → `comboCount++`
- 超過 2 秒無擊殺 → combo 重置
- combo 加成：`+comboCount × 5%` 攻速 + XP 獲取
- UI：combo 數字顯示於玩家頭上（Pirata One + xp-glow）

### 盜賊技能池
| 技能 | 描述 | 稀有度 |
|------|------|--------|
| 🗡️ 雙投 | 每次投擲 +1 把匕首（扇形） | common |
| 💨 閃避 | 每 3 秒可觸發無敵衝刺 0.4s | rare |
| 🩸 放血 | 命中後敵人每秒失血（DoT） | common |
| ☠️ 暗殺 | 單體 HP < 30% 時爆擊率 +40% | rare |
| 🎭 幻影 | 殘影欺敵，敵人隨機攻擊幻影 | legendary |
| 🔗 毒刃 | 命中後傳播毒效果到鄰近敵人 | legendary |

### 武器進化（盜賊專屬）
| 進化名 | 條件 | 效果 |
|--------|------|------|
| 🌑 暗殺之主 | 暗殺 Lv3 + 雙投 Lv3 | 暗殺無 CD 限制，每擊皆爆擊 |
| 🧪 瘟疫使者 | 放血 Lv3 + 毒刃 Lv3 | 毒/血傳播給全場所有敵人 |

### 閃避衝刺說明
- 按右搖桿（手機）或 Shift（PC）觸發
- 向當前移動方向衝刺 140px，0.4s 無敵幀
- CD：3 秒，HUD 顯示 CD 倒計時（小圓點）

### 實作步驟
- [x] 開場選角畫面擴充（3 張卡：騎士 / 法師 / 盜賊，cardW=180px）
- [x] 盜賊本體繪製（深棕皮甲 + blood 腰帶頭巾 + 雙匕首 + 衝刺殘影 + CD 弧線）
- [x] 匕首投擲系統（`daggers[]`，扇形扔出 1+N 把，命中消失）
- [x] 連殺計數器（`comboCount`、`comboTimer` 2 秒窗）+ HUD combo 顯示
- [x] 閃避衝刺（Shift / 右搖桿快推，14 幀無敵衝刺 ≈140px，CD 縮減技能）
- [x] DoT 系統（放血 / 毒刃，每 60 幀掉血，繞過 hitCooldown，直接扣 HP）
- [x] 盜賊技能池 `ROGUE_SKILL_POOL`（8 技能）+ `ROGUE_EVOLUTION_DEFS`（2 進化）
- [x] 幻影系統（`phantoms[]`，`getEnemyTarget()` 55% 敵人分心追幻影，3 秒重決定）
- [x] 毒刃傳播（瘟疫使者進化 → 全場傳播；普通 → 鄰近 2 隻）
- [x] `pickUpgradeOptions` / `checkEvolutions` 加 rogue 分支
- [x] `resetGame()` rogue 分支 + 所有盜賊陣列重置
- [x] `gameLoop` 更新/繪製（daggers / phantoms / combo timer）
- [x] 事件監聽：'3' 鍵選盜賊、Shift 衝刺

---

## 設計決策

| 議題 | 選項 | 暫定方向 |
|------|------|---------|
| 騎士暖膚 vs 冷鐵的「臉部辨識感」| (a) 全冷鐵藍灰 (b) 加暗紅披風破單調 | (a)，DESIGN.md RISK 選項 |
| 骷髏動畫 idle bobbing 要不要保留 | DESIGN.md anti-slop 第 9 條：「角色不要無謂浮動」| 看實機，太靜可微保留 |
| 升級 ink-bloom 動畫時長 | 600 / 800 / 1200ms | 800ms（已實作）|
| 法師選角入口 | 開場畫面加選角 vs 進入後按 Tab 切換 | 開場選角（更清晰，不影響戰鬥中 UI）|
| 盜賊閃避觸發鍵 | Shift（PC）/ 右搖桿雙擊（手機） | Shift + 右搖桿雙擊（待測試手感）|
| 三角色選角呈現 | 橫排 3 張雕版卡 vs 旋轉選擇盤 | 橫排卡片（與技能選單保持一致風格）|

---

## 下次怎麼接手

1. 在 `06_割草遊戲/` 路徑下開新 Claude 對話
2. 說「**繼續跑 BACKLOG**」或「**進 Phase 6 盜賊**」
3. Claude 應自動讀本檔 + DESIGN.md + repo CLAUDE.md
4. Phase 5 已全數完成；Phase 6 從盜賊「實作步驟」第一項開始

### 目前狀態（2026-05-21）
- ✅ Phase 5 法師：選角畫面 + 魔法彈 + 冰牆 + 進化 → 全部完成
- ✅ Phase 6 盜賊：匕首 + 衝刺 + Combo + DoT + 幻影 + 三角色選角 → 全部完成
- 🔜 HUD 法師 MP 條：可選做，Phase 5 遺留低優先項目
- 🔜 Phase 7 想法：更多敵人種類 / 精靈叢林地圖換膚 / 排行榜 / 搖桿優化

---

## 🏚️ Stage 7 · 遊戲深度設計（2026-05-29 啟動）

> 目標：讓玩家每局死後有回音、每局成果有積累、世界更大。

### 7-1 死後審判畫面（✅ 完成）
- [x] 全域 `runStats` 追蹤：擊殺數、等級、時間、最高連殺、受傷次數
- [x] localStorage 存儲 `lastRunStats`（跨局比對）
- [x] 改寫 `drawGameOverScreen()`：顯示本局 vs 上局統計差異（↑/↓）
- [x] 本局「高光」區塊：最長生存時間 + 最高連殺 + 主要傷害來源
- [x] 顯示本局獲得的墓誌銘金幣數量

### 7-2 墓誌銘金幣系統（✅ 完成）
- [x] `tombCoins` localStorage 跨局存儲
- [x] 金幣發放：每 5 次擊殺 +1 幣、每升一級 +2 幣、打倒 Boss +20 幣、零傷害通關 +15 幣
- [x] `TABLET_DEFS` 定義 7 項石板升級
- [x] `drawTabletScreen()` ── canvas 石板升級畫面（新 state `'tablet'`）
- [x] 選角畫面底部新增「石板」入口按鈕

### 7-3 三幕制關卡結構（✅ 完成）
- [x] `actPhase` 全域：0=廢城入口 / 1=腐敗森林 / 2=骷髏王廷
- [x] 第一幕→第二幕：累積 40 擊殺後觸發幕次公告
- [x] 第二幕：弓箭手比例提高，幕次 banner 顯示 180 幀
- [x] 第三幕：大魔王登場，**持續生怪**（原版大魔王出現後停生怪）
- [x] `actBannerTimer` 控制幕次公告淡出

### 7-4 敵人圖鑑（✅ 完成）
- [x] `codexUnlocked` Set + localStorage 跨局儲存
- [x] `codexKillCounts` 統計各類型總擊殺數
- [x] 首次擊殺時觸發圖鑑解鎖動畫（右下角小卡片飛入）
- [x] `CODEX_ENTRIES` 5 個怪物條目（古書語氣描述）
- [x] `drawCodexScreen()` ── canvas 圖鑑畫面（新 state `'codex'`）
- [x] 選角畫面底部新增「圖鑑」入口按鈕

### 7-5 隱藏內容（✅ 完成）
- [x] **死靈師解鎖**：累積死亡 5 次，選角出現第四個角色卡
- [x] **完美破關彩蛋**：本局零受傷打倒大魔王，破關畫面顯示特殊金邊 + 「無傷奇跡」稱號
- [x] **老頭子彩蛋**：大魔王跨局復活 5 次以上，Boss 血條名稱變成「老頭子」
- [x] **死靈師角色**：鐮刀近戰、獨立技能池（`NECROMANCER_SKILL_POOL`）、黑袍白骨視覺

---

## 🤖 Stage 8 · 內建 AUTOPILOT bot（✅ 騎士版完成，已通關 ×2）

> 在 index.html 內建自動破關 bot，右上角「AUTO」齒輪面板控制（雕版風、無 emoji、半透明）。
> 全部讀遊戲全域狀態（player/enemies/arrows/expGems…）→ 寫 joyMove + mouseX/Y 操控，獨立 rAF loop。

### UI（#autopilot-panel + #sound-toggle，CSS 雕版風）
- [x] 齒輪 AUTO 收起半透明、hover 清晰；點開展 LV1/LV2/LV3/LV4 + 技能自動/手動 + STOP
- [x] 狀態 HUD（版本/角色/HP/擊殺/時間/幕次），全透明只留描邊文字
- [x] **靜音開關**（右上喇叭 icon）：全域 `audioMuted` 旗標，BGM 淡入 + SFX 發聲都讀它（重開不恢復）

### bot 版本（騎士，botVersion 控制；都繼承邊界排斥 + 撿 XP + 繞精英骷髏）
- [x] **LV1** kiting，不躲箭（基準對照）
- [x] **LV2** + 飛箭側向閃避（偵測 320px / 擦邊 44 / 權重 2.0）
- [x] **LV3** 主動進攻清場：朝敵群質心推進繞圈，優先獵殺弓箭手（貼邊射手放棄改打人多）
- [x] **LV4** = LV3 + 只鎖畫面內敵人（不追畫面外、不貼邊界）

### 技能自動選（apAutoPick，動態優先序）
- [x] 走割魂大鐮：`刀刃伸長 → 連鎖割 → 刀刃加寬`（核心保護）；湊齊後主攻連鎖割清群
- [x] 護盾只在 HP≤3 搶；×2 雙倍卡「適度優先」（分層：保命 > 核心材料 > 其他含 ×2 前移）

### 同場修掉的遊戲 bug
- [x] **`isNecro` TDZ 崩潰**：選角畫面 `_drawCharCard` 在宣告前用 `isNecro` → 整個選角畫面只畫一張卡。宣告移到函式頂部修復。

### 🔜 後續：LV5 盜賊衝刺無敵版
> 騎士近戰打遠程有先天劣勢（箭速 4.5 > 移速 3.2，正面直射躲不掉）。真正機制突破是盜賊「閃避衝刺 14 幀無敵」直接穿箭雨。要做時讀盜賊機制（fireDagger 瞄準 / dash 觸發 / 三進化）。

### 觸發語 / 操作
- 開遊戲 → 右上 AUTO 點開選 LV → bot 自動選騎士開打。檔案就是 index.html，無需注入。
- 改 bot 邏輯：搜 `initAutopilot` / `apComputeMove` / `apAutoPick`（在 index.html 結尾 `<script>` 內）。

---

## 重要檔案位置

- 設計聖經：[DESIGN.md](DESIGN.md)
- 預覽頁：[design-preview.html](design-preview.html)（不要 commit，看完可刪）
- repo 指令：[CLAUDE.md](CLAUDE.md)
- 主程式：[index.html](index.html)
