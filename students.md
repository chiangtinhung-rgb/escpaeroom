# 校服學生 Sprite Sheet — 玩家角色

[← 返回素材總覽](../README.md)

## 1. 角色概覽

本素材包含 **男學生（schoolboy）** 與 **女學生（schoolgirl）**，外觀為 Q 版校園制服像素角色。可作為校園密室逃脫的可操作主角、同伴或 NPC；角色設定與遊戲功能屬建議，尚需由遊戲程式實作。

![男女學生預覽](../assets/sprites/students/preview_contact_sheet.png)

> 這張圖是排版預覽，不是供遊戲直接切割的 Sprite Sheet。

## 2. 素材檔案

| 用途 | 男學生 | 女學生 |
| --- | --- | --- |
| **64px 透明圖集** | [PNG](../assets/sprites/students/schoolboy/schoolboy_spritesheet_64px.png) | [PNG](../assets/sprites/students/schoolgirl/schoolgirl_spritesheet_64px.png) |
| 96px 透明圖集 | [PNG](../assets/sprites/students/schoolboy/schoolboy_spritesheet_96px.png) | [PNG](../assets/sprites/students/schoolgirl/schoolgirl_spritesheet_96px.png) |
| 64px 動畫座標 | [JSON](../assets/sprites/students/schoolboy/schoolboy_atlas_64px.json) | [JSON](../assets/sprites/students/schoolgirl/schoolgirl_atlas_64px.json) |
| 96px 動畫座標 | [JSON](../assets/sprites/students/schoolboy/schoolboy_atlas.json) | [JSON](../assets/sprites/students/schoolgirl/schoolgirl_atlas.json) |
| 待機 GIF | [GIF](../assets/sprites/students/schoolboy/gif_previews/idle.gif) | [GIF](../assets/sprites/students/schoolgirl/gif_previews/idle.gif) |
| 走路 GIF | [GIF](../assets/sprites/students/schoolboy/gif_previews/walk_down.gif) | [GIF](../assets/sprites/students/schoolgirl/gif_previews/walk_down.gif) |
| 調查 GIF | [GIF](../assets/sprites/students/schoolboy/gif_previews/interact.gif) | [GIF](../assets/sprites/students/schoolgirl/gif_previews/interact.gif) |

**圖集規格：** 8 欄 × 10 行；每行 8 幀。每位角色共 **10 種動畫 × 8 幀 = 80 幀**。

- 64px：單幀 64 × 64，整張 512 × 640（推薦像素遊戲使用）。
- 96px：單幀 96 × 96，整張 768 × 960。
- 格式：透明背景 RGBA PNG，無網格間距。

## 3. 動畫表（0-based row）

| Row | 動畫名稱 | 說明 | 幀數 | FPS | 循環 | 密室逃脫用途建議 |
| ---: | --- | --- | ---: | ---: | --- | --- |
| 0 | `idle` | 待機 | 8 | 5 | 是 | 停止移動時播放 |
| 1 | `walk_down` | 向下走 | 8 | 9 | 是 | 玩家向畫面下方移動 |
| 2 | `walk_up` | 向上走 | 8 | 9 | 是 | 玩家向畫面上方移動 |
| 3 | `walk_left` | 向左走 | 8 | 9 | 是 | 玩家向左移動 |
| 4 | `walk_right` | 向右走 | 8 | 9 | 是 | 玩家向右移動 |
| 5 | `run` | 跑步 | 8 | 12 | 是 | 被追逐時加速，動作方向需測試 |
| 6 | `interact` | 調查／互動 | 8 | 7 | 否 | 調查箱子、日記、門鎖 |
| 7 | `pick_up` | 拾取道具 | 8 | 7 | 否 | 拿起鑰匙、證物 |
| 8 | `scared` | 受驚 | 8 | 9 | 否 | 遇見幽靈、觸發機關 |
| 9 | `crouch` | 蹲下 | 8 | 6 | 是 | 躲藏、穿過低矮空間 |

每行依序為 `00` 到 `07`，例如 `walk_down_00` 至 `walk_down_07`。動畫名稱與 FPS 對應原始 `schoolboy_atlas.json` / `schoolgirl_atlas.json`。

## 4. 建議互動流程

```text
玩家移動 → 根據方向播放 walk_down / walk_up / walk_left / walk_right
玩家停止 → idle
靠近可互動物品並按 E → interact → 判定是否找到線索
獲得道具 → pick_up → 更新背包
觸發驚嚇事件 → scared → 恢復 idle
按住蹲下鍵 → crouch → 解除後恢復移動
```

### 建議角色狀態（示例，非素材原有資料）

```json
{
  "characterId": "schoolgirl",
  "type": "player",
  "spriteSheet": "assets/sprites/students/schoolgirl/schoolgirl_spritesheet_64px.png",
  "atlas": "assets/sprites/students/schoolgirl/schoolgirl_atlas_64px.json",
  "startingAnimation": "idle",
  "canInteract": true,
  "canPickUpItems": true
}
```

## 5. 匯入設定

- **Unity**：Texture Type = Sprite (2D and UI)、Sprite Mode = Multiple；Sprite Editor → Slice → Grid by Cell Size = `64 × 64`（或 `96 × 96`）。
- **Godot**：`AnimatedSprite2D` / `SpriteFrames`，圖集為 `hframes = 8`、`vframes = 10`，依上表設定 FPS。
- 使用 Nearest / Point 過濾；角色座標錨點建議底部中央。
- 64px 的 JSON 為本次由原始 96px 座標等比例換算產生；請勿將 64px 圖片與 96px JSON 混用。

## 6. 驗收清單

- [ ] 四方向走路切換正常
- [ ] 待機與走路的角色腳底定位一致
- [ ] 調查、拾取及受驚動畫播放完畢後能回到 idle
- [ ] 碰撞箱獨立於整張影格尺寸設定
- [ ] 連續 8 幀播放時沒有背景殘留或裁切

[← 返回素材總覽](../README.md)
