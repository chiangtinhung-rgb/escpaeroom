# 萬聖節幽靈 Sprite Sheet — 幽靈怪物

[← 返回素材總覽](../README.md)

## 1. 角色概覽

戴南瓜巫師帽的可愛白色像素幽靈，帶有紫色光效。適用於校園密室逃脫、鬼屋場景、突發驚嚇和追逐橋段；實際 AI、追逐和音效需要另外開發。

![萬聖節幽靈預覽](../assets/sprites/ghost/preview_contact_sheet.png)

> 此預覽圖有標籤，不是供遊戲切割的透明圖集。

## 2. 素材檔案

- **[64px 透明 Sprite Sheet](../assets/sprites/ghost/halloween_ghost_spritesheet_64px.png)** — `512 × 512`，8 × 8 網格。
- [128px 透明 Sprite Sheet](../assets/sprites/ghost/halloween_ghost_spritesheet_128px.png) — `1024 × 1024`，8 × 8 網格。
- [64px Atlas JSON](../assets/sprites/ghost/halloween_ghost_atlas_64px.json) — 幀座標與動畫名稱。
- [128px Atlas JSON](../assets/sprites/ghost/halloween_ghost_atlas_128px.json) — 幀座標與動畫名稱。
- [Idle GIF 預覽](../assets/sprites/ghost/gif_previews/idle.gif) · [Attack GIF 預覽](../assets/sprites/ghost/gif_previews/attack.gif) · [Die GIF 預覽](../assets/sprites/ghost/gif_previews/die.gif)

**圖集規格：** 8 欄 × 8 行；每行 8 幀；共 **64 幀**；透明背景 RGBA。

## 3. 動畫表（0-based row）

| Row | 動畫名稱 | 說明 | 幀數 | FPS | 是否循環建議 |
| ---: | --- | --- | ---: | ---: | --- |
| 0 | `idle` | 待機／漂浮 | 8 | 7 | 是 |
| 1 | `walk_down` | 向下飄行 | 8 | 9 | 是 |
| 2 | `walk_up` | 向上飄行 | 8 | 9 | 是 |
| 3 | `walk_left` | 向左飄行 | 8 | 9 | 是 |
| 4 | `walk_right` | 向右飄行 | 8 | 9 | 是 |
| 5 | `attack` | 紫色魔法攻擊 | 8 | 11 | 否 |
| 6 | `hurt` | 受傷 | 8 | 8 | 否 |
| 7 | `die` | 消散 | 8 | 9 | 否 |

FPS 對應原始 `halloween_ghost_atlas_64px.json` 中的 `fps`。影格順序左至右，每列從 `00` 到 `07`。

## 4. 遊戲設計建議

- **氣氛事件**：玩家打開教室門、拿起特定道具或關燈時，觸發幽靈出現。
- **巡邏／追逐**：用四方向動畫跟隨玩家的相對方向。
- **攻擊**：玩家靠得太近時播放紫色魔法 `attack`，配合遊戲程式套用受傷或恐懼狀態。
- **解謎解除**：玩家完成正確儀式或找到關鍵物品後，播放 `die` 消散效果。

### 建議事件（示例）

```json
{
  "entityId": "ghost_01",
  "type": "spectral_enemy",
  "spriteSheet": "assets/sprites/ghost/halloween_ghost_spritesheet_64px.png",
  "atlas": "assets/sprites/ghost/halloween_ghost_atlas_64px.json",
  "initialAnimation": "idle",
  "onPlayerDetected": "walk_down",
  "onAttack": "attack",
  "onPuzzleSolved": "die"
}
```

> `onPlayerDetected` 的方向只是示例；真實遊戲應依玩家相對位置選擇 walk_up / walk_down / walk_left / walk_right。

## 5. 匯入及驗收

- **Unity**：Sprite Multiple，依 64 × 64（或 128 × 128）切割，Point 過濾。
- **Godot**：`AnimatedSprite2D`，`hframes = 8`、`vframes = 8`，按列建立動畫。
- 建議 pivot 於角色下方中央，參考原始 JSON：`x = 0.5`、`y = 0.87`。
- 正式遊戲內須檢查不同方向幀、發光邊緣和死亡幀連續性。

- [ ] 飄行動畫循環正常
- [ ] 追逐時方向切換符合移動方向
- [ ] 魔法攻擊只播放一次
- [ ] 消散結束後角色才移除或隱藏
- [ ] 透明區域與光效不留下矩形背景

[← 返回素材總覽](../README.md)
