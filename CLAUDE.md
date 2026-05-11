# Lawn Mowing Game — Claude Instructions

## Project Overview
Single-file HTML5 Canvas roguelite (~2900 lines vanilla JS). 騎士 vs 骷髏，Vampire Survivors-like。
- **Repo**: ArdenLin88/lawn-mowing-game
- **Deploy**: Vercel (auto-deploy on push to master)
- **Architecture**: 全部在 `index.html` — HTML + CSS + canvas JS

## Design System
**Always read [DESIGN.md](DESIGN.md) before making any visual or UI decisions.**

所有字體、顏色、間距、特效、aesthetic direction 都定義在 DESIGN.md 裡。

- 不要 deviate without explicit user approval
- QA / 視覺修改時，flag 任何不符合 DESIGN.md 的代碼
- 視覺爭議：以 DESIGN.md 為準。**先改文件，再改代碼**。

## Visual Direction Quick Reference
- **方向**: Engraved Woodcut × Witchlight（雕版 × 鬼火）
- **字體**: Pirata One（display）+ IM Fell English（body）
- **核心紀律**: 80% 畫面只用 bg/surface/ink/muted，飽和色配給制
- **Anti-slop**: 不用紫 / 不用圓角 / 不用 shadowBlur / 不用 emoji icons / 不用 neon glow

## 工作流程
- 「上版 / 上 git / 推上去 / 部署」 = `git add → commit → push`，Vercel 自動部署
- Commit 風格：中文 conventional（`polish:` / `feat:` / `fix:`）
- **不 commit**：`.gstack/`、`design-preview.html`（本機預覽用）
