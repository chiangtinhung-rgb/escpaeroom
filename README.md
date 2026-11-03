# 校園密室逃脫：像素角色素材庫

> School Escape Room — Pixel Sprite Assets · GitHub 文件與素材包

這個資料夾整理三組已生成的遊戲角色素材：**校服學生、萬聖節南瓜、萬聖節幽靈**。包含可直接在 GitHub 瀏覽的 Markdown 說明、透明 PNG Sprite Sheet、動畫 JSON 資料及少量 GIF 預覽，方便在 2D 密室逃脫／校園解謎遊戲中使用。

## 角色文件

| 角色 | 預覽 | 文件 | 動畫數量 |
| --- | --- | --- | --- |
| 校服學生（男／女） | ![學生預覽](assets/sprites/students/preview_contact_sheet.png) | [學生角色與動畫](docs/students.md) | 每角色 10 種動作 × 8 幀 = 80 幀 |
| 萬聖節南瓜 | ![南瓜預覽](assets/sprites/pumpkin/preview_contact_sheet.png) | [南瓜角色與動畫](docs/pumpkin.md) | 8 種動作 × 8 幀 = 64 幀 |
| 萬聖節幽靈 | ![幽靈預覽](assets/sprites/ghost/preview_contact_sheet.png) | [幽靈角色與動畫](docs/ghost.md) | 8 種動作 × 8 幀 = 64 幀 |

> 上表預覽圖包含排版及文字，**不可直接當作遊戲圖集切割**。實際使用 `*_spritesheet_64px.png` 等透明圖集。

## 專案資料夾

```text
school_escape_room_github/
├── README.md
├── docs/
│   ├── students.md
│   ├── pumpkin.md
│   └── ghost.md
└── assets/
    └── sprites/
        ├── students/
        │   ├── preview_contact_sheet.png
        │   ├── schoolboy/
        │   │   ├── schoolboy_spritesheet_64px.png
        │   │   ├── schoolboy_spritesheet_96px.png
        │   │   ├── schoolboy_atlas_64px.json
        │   │   ├── schoolboy_atlas.json
        │   │   └── gif_previews/
        │   └── schoolgirl/
        │       ├── schoolgirl_spritesheet_64px.png
        │       ├── schoolgirl_spritesheet_96px.png
        │       ├── schoolgirl_atlas_64px.json
        │       ├── schoolgirl_atlas.json
        │       └── gif_previews/
        ├── pumpkin/
        │   ├── pumpkin_spritesheet_64px.png
        │   ├── pumpkin_spritesheet_128px.png
        │   ├── pumpkin_atlas_64px.json
        │   ├── pumpkin_atlas.json
        │   ├── preview_contact_sheet.png
        │   └── preview_*.gif
        └── ghost/
            ├── halloween_ghost_spritesheet_64px.png
            ├── halloween_ghost_spritesheet_128px.png
            ├── halloween_ghost_atlas_64px.json
            ├── halloween_ghost_atlas_128px.json
            ├── preview_contact_sheet.png
            └── gif_previews/
```

## 快速開始：上傳 GitHub

1. **先解壓縮**下載的 GitHub 素材包，GitHub 不會自動解壓上傳的 ZIP。
2. 開啟你的 GitHub Repository，選擇 **Add file → Upload files**，將解壓後的 `README.md`、`docs/`、`assets/` 一起上傳。也可以用 Git 指令上傳。
3. 確認 README 裡的連結和預覽圖片正常顯示，並提交 Commit。
4. 在遊戲引擎中讀取 `assets/sprites/` 下的透明 PNG 和對應 JSON；不要用 `preview_contact_sheet.png` 作遊戲素材。

已經有 `README.md` 的專案：請**將這份 README 的內容合併到原本 README**，而不是直接覆蓋。`docs/` 與 `assets/` 可加入既有專案；如果資料夾名稱改變，記得修改 Markdown 的相對路徑。

### Git 指令上傳（適用已建立 Git Repository 的情況）

```bash
git add README.md docs assets/sprites
git commit -m "Add escape room sprite asset documentation"
git push
```

## 通用圖集規格

| 素材 | 64px 圖集尺寸 | 網格 | 每幀尺寸 |
| --- | --- | --- | --- |
| 學生（男／女） | 512 × 640 | 8 欄 × 10 行 | 64 × 64 |
| 南瓜 | 512 × 512 | 8 欄 × 8 行 | 64 × 64 |
| 幽靈 | 512 × 512 | 8 欄 × 8 行 | 64 × 64 |

- 動畫的 **row（列／行）索引從 0 開始**，每列 8 幀，從左至右播放。
- 素材為透明背景的 PNG（RGBA）。請使用 **Nearest / Point** 過濾及整數倍放大，避免像素邊緣模糊。
- `*_atlas*.json` 內含每幀的座標、尺寸與動畫順序；學生 `*_atlas_64px.json` 為本次依原始 96px 版本換算出的 64px 版本。
- 建議使用角色底部中央作為定位點（pivot），並在引擎內依遊戲座標微調。
- JSON 屬於素材資料，不代表遊戲已具備行走、碰撞、追逐或解謎程式；這些玩法需要另行實作。

## 遊戲情境建議（非已完成程式功能）

- 學生：玩家角色，使用方向鍵移動；靠近線索時播放 `interact`；拾取鑰匙時播放 `pick_up`。
- 南瓜：走廊或教室的障礙敵人，巡邏時使用 `walk_*`，被觸發時使用 `attack`。
- 幽靈：校園靈異事件的追逐者或驚嚇事件，接近玩家時使用 `walk_*` 或 `attack`。

## 注意事項

這些素材來自 AI 輔助生成與整理，請在正式發行前檢查影格連貫性、角色尺寸、方向一致性及第三方素材授權。本文僅記錄目前素材規格，遊戲玩法與角色背景是可自行調整的設計建議。
