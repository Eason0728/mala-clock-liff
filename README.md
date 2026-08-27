# mala-clock-liff

麻的小辛辣打卡系統 LINE 化（LIFF）的**獨立**工作區。

⚠ 與現有打卡系統 `~/mala-clock-in` **完全分離**，不共用任何資料、後端或儲存空間。

## 現況：階段 0（可行性驗證）

唯一的未知數是「LIFF 內建瀏覽器能不能穩定取得足夠精準的 GPS」。
`spike/gps-test.html` 就是回答這個問題的拋棄式測試頁。

- 純前端，零網路請求
- 驗證項目：LIFF init / getProfile / geolocation 精準度 / 取得耗時 / 距離計算
- 判定門檻對齊正式系統：精準度 40m、誤差折扣上限 100m、門市半徑 20m

操作步驟見 `SETUP.md`。

## 後續階段（驗證通過才做）

1. 後端加 userId↔員工對照表、綁定 handler（5 個後端各一份）
2. 前端身分層改用 `liff.getProfile()` 取代 `?k=` 金鑰
3. 全門市座標表 → 支援打卡自動標記地點
4. manager.html 也進 LIFF（店長不用再保管主管金鑰網址）
5. 圖文選單（一個官方帳號，per-user 選單區分店長/同仁）
