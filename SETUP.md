# LIFF 定位驗證 — 你要做的部分

只有這幾段非你不可（要用你的帳號登入 / 要人在店裡），其餘我處理。

測試頁網址：**https://eason0728.github.io/mala-clock-liff/spike/gps-test.html**

---

## A. 到 LINE Developers 建 channel（約 15 分鐘）

1. 開 https://developers.line.biz/console/ ，用你的 LINE 帳號登入
2. **建 Provider**（如果還沒有）→ 名稱建議填 **鼎兆元**
   - ⚠ 之後打卡相關的 channel 全都要建在**同一個 Provider 底下**，
     userId 才會一致，跨店支援才認得出是同一個人
3. 在該 Provider 下 → **Create a new channel** → 選 **LINE Login**
   - Channel name：`鼎兆元打卡`
   - App types：勾 **Web app**
4. 進入該 channel → 上方 **LIFF** 分頁 → **Add**
   - LIFF app name：`打卡定位測試`
   - Size：**Full**
   - Endpoint URL：`https://eason0728.github.io/mala-clock-liff/spike/gps-test.html`
   - Scopes：勾 **profile**、**openid**
   - Bot link feature：Off
5. 建好後會出現一組 **LIFF ID**（長得像 `2001234567-abcdefgh`）→ 複製給我

---

## B. 事前準備：查出三家店的門口座標

**用 Google 地圖的固定座標當基準點，比現場按「設為基準點」準得多**——
現場設的基準點自己就帶著 ±30m 誤差，拿它去量另一個 ±30m 的點，誤差是疊加的。

怎麼查：

- **手機**：Google 地圖上長按店門口 → 底部卡片會顯示座標 → 點一下複製
- **電腦**：Google 地圖上對店門口按右鍵 → 選單最上面那行就是座標 → 點一下複製

抄下來長這樣：`24.801234, 120.971234`

> 測試頁的座標欄三種貼法都吃：純座標、Google 地圖網址、度分秒。
> 貼反了（經緯度顛倒）會跳出警告，不會默默算錯。

---

## C. 現場實測（約 10 分鐘）

我把 LIFF ID 填好之後：

1. **先做對照組**：在店裡用**一般瀏覽器**（Safari／Chrome）開測試頁，按「取得目前位置」
   - 這是你手機 GPS 的基準值，用來對照 LINE 內建瀏覽器有沒有讓定位變差
2. 改用 **LINE** 開同一個 LIFF，按「取得目前位置」
3. 在第④區貼上剛才查到的**店門口座標**，按「用這組座標當基準點」
4. 走到**店內最裡面**、**廚房**、**騎樓外**各按一次「取得目前位置」，看距離與判定
5. 按「連續取樣 20 秒」，放著別動
6. 找一位店員用**他的手機**（最好是 Android，跟你的 iPhone 做對照）重跑一次 2～5
7. 按「產生報告」→ 長按複製 → 傳給我

---

## 判讀（頁面會自己算，你不用記）

| 結果 | 意思 |
|---|---|
| ✅ 通過 | 精準度中位數 ≤40m、最差 ≤100m、最慢 ≤8 秒 → 可以做 |
| ⚠ 勉強 | 定位不穩，門市半徑可能要從 20m 放寬 |
| ❌ 不通過 | LIFF 內定位撐不住打卡，整案要改走別的方向 |

---

## 這支測試頁不會碰到什麼

- 不呼叫任何 Apps Script 後端，**不 POST 任何資料**
- 不使用 localStorage（正式系統的 `mala_clock_device` 完全不受影響）
- 不含任何門市座標、員工金鑰、試算表 ID（座標由你當場貼）
- **不會產生任何打卡紀錄**（頁面最上方有紅字警告，店員不會誤會）
- 基準點只存 sessionStorage，關掉分頁就消失
