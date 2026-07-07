# Product Requirements Document
# Bet Stacker Blackjack

---

| 欄位 Field | 內容 Content |
|---|---|
| 文件版本 Version | v1.3 |
| 撰寫日期 Date | 2026-05-26 |
| 狀態 Status | Draft |
| 適用對象 Audience | 產品 × 設計團隊 Product & Design Team |

---

## 1. 產品概覽 Product Overview

### 1.1 背景 Background

本產品為傳統七座位 21 點（Classic 7-seat Blackjack）的變體版本。在保留原有 21 點核心規則的基礎上，引入了「**疊加賭注（Bet Stacker）**」隨機獎勵機制，為玩家在每一局開局階段創造額外的注碼擴大機會，進而爭取更高的潛在派彩。

This game is a variant of classic 7-seat Blackjack. It preserves standard Blackjack rules while introducing the **Bet Stacker** mechanic — a randomised bonus phase at the start of each round that allows players to amplify their stake before gameplay begins, unlocking higher potential payouts.

### 1.2 遊戲主軸 Core Proposition

> 傳統 21 點 × 隨機疊注機制 → 低技術門檻、高期待回報、節奏緊湊
>
> Classic Blackjack × Randomised Bet-Stacking → low skill barrier, elevated payout potential, fast session rhythm

### 1.3 目標玩家 Target Players

- 熟悉傳統 21 點規則的休閒玩家 Casual players familiar with standard Blackjack
- 尋求額外隨機獎勵刺激感的玩家 Players who enjoy randomised reward spikes
- 喜好中短場次、快速節奏的玩家 Players who prefer short-to-medium sessions with brisk pacing

---

## 2. 名詞定義 Glossary

| 術語 Term | 定義 Definition |
|---|---|
| 主注 Main Bet | 玩家每局必須放置的基礎賭注 The primary wager a player must place each round |
| 邊注 Side Bet | 玩家自願放置的附加賭注（非強制）An optional supplementary wager |
| 後面跟注 Bet Behind | 跟隨其他座位玩家下注的機制 Wagering on another seated player's hand |
| Bet Stacker 費用 | 主注 / 後面跟注金額的 10%，系統自動扣除 A 10% surcharge auto-collected on Main Bet & Bet Behind |
| 獎勵元素 Bonus Element | 每局隨機抽取的一個牌面點數（Rank），例如 7、K A randomly drawn card Rank per round (e.g. 7, K) |
| 獎金乘數 Bonus Multiplier | 25% / 50% / 75% / 100% 四選一，隨機決定 One of four multipliers randomly selected each round |
| 獎金價值 Bonus Value | 主注 × 獎金乘數的計算結果 Main Bet × Bonus Multiplier |
| 疊加 Stack | 將獎金價值直接加入玩家主注的動作 Adding Bonus Value on top of the player's Main Bet |
| 套現 Cashout | 玩家提早結算、放棄繼續牌局並拿走估算金額的功能 Early settlement option based on current hand vs dealer's upcard |
| 軟 17 Soft 17 | 含 Ace 且計為 11 的 17 點手牌 A 17-point hand containing an Ace counted as 11 |
| 爆牌 Bust | 手牌點數超過 21 Hand value exceeding 21 |

---

## 3. 遊戲核心規則 Core Game Rules

### 3.1 基本目標 Objective

玩家的最終手牌點數必須**比莊家更接近 21 點**，且**不得超過 21 點（爆牌）**。  
The player's final hand must be **closer to 21 than the dealer's**, without **exceeding 21 (bust)**.

- 若開局前兩張牌點數合計剛好為 21 → **Blackjack**（自動勝利，賠率 **6 : 5**）  
  If the first two cards total 21 → **Blackjack** (automatic win, pays **6 : 5**)

### 3.2 牌面計算 Card Values

| 牌面 Card | 點數 Value |
|---|---|
| 2 – 10 | 面值 Face value |
| J / Q / K | 10 |
| A（Ace） | 1 或 11（以不爆牌為優先）1 or 11 (whichever avoids bust) |

### 3.3 莊家限制 Dealer Rules

| 手牌狀況 Dealer Hand | 動作 Action |
|---|---|
| ≤ 16 點 | 強制要牌 Must Hit |
| Soft 17（含）以上 | 強制停牌 Must Stand |

### 3.4 標準玩家操作 Standard Player Actions

| 操作 Action | 條件 Condition | 說明 Description |
|---|---|---|
| 停牌 Stand | 任意時機 Any time | 不再要牌，保持當前點數 Keep current hand |
| 要牌 Hit | 任意時機 Any time | 再抽一張牌 Draw one more card |
| 加倍 Double Down | 僅初始兩張牌 Initial 2 cards only | 加注一倍，且只能再抽一張牌 Double the bet, receive exactly one more card |
| 分牌 Split | 初始兩張牌點數相同 Pair on initial 2 cards | 分成兩手各自遊玩；**分牌後不可再次分牌（Re-split 不允許）** Split into two separate hands; **Re-split is not permitted** |

---

## 4. Bet Stacker 機制 Bet Stacker Mechanic

### 4.1 概覽 Overview

Bet Stacker 是本遊戲的獨家特色，在每一局中為玩家創造「隨機擴大注碼」的機會。整個機制分為三個階段：

Bet Stacker is the defining feature of this game, creating a randomised bet-amplification opportunity each round. It operates in three phases:

```
[下注階段] → [Bet Stacker Phase（隨機抽獎）] → [常規牌局操作]
[Betting]  →  [Bet Stacker Phase (RNG)]      →  [Standard Play]
```

---

### 4.2 Bet Stacker 費用 Surcharge

- **觸發條件**：玩家放置主注或後面跟注時自動觸發  
  **Trigger**: Automatically applied when placing Main Bet or Bet Behind
- **費率**：主注 / 後面跟注金額的 **10%**  
  **Rate**: **10%** of the Main Bet or Bet Behind amount
- **說明**：此費用為參與 Bet Stacker 機制的必要成本，不可選擇退出  
  **Note**: This surcharge is mandatory for participation and cannot be opted out
- **後面跟注（Bet Behind）疊注規則**：後面跟注者享有與座位主玩家**相同的 Bet Stacker 疊加結果**；若座位主玩家手牌觸發疊注，跟注者的賭注亦同步疊加相應獎金價值  
  **Bet Behind Stacking Rule**: Bet Behind players receive the **same Bet Stacker outcome as the seat player**; if the seat player's hand triggers a stack, the Bet Behind wager is stacked by the same Bonus Value proportionally

> **範例 Example**：主注 $100 → 自動收取 $10 Bet Stacker 費用  
> Main Bet $100 → $10 Bet Stacker surcharge auto-deducted

---

### 4.3 隨機獎勵元素生成 Bonus Element Generation

每局開始時，系統進行兩次獨立隨機抽取：  
At the start of each round, the system performs two independent random draws:

| 隨機項目 Random Item | 說明 Description | 範例 Example |
|---|---|---|
| **獎勵元素（Bonus Element）** | 從 A、2–10、J、Q、K 中隨機抽取一個點數（Rank） Randomly draw one Rank from A, 2–10, J, Q, K | `7` |
| **獎金乘數（Bonus Multiplier）** | 從 25%、50%、75%、100% 中隨機抽取一個乘數 Randomly draw one multiplier from 25%, 50%, 75%, 100% | `75%` |

> **獎金價值計算 Bonus Value Calculation**：  
> `獎金價值 = 主注 × 獎金乘數`  
> `Bonus Value = Main Bet × Bonus Multiplier`  
>
> 範例 Example：主注 $100 × 75% = **$75 獎金價值 Bonus Value**

---

### 4.4 疊注判定 Stack Determination

發完初始兩張牌後，系統進行以下判定：  
After dealing the initial two cards, the system evaluates:

```
IF 玩家手牌中任意一張（或兩張）的 Rank == 獎勵元素 Rank
THEN 將獎金價值疊加到玩家主注上
ELSE 主注維持原金額不變
```

| 手牌情境 Scenario | 疊加次數 Stacks | 結果 Result |
|---|---|---|
| 兩張牌都不符合 Neither card matches | 0 | 無疊加 No stack |
| 一張牌符合 One card matches | 1 | 主注 + 1× 獎金價值 Main Bet + 1× Bonus Value |
| 兩張牌都符合（對子）Both cards match (pair) | 2 | 主注 + 2× 獎金價值 Main Bet + 2× Bonus Value |

> **範例 Example（兩張都符合）**：  
> 主注 $100，獎金價值 $75，兩張牌都為 7  
> 新注碼 = $100 + $75 + $75 = **$250**  
> Main Bet $100, Bonus Value $75, both cards are 7  
> New stake = $100 + $75 + $75 = **$250**

---

### 4.5 操作連動規則 Action Interaction Rules

疊加完成後，新注碼金額（Main Bet + 累積 Bonus Value）將作為後續所有操作的計算基礎：  
After stacking, the new stake (Main Bet + accumulated Bonus Value) becomes the basis for all subsequent actions:

#### 4.5.1 分牌 Split

- 分牌後的**每一手**均繼承**原始賭注 + 已獲得的疊加獎金價值**  
  Each split hand inherits the **original bet + all accumulated Bonus Value**
- 若分牌後的新手牌也符合獎勵元素，不再進行額外疊加  
  Further Bet Stacker stacking does not apply to post-split hands

> **範例**：主注 $100 + 疊加 $75 = $250 新注碼  
> 分牌後：手牌 A = $250，手牌 B = $250  
> Split result: Hand A = $250, Hand B = $250

#### 4.5.2 加倍 Double Down

- 加倍時，新賭注的計算基礎為**已疊加後的新注碼總額**  
  Double Down wager is calculated from the **new stacked stake total**
- 加倍金額 = 新注碼總額（再押一次相同金額）  
  Additional bet = current stacked stake (matched in full)

> **範例**：新注碼 $250 → 加倍需再押 $250，總風險 = $500  
> Example: Stacked stake $250 → Double Down adds another $250, total at risk = $500

---

## 5. 邊注規格 Side Bet Specifications

邊注為玩家自願參與的附加賭注，獨立於主注結算，不影響 Bet Stacker 機制的運作。  
Side bets are optional wagers settled independently from the Main Bet and do not interact with the Bet Stacker mechanic.

### 5.1 邊注總覽 Side Bet Overview

| 邊注名稱 Side Bet | 判定牌張 Cards Used | 結算時機 Settlement Timing |
|---|---|---|
| Perfect Pairs | 玩家初始兩張牌 Player's initial 2 cards | 發牌後立即結算 Settled immediately after deal |
| 21+3 | 玩家初始兩張牌 + 莊家明牌 Player's 2 cards + Dealer's upcard | 發牌後立即結算 Settled immediately after deal |
| HOT 3 | 玩家初始兩張牌 + 莊家明牌 Player's 2 cards + Dealer's upcard | 發牌後立即結算 Settled immediately after deal |
| Bust Bonus | 莊家最終手牌（爆牌時）Dealer's final hand (bust only) | 莊家爆牌時結算 Settled when dealer busts |

---

### 5.2 Perfect Pairs

**判定邏輯 Determination Logic**

玩家初始兩張牌的**點數（Rank）與花色（Suit）完全相同**即獲勝。  
Player wins when both initial cards share the **exact same Rank AND Suit**.

| 牌型 Hand Type | 條件 Condition | 賠率 Payout |
|---|---|---|
| Perfect Pair | 兩張牌點數相同 + 花色相同 Same Rank + Same Suit | **25 : 1** |
| 其他 Any other combination | — | 輸 Lose |

> **範例 Example**：♠7 + ♠7 → Perfect Pair，賠率 25:1  
> ♠7 + ♥7 → 不符合，邊注輸 Not a Perfect Pair, side bet lost

**設計備注 Design Note**：  
使用多副牌（Multi-deck）時，相同點數 + 相同花色的組合仍可成立（例如兩副牌各一張 ♠7）。需確認平台使用牌副數量以評估機率。  
In a multi-deck shoe, identical Rank + Suit combinations remain valid. Confirm deck count for probability calibration.

---

### 5.3 21+3

**判定邏輯 Determination Logic**

取**玩家初始兩張牌**加上**莊家明牌**，共三張牌，組成撲克牌型。以下牌型由高至低排列：  
Three cards — player's initial 2 + dealer's upcard — form a poker hand. Ranked highest to lowest:

| 牌型 Hand Type | 定義 Definition | 賠率 Payout |
|---|---|---|
| Suited Trips（三條同花） | 三張點數相同 + 花色相同 Three cards: same Rank AND same Suit | **100 : 1** |
| Straight Flush（同花順） | 三張連號 + 花色相同 Three consecutive Ranks + same Suit | **40 : 1** |
| Three of a Kind（三條） | 三張點數相同，花色不同 Three cards: same Rank, any Suit | **30 : 1** |
| Straight（順子） | 三張連號，花色不限 Three consecutive Ranks, any Suit | **10 : 1** |
| Flush（同花） | 三張花色相同，非連號 Three cards: same Suit, not consecutive | **5 : 1** |
| 其他 No qualifying hand | — | 輸 Lose |

> **範例 Examples**：  
> ♠7 + ♠8 + ♠9 → Straight Flush，賠率 40:1  
> ♣K + ♠K + ♥K → Three of a Kind，賠率 30:1  
> ♦3 + ♦3 + ♦3 → Suited Trips，賠率 100:1

**點數連號規則 Rank Sequence Rules**：  
A 可作為最低牌（A-2-3）或最高牌（Q-K-A），但不可繞圈（K-A-2 不成立）。  
Ace plays as low (A-2-3) or high (Q-K-A); wrap-around (K-A-2) is not valid.

---

### 5.4 HOT 3

**判定邏輯 Determination Logic**

取**玩家初始兩張牌**加上**莊家明牌**，共三張牌的**點數總和**決定派彩。  
The **sum of point values** of player's initial 2 cards + dealer's upcard determines the payout.

| 三牌點數總和 Three-Card Total | 賠率 Payout |
|---|---|
| **21** | **10 : 1** |
| **20** | **4 : 1** |
| **19** | **2 : 1** |
| 18 以下或超過 21 Below 18 or above 21 | 輸 Lose |

> **範例 Examples**：  
> 玩家 7 + 5，莊家明牌 8 → 總和 20，賠率 4:1  
> 玩家 A + K，莊家明牌 10 → 總和 21，賠率 10:1（A 計為 11）

**Ace 計算規則 Ace Counting**：  
HOT 3 計算中，A 優先計為 **11**（若總和不超過 21）。  
In HOT 3 calculation, Ace counts as **11** (unless total exceeds 21, then counts as 1).

---

### 5.5 Bust Bonus

**判定邏輯 Determination Logic**

**玩家停牌（Stand）後**，若莊家最終手牌超過 21 點（爆牌），根據**莊家爆牌時的手牌總張數**決定派彩。  
**After the player Stands**, if the dealer's final hand exceeds 21 (busts), payout is determined by the **total number of cards in the dealer's busted hand**.

| 莊家爆牌張數 Dealer Bust Card Count | 賠率 Payout |
|---|---|
| 3 張 3 cards | **1 : 1** |
| 4 張 4 cards | **2 : 1** |
| 5 張 5 cards | **9 : 1** |
| 6 張 6 cards | **50 : 1** |
| 7 張以上 7+ cards | **100 : 1** |
| 莊家未爆牌 Dealer does not bust | 輸 Lose |

> **範例 Examples**：  
> 莊家以 5 張牌爆牌（如 6+4+5+8+1）→ 賠率 9:1  
> Dealer busts with 5 cards (e.g. 6+4+5+8+1) → Payout 9:1  
>
> 莊家以 7 張牌爆牌 → 賠率 100:1  
> Dealer busts with 7 cards → Payout 100:1

**觸發限制 Trigger Conditions**：

- 僅在**玩家選擇停牌（Stand）後**該邊注才有效；玩家若爆牌（Bust），Bust Bonus 視為輸  
  Bust Bonus is only active if the **player Stands**; if the player busts, the side bet is lost regardless of the dealer's outcome
- 玩家 Blackjack 時，邊注仍正常結算（莊家需翻牌後才結算）  
  If player has Blackjack, the side bet still settles after the dealer reveals their hole card

---

### 5.6 邊注通用規則 General Side Bet Rules

- 邊注獨立結算，**不受主注勝負影響** Side bets settle independently; main hand outcome does not affect them
- 邊注**不受 Bet Stacker 疊注機制影響** Side bets are **not subject to Bet Stacker stacking**
- 邊注最低 / 最高注額依桌面設定，與主注上下限分開計算 Min/max side bet limits are set separately from main bet limits
- 玩家在主注 Blackjack 時，邊注仍正常結算 Side bets settle normally even when the player has Blackjack

---

## 6. 套現功能 Cashout Feature  

### 5.1 功能描述 Description

玩家在操作階段（Hit / Stand 選擇前）可隨時選擇**提早結算（Cashout）**，無需等待牌局完整結束。  
At any point during the action phase (before selecting Hit/Stand), the player may choose **early settlement (Cashout)** without waiting for the round to conclude.

### 5.2 派彩計算邏輯 Payout Calculation Logic

套現金額由系統根據以下因素即時估算：  
The Cashout amount is calculated in real-time based on:

- 玩家當前手牌點數及組合 Player's current hand value and composition
- 莊家明牌（可見的那張）Dealer's upcard (visible card)
- 當前注碼（含疊加後的新注碼）Current stake (including stacked bonus)

> **設計備注**：套現金額通常低於「玩到底並獲勝」的預期回報，以反映玩家提前規避莊家爆牌以外風險的成本。  
> **Design Note**: The Cashout amount will typically be less than the expected winning payout, reflecting the cost of early risk avoidance.

### 5.3 UI 要求 UI Requirements

- 套現按鈕需在玩家操作階段**顯著可見**且隨時可點擊  
  The Cashout button must be **prominently visible** and tappable throughout the player's action phase
- 按下後須顯示確認對話框，避免誤觸  
  Pressing must trigger a confirmation dialog to prevent accidental activation
- 即時顯示目前估算的套現金額（動態更新）  
  Display the current estimated Cashout value in real-time (dynamically updated)

---

## 6. 使用者流程 User Flow

```
開始新局
Start Round
    │
    ▼
[下注階段 Betting Phase]
玩家放置主注（必填）+ 邊注（選填）+ 後面跟注（選填）
Player places Main Bet (required) + Side Bets (optional) + Bet Behind (optional)
系統自動扣除 10% Bet Stacker 費用
System auto-deducts 10% Bet Stacker surcharge
    │
    ▼
[Bet Stacker Phase]
系統隨機抽取：獎勵元素（Rank）+ 獎金乘數（%）
System randomly draws: Bonus Element (Rank) + Bonus Multiplier (%)
UI 顯示：本局獎勵元素與獎金乘數
UI shows: This round's Bonus Element and Multiplier
    │
    ▼
[發牌 Deal]
莊家發初始兩張牌（玩家明牌 × 2，莊家一明一暗）
Dealer deals initial cards (Player: 2 face-up; Dealer: 1 up, 1 down)
    │
    ▼
[疊注判定 Stack Check]
玩家手牌 Rank 是否符合獎勵元素？
Does player hand match Bonus Element?
    ├── 符合 0 張 → 主注不變 Stake unchanged
    ├── 符合 1 張 → 主注 + 1× 獎金價值 Stake + 1× Bonus Value
    └── 符合 2 張 → 主注 + 2× 獎金價值 Stake + 2× Bonus Value
    │
    ▼
[Blackjack 檢查 Blackjack Check]
    ├── 玩家 Blackjack → 莊家是否也 Blackjack？
    │       ├── 是 → 平局 Push
    │       └── 否 → 玩家勝，Blackjack 賠率
    ├── 莊家 Blackjack → 玩家（非 Blackjack）負
    └── 雙方皆無 → 進入操作階段
    │
    ▼
[玩家操作階段 Player Action Phase]
玩家選擇：Stand / Hit / Double Down / Split / Cashout
Player chooses: Stand / Hit / Double Down / Split / Cashout
    ├── Cashout → 結算，領取估算金額，本局結束
    ├── Split  → 分成兩手，各繼承新注碼，分別操作
    ├── Double → 以新注碼為基礎加倍，只再抽一張牌
    ├── Hit    → 再抽一張牌，若爆牌 → 玩家負
    └── Stand  → 鎖定手牌，進入莊家操作
    │
    ▼
[莊家操作階段 Dealer Action Phase]
莊家翻開底牌，依規則 Hit（≤16）/ Stand（Soft 17+）
Dealer reveals hole card, Hits (≤16) / Stands (Soft 17+)
    │
    ▼
[結算 Settlement]
比較最終點數，派彩或收注
Compare final hands, pay or collect
    │
    ▼
新局開始 Next Round
```

---

## 7. UI 狀態規格 UI State Specifications

### 7.1 下注介面 Betting Interface

| 元素 Element | 狀態 State | 說明 Description |
|---|---|---|
| 主注籌碼區 Main Bet Area | 預設空白 Default empty | 玩家點擊籌碼放置主注 |
| 邊注區 Side Bet Area | 可選擇 Optional | 顯示各邊注類型與最低注額 |
| Bet Stacker 費用提示 | 主注放置後即時顯示 Show on Main Bet placement | 顯示「+10% Bet Stacker Fee：$XX」 |
| 確認下注按鈕 Confirm Bet | 主注放置後啟用 Enabled after Main Bet | 點擊後鎖定賭注，進入 Bet Stacker Phase |

### 7.2 Bet Stacker Phase 介面

| 元素 Element | 說明 Description |
|---|---|
| 獎勵元素展示區 Bonus Element Display | 醒目顯示本局隨機抽到的牌面點數（例：「🃏 7」） |
| 獎金乘數展示區 Bonus Multiplier Display | 顯示乘數（例：「× 75%」）及對應獎金價值（例：「+ $75」） |
| 動態動畫 Animation | 以轉盤 / 抽卡動效呈現隨機抽取過程，增強期待感 |
| 疊注結果提示 Stack Result | 判定後顯示「Stacked! +$75」或「No Stack」 |

### 7.3 玩家操作介面 Player Action Interface

| 按鈕 Button | 顯示條件 Display Condition |
|---|---|
| Stand | 始終顯示 Always visible |
| Hit | 始終顯示，爆牌後隱藏 Always visible, hidden after bust |
| Double Down | 僅初始兩張牌時顯示 Only on initial 2-card hand |
| Split | 初始兩張牌 Rank 相同時顯示 Only when initial pair matches |
| Cashout | 操作階段始終顯示，顯示即時估算金額 Always visible with live amount |

### 7.4 注碼顯示規則 Stake Display Rules

| 場景 Scenario | 顯示格式 Display Format |
|---|---|
| 疊加前 Before Stack | `主注：$100` |
| 疊加後 After Stack | `主注：$100 → $250（+$150 Stacked）` |
| 加倍後 After Double | `主注：$250 × 2 = $500` |
| 分牌後 After Split | 各手分別顯示 `$250` |

---

## 8. 數學模型摘要 Math Model Summary

### 8.1 Bet Stacker 費用 Surcharge

```
Bet Stacker Fee = (Main Bet + Bet Behind) × 10%
```

### 8.2 獎金價值 Bonus Value

```
Bonus Value = Main Bet × Bonus Multiplier
Bonus Multiplier ∈ { 25%, 50%, 75%, 100% }（各等機率 Equal probability）
```

### 8.3 疊注後新注碼 New Stacked Stake

```
New Stake = Main Bet + (Matched Cards Count × Bonus Value)
Matched Cards Count ∈ { 0, 1, 2 }
```

### 8.4 加倍後總注碼 Total after Double Down

```
Total at Risk = New Stake × 2
```

### 8.5 Blackjack 賠率 Blackjack Payout

- 一般勝利 Standard Win：**1 : 1**（以新注碼為基礎 based on New Stake）
- Blackjack 勝利 Blackjack Win：**6 : 5**（以新注碼為基礎 based on New Stake）
- 平局 Push：退還全額注碼 Full stake returned

> **範例 Example**：新注碼 $250 且達成 Blackjack → 派彩 $250 × 6/5 = **$300**（加上退還本金共 $550）  
> New Stake $250 with Blackjack → Payout $250 × 6/5 = **$300** (plus $250 stake returned = $550 total)

---

## 9. 邊界條件與異常處理 Edge Cases & Error Handling

| 情境 Scenario | 處理方式 Handling |
|---|---|
| 玩家在 Bet Stacker Phase 期間斷線 Disconnection during Bet Stacker Phase | 重新連線後恢復至斷線前狀態，獎勵元素已鎖定不重抽 Resume to pre-disconnect state; Bonus Element is locked |
| 分牌後手牌也為對子 Pair after Split | **Re-split 不允許**；分牌後若再得到對子，只能 Hit / Stand / Double，不得再次分牌 Re-split is **not permitted**; if a split hand forms another pair, player may only Hit, Stand, or Double |
| 主注為最低注額，獎金乘數 25% 時 Min Bet + 25% Multiplier | 獎金價值可為小數，系統四捨五入至最小貨幣單位 Bonus Value rounded to minimum currency unit |
| 加倍後注碼超過桌面上限 Double Down exceeds table max | 加倍上限為桌面最高注額，差額不退還疊加金 Capped at table maximum; difference is not refunded |
| 莊家與玩家同時 Blackjack | 平局（Push），退還含疊加金之全部注碼 Push: full stacked stake returned |
| 套現後手牌已自動勝出（估算錯誤）Cashout payout undervalues winning hand | 套現為玩家主動選擇，不予補差額 Cashout is player-initiated; no supplementary payout |

---

## 10. 驗收標準 Acceptance Criteria

### 10.1 Bet Stacker 費用

- [ ] 放置主注時，系統自動計算並顯示 10% 費用
- [ ] 放置後面跟注時，同樣自動扣取 10% 費用
- [ ] 費用金額在 UI 上清晰標示，不得隱藏

### 10.2 Bet Stacker Phase

- [ ] 每局必須隨機抽取一個獎勵元素（Rank）及一個獎金乘數
- [ ] 四個乘數選項（25% / 50% / 75% / 100%）機率相等
- [ ] 抽取結果在 UI 上有明確的視覺呈現
- [ ] 獎金價值計算公式：主注 × 乘數，精度至最小貨幣單位

### 10.3 疊注判定

- [ ] 發牌後自動比對玩家手牌 Rank 與獎勵元素
- [ ] 匹配 0 張：主注不變
- [ ] 匹配 1 張：主注 + 1× 獎金價值
- [ ] 匹配 2 張：主注 + 2× 獎金價值
- [ ] 疊加結果以動畫及數字清楚呈現

### 10.4 操作連動

- [ ] 分牌後每手繼承疊加後新注碼
- [ ] 加倍的基礎金額為疊加後新注碼（非原始主注）
- [ ] 加倍上限為桌面最高注額

### 10.5 套現

- [ ] 操作階段全程顯示 Cashout 按鈕及即時金額
- [ ] 點擊後顯示確認對話框
- [ ] 確認後立即結算，金額正確轉入玩家帳戶
- [ ] 套現金額邏輯基於玩家手牌 + 莊家明牌即時運算

### 10.6 莊家規則

- [ ] 手牌 ≤ 16 點必須要牌
- [ ] Soft 17（含）以上必須停牌
- [ ] 莊家翻牌動作有清晰動畫，流程不得省略

---

## 11. 待討論事項 Open Questions

| # | 問題 Question | 負責人 Owner | 截止日 Due |
|---|---|---|---|
| 1 | ~~邊注種類與賠率規格為何？What are the Side Bet types and payout odds?~~ | ~~產品 PM~~ | ✅ 已完成（見第 5 章）Resolved (see §5) |
| 2 | ~~Blackjack 賠率是 3:2 或 6:5？~~ | ~~產品 PM~~ | ✅ **6 : 5**（見 §3.1、§8.5）|
| 3 | 套現金額的精確演算法由數學組提供？Exact Cashout algorithm to be defined by math team? | 數學 Math | ⏸ **本版本暫不納入 Out of scope for v1** |
| 4 | ~~Bet Stacker 獎勵元素的隨機來源是否使用 RNG 憑證？~~ | ~~技術 Tech~~ | ✅ **無需 RNG 憑證 No certified RNG required** |
| 5 | ~~分牌後是否允許再次分牌（Re-split）？~~ | ~~產品 PM~~ | ✅ **不允許 Not permitted**（見 §3.4、§9）|
| 6 | ~~後面跟注（Bet Behind）的 Bet Stacker 疊加是否與座位主玩家相同？~~ | ~~產品 PM~~ | ✅ **是，相同 Yes, same stack applies**（見 §4.2）|
| 7 | ~~Bust Bonus 的具體賠率結構？What is the exact Bust Bonus payout structure?~~ | ~~產品 PM~~ | ✅ 已完成（見第 5.5 節）Resolved (see §5.5) |

---

*文件結束 End of Document*  
*如有修訂請更新版本號並記錄變更歷史 Please update version and change log upon revision*
