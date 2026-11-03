# 萬聖節南瓜 Sprite Sheet — 南瓜怪物

[← 返回素材總覽](../README.md)

## 1. 角色概覽

發光的萬聖節南瓜怪物（Jack-o'-lantern），橘色瓜身、綠色瓜蒂、表情帶有惡作劇感。適合作為學校走廊、廢棄教室或萬聖節關卡中的移動障礙或敵人；角色行為需另外編寫遊戲邏輯。

![萬聖節南瓜預覽](../assets/sprites/pumpkin/preview_contact_sheet.png)

> 上方為動作展示圖。遊戲需使用下方透明 PNG 圖集，勿切割預覽圖。

## 2. 素材檔案

- **[64px 透明 Sprite Sheet](../assets/sprites/pumpkin/pumpkin_spritesheet_64px.png)** — `512 × 512`，8 × 8 網格。
- [128px 透明 Sprite Sheet](../assets/sprites/pumpkin/pumpkin_spritesheet_128px.png) — `1024 × 1024`，8 × 8 網格。
- [64px Atlas JSON](../assets/sprites/pumpkin/pumpkin_atlas_64px.json) — 64px 對應座標與動畫順序。
- [128px Atlas JSON](../assets/sprites/pumpkin/pumpkin_atlas.json) — 128px 對應座標與動畫順序。
- [Idle GIF 預覽](../assets/sprites/pumpkin/preview_idle.gif) · [Walk GIF 預覽](../assets/sprites/pumpkin/preview_walk_down.gif) · [Attack GIF 預覽](../assets/sprites/pumpkin/preview_attack.gif)

**圖集規格：** 8 欄 × 8 行；每行 8 幀；共 **64 幀**；透明背景 RGBA。

## 3. 動畫表（0-based row）

| Row | 動畫名稱 | 說明 | 幀數 | 建議 FPS | 是否循環建議 |
| ---: | --- | --- | ---: | ---: | --- |
| 0 | `idle` | 待機 | 8 | 6 | 是 |
| 1 | `walk_down` | 向下走 | 8 | 8 | 是 |
| 2 | `walk_up` | 向上走 | 8 | 8 | 是 |
| 3 | `walk_left` | 向左走 | 8 | 8 | 是 |
| 4 | `walk_right` | 向右走 | 8 | 8 | 是 |
| 5 | `attack` | 攻擊／火焰效果 | 8 | 10 | 否 |
| 6 | `hurt` | 受傷 | 8 | 7 | 否 |
| 7 | `die` | 死亡／破碎 | 8 | 7 | 否 |

動畫名稱與 FPS 對應原始 `pumpkin_atlas_64px.json` 的 `row_order`、`suggested_fps`。每列影格依左至右排列，從 `00` 到 `07`。

## 4. 遊戲設計建議

- **巡邏**：在走廊或教室周圍移動，使用四方向走路動畫。
- **阻擋**：玩家靠近時可能觸發 `attack`，例如噴出南瓜火焰。
- **解謎**：玩家關閉燈籠、解除機關後可播放 `hurt` 或 `die` 作為視覺回饋。
- **掉落物品**：如果遊戲設計要求，可在死亡動畫結束後產生鑰匙、密碼紙等道具（此功能未包含於素材）。

### 建議關卡事件（示例）

```json
{
  "entityId": "pumpkin_01",
  "type": "hazard",
  "spriteSheet": "assets/sprites/pumpkin/pumpkin_spritesheet_64px.png",
  "atlas": "assets/sprites/pumpkin/pumpkin_atlas_64px.json",
  "initialAnimation": "idle",
  "onPlayerEnterRange": "attack",
  "onDefeated": "die"
}
```

## 5. 匯入及驗收

- **Unity**：Sprite Multiple，切割 64 × 64（或 128 × 128），Point 過濾，Compression None。
- **Godot**：`hframes = 8`、`vframes = 8`；依不同列設為對應動畫。
- 角色中心或底部中央可作為 pivot；請依碰撞方式微調。
- AI 生成圖幀的動態與特效可能有不連貫之處，正式用於遊戲前請逐行試播。

- [ ] 待機與移動循環平順
- [ ] 攻擊動畫播完後返回適當狀態
- [ ] 死亡動畫只播放一次
- [ ] PNG 透明區域、碰撞範圍與畫面縮放正確

[← 返回素材總覽](../README.md)
