# LIFF 定位驗證 — 你要做的部分

只有這兩段非你不可（要用你的帳號登入），其餘我處理。

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
   - Endpoint URL：**（等我給你網址後再填）**
   - Scopes：勾 **profile**、**openid**
   - Bot link feature：Off
5. 建好後會出現一組 **LIFF ID**（長得像 `2001234567-abcdefgh`）→ 複製給我

## B. 現場實測（約 10 分鐘）

我把 LIFF ID 填好、網址給你之後：

1. 你自己先在**店裡**用 LINE 開一次，按「取得目前位置」
2. 找一位店員，用**他的手機**（最好是 Android，跟你的 iPhone 做對照）也開一次
3. 站在**店門口**按「把目前位置設為基準點」
4. 走到**店內最裡面**、**廚房**、**騎樓外**各按一次「取得目前位置」
5. 按「連續取樣 20 秒」，放著別動
6. 最後按「產生報告」→ 長按複製 → 傳給我

## 判讀（頁面會自己算，你不用記）

| 結果 | 意思 |
|---|---|
| ✅ 通過 | 精準度中位數 ≤40m、最差 ≤100m、最慢 ≤8 秒 → 可以做 |
| ⚠ 勉強 | 定位不穩，門市半徑可能要從 20m 放寬 |
| ❌ 不通過 | LIFF 內定位撐不住打卡，整案要改走別的方向 |

## 這支測試頁不會碰到什麼

- 不呼叫任何 Apps Script 後端，**不 POST 任何資料**
- 不使用 localStorage（正式系統的 `mala_clock_device` 完全不受影響）
- 不含任何門市座標、員工金鑰、試算表 ID
- **不會產生任何打卡紀錄**（頁面最上方有紅字警告，店員不會誤會）
- 基準點只存 sessionStorage，關掉分頁就消失
