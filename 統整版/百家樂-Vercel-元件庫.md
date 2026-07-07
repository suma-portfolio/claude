# 百家樂 · Vercel 元件庫（Component Library）

> 來源：Figma `Claude測試` → 頁面 **Vercel 元件** → Section **百家樂**（`152:106273`，3110 × 2672）
> 設計語言：**Vercel Geist**（近白畫布 `#fafafa`、墨黑 `#171717`、1px hairline `#ebebeb`、單一藍點綴 `#0070f3`）
> 語意色：**閒 Player = 藍 `#0070f3`**、**莊 Banker = 墨黑 `#171717`**、**和 Tie = 中灰 `#8f8f8f`**
> Section 連結：https://www.figma.com/design/19DNqBdUzqTOBDYzFxFSXL/?node-id=152-106273

本檔為此 Section 內 **41 個節點**（含 24 個 Component / 12 個 Instance / 5 個輔助 Frame・Text）的規格清單，依用途分類。每個元件標註 **Figma ID、尺寸（px）、結構、用途**。

---

## 一、設計 Token（Design Tokens）

### 色彩

| Token | HEX | 用途 |
|---|---|---|
| ink / primary | `#171717` | 主文字、莊 Banker、primary 填色、邊框最深階 |
| body | `#4d4d4d` | 次要內文 |
| mute | `#8f8f8f` | 說明文字、和 Tie、metadata |
| faint | `#a1a1a1` | placeholder、disabled |
| hairline | `#ebebeb` | 1px 卡片／分隔線 |
| canvas | `#fafafa` | 頁面底色 |
| canvas-elevated | `#ffffff` | 卡片、按鈕、輸入框 |
| link / accent（閒 Player） | `#0070f3` | 閒、連結、進行中狀態、focus |

### 字體

| Style | Family / Weight | Size / LH / Tracking | 用途 |
|---|---|---|---|
| heading-md | Geist SemiBold (600) | 20 / 28 / −0.4 | 卡片標題 |
| label-sm | Geist Medium (500) | 14 / 20 / −0.28 | 強調標籤 |
| mono-eyebrow | Geist Mono Medium (500) | 12 / 16 / 0 | 大寫技術 eyebrow（LIVE、狀態） |
| body-md | Geist Regular (400) | 14 / 20 / 0 | 內文、賠率 |
| body-sm | Geist Regular (400) | 12 / 16 / 0 | 註腳、metadata |
| button-md | Geist Medium (500) | 14 / 20 / 0 | 按鈕文字 |

### 圓角 / 間距

- 圓角：`sm 6px`（按鈕/輸入）、`md 12px`（卡片）、`lg 16px`（大面板）、`full 9999px`（圓形圖示鈕/籌碼）
- 間距（4px 基準）：`xxs 4 · xs 8 · sm 12 · md 16 · lg 24 · xl 32`

---

## 二、投注區（Betting Zones）

| 元件 | Figma ID | 尺寸 | 結構 | 用途 |
|---|---|---|---|---|
| **Vercel/BC Mobile Betting Zone (閒和莊)** | `178:27069` | 494 × 132 | 3 格：閒(186) · 和(122) · 莊(186) | 手機主投注區。閒藍／和灰／莊墨，白卡 hairline，賠率常駐 |
| **MB_投注區** | `176:32130` | 598 × 308 | 主注列(132) + 邊注列(88) + 邊注列(88) | 手機完整投注區（主注＋兩排邊注堆疊） |
| **PC_投注區** | `180:37293` | 704 × 232 | 邊注列(56) + 主注列(172) | 桌面版投注區（主注橫列＋上方邊注） |
| **多台＿投注区** | `178:27178` | 864 × 175 | 5 × `main_bet`（閒對/閒/和/莊/莊對） | 多台模式壓縮投注列 |
| **Vercel/BC PC Side Bets** | `137:23` | 609 × 171 | 龍寶/對子等邊注格 + 「莊龍寶 最高30:1」 | 桌面邊注群（龍寶、對子、幸運） |
| **Vercel/BC Mobile Side Bets (龍寶/對子)** | `134:995` | 338 × 46 | 3 格 + 「莊對 11:1」 | 手機邊注一列：閒對／龍寶／莊對 |
| **Vercel/BC Mobile Pair Bets (完美/任意對子)** | `134:1002` | 335 × 48 | 2 格（168 × 2） | 完美對子 / 任意對子 |

**狀態後綴建議**：`_Default / _Hover / _Active(已下注) / _Locked(已鎖定) / _Win / _Lose`。
下注鎖定時整區灰化並顯示「已鎖定」；命中時該格反白高亮＋派彩。

---

## 三、座位列（Seat Panels）

| 元件 | Figma ID | 尺寸 | 結構 | 用途 |
|---|---|---|---|---|
| **PC_SeatPanel** | `180:37026` | 612 × 52 | 8 × 座位(73) | 桌面 8 席位列（頭像／下注額／籌碼） |
| **MB_SeatPanel** | `180:37187` | 900 × 66 | 8 × 座位(109) | 手機 8 席位列（含中心亮起的當前座位） |

---

## 四、牌與發牌（Cards & Dealing）

| 元件 | Figma ID | 尺寸 | 結構 | 用途 |
|---|---|---|---|---|
| **Vercel/扑克 (手牌)** | `137:24` | 314 × 58 | 7 × `card`(38 × 58) | 閒／莊手牌卡排（點數＋花色，花色墨黑） |
| **MB_开牌** | `176:30009` | 432 × 90 | 2 × Frame(216)：閒 / 莊 | 手機開牌列（閒點數 vs 莊點數） |
| **Vercel/Dealer Card (視訊區域)** | `176:29283` | 370 × 164 | 「荷官 / 視訊區域」標籤 + Timer(56) | 真人荷官視訊區疊層（LIVE DEALER + 倒數） |

---

## 五、路紙（Roadmaps）

| 元件 | Figma ID | 尺寸 | 結構 | 用途 |
|---|---|---|---|---|
| **RoadmapBaccarat** | `176:29282` | 314 × 236 | `Big6x8`（6×8 格） | 大路主體（6 列 × 8 欄，莊墨／閒藍／和灰） |
| **rightRoadMap** | `180:35416` | 572 × 170 | 統計列(23) + 路紙(143) | 桌面右欄路紙（統計＋大路＋下三路） |
| **Vercel/BC Mobile Roadmap (路紙珠盤)** | `187:5439` | 572 × 143 | 珠盤(95) + 下方列(48) | 手機路紙珠盤 |
| **Vercel/BC Mobile Roadmap Stats (統計列)** | `187:4275` | 578 × 32 | AskRoad(132) + Stat(350) + span(80) | 問路 + 莊/閒/和/對統計 + 路紙選台 |

**顏色規範**：莊 = 墨黑實心、閒 = 藍、和 = 灰；珠盤／大路沿用相同語意色。

---

## 六、頁首與狀態（Header & Status）

| 元件 | Figma ID | 尺寸 | 結構 | 用途 |
|---|---|---|---|---|
| **Vercel/BC MultiBet Header** | `131:1106` | 408 × 47 | 免傭 toggle・多台投注・最小限紅 ₩80・關閉 | 多台投注頁首列 |
| **Vercel/StatusBanner (狀態列)** | `152:79803` | 370 × 75 | 狀態文字 Frame + Timer(56) | 局態橫幅（請投注／發牌中／已下注·等待發牌） |
| **請投注** | `152:79467` | 42 × 17 | Text | 狀態文字（投注中提示） |
| **ResultToast** | `137:142` | 172 × 51 | 「您贏 ₩200」 | 結算派彩 Toast |
| **Timer** | `127:1845` | 56 × 55 | 數字(14) + 環形進度 Frame | 倒數計時（環形＋秒數） |
| **狀態（開牌）** | `189:6931` | 56 × 55 | Vector + 「開牌」 | 開牌／揭牌狀態鈕 |

---

## 七、籌碼與結算（Chips & Settlement）

| 元件 | Figma ID | 尺寸 | 結構 | 用途 |
|---|---|---|---|---|
| **籌碼區** | `137:38` | 354 × 44 | 微調 + 4 籌碼(30/30/32/30) + ×2 | 籌碼面額選擇列（含加倍） |
| **結算列** | `137:2215` | 338 × 56 | Frame2(總注/餘額 203) + Frame4(限紅 112) | 底部結算資訊列（本局總注・餘額・限紅） |

---

## 八、按鈕與圖示（Buttons & Icons）

| 元件 | Figma ID | 尺寸 | 用途 |
|---|---|---|---|
| **btn_toggle** | `152:106286` | 96 × 41 | 開關（免傭等），內含 30px 圓鈕 |
| **btn__videocam_active** | `160:29731` | 48 × 48 | 視訊鏡頭（開） |
| **btn__videocam_normal** | `160:29732` | 48 × 48 | 視訊鏡頭（關） |
| **btn_top_active** | `160:29733` | 48 × 48 | 置頂（開） |
| **btn_top_normal** | `160:29734` | 48 × 48 | 置頂（關） |
| **btn_enter** | `160:29735` | 32 × 32 | 私人桌離開 |
| **btn_Gplay** | `160:29736` | 32 × 32 | 資訊 / 玩法說明 |
| **btn_barMenu** | `160:29737` | 48 × 48 | 三點選單 |
| **btn_dehaze** | `160:29738` | 48 × 48 | 漢堡選單 |
| **btn_chevronBackward** | `160:29739` | 48 × 48 | 返回 |
| **&lt;iconSize&gt; visibility** | `160:29845` | 32 × 32 | 顯示/隱藏（眼睛） |
| **&lt;iconSize&gt; quickReferenceAll** | `160:29846` | 32 × 32 | 快速參考／路紙 |
| **Component 174** | `160:31180` | 83 × 83 | 大型圓形視訊鈕 |
| **Component 178** | `160:31181` | 83 × 83 | 大型圓形功能鈕 |
| **洗牌 (Shuffle)** | `180:37372` | 180 × 82 | 洗牌提示（2 × Shuffle_L） |

> 按鈕形狀依 Vercel 規範：功能/導覽鈕用 6px 方角或圓形圖示鈕；行銷型 CTA 才用全圓 pill。

---

## 九、輔助節點（Helpers）

| 節點 | Figma ID | 尺寸 | 說明 |
|---|---|---|---|
| 標題文字「百家樂 · Vercel 元件」 | `131:909` | 244 × 34 | Section 標題 |
| `div`（珠路點列） | `131:985` | 300 × 69 | 45 × `span`(20×23) 珠盤點位範例 |

---

## 十、遊戲狀態 × 元件對應（State → Components）

依百家樂流程狀態機，各階段建議組合：

| 階段 | 主要元件 |
|---|---|
| **IDLE / 局間** | Roadmap 系列、Roadmap Stats、結算列、Timer |
| **BETTING 投注中** | StatusBanner(請投注)、Betting Zone(閒和莊)、Side Bets、Pair Bets、籌碼區、Timer |
| **NO_MORE_BETS 停止投注** | 投注區 `_Locked` 灰化、StatusBanner |
| **DEALING 發牌中** | Dealer Card(視訊)、扑克(手牌)、MB_开牌、StatusBanner(發牌中…)、投注區 `_Locked` |
| **SETTLEMENT 結算** | ResultToast、投注區 `_Win/_Lose`、結算列、Roadmap 即時更新 |

---

## 十一、命名對照（交接用）

| 類別 | 前綴 | 範例 |
|---|---|---|
| 投注區 | `Bet_` | `Bet_Player`、`Bet_Tie`、`Bet_Banker`、`Bet_PlayerPair` |
| 籌碼 | `Chip_` | `Chip_100_Selected` |
| 按鈕 | `btn_` | `btn_barMenu`、`btn_chevronBackward` |
| 路紙 | `Road_` | `Road_BigRoad`、`Road_BeadPlate` |
| 牌 | `Card_` | `Card_Player_1`、`Card_Banker_2` |
| 狀態 | `Status_` | `StatusBanner`、`ResultToast`、`Timer` |

> 狀態後綴：`_Default / _Hover / _Active / _Locked / _Win / _Lose`。

---

*產生自 Figma Section `152:106273`（41 節點）。分類與用途為依 Vercel 設計語言與百家樂流程整理之說明文件。*
