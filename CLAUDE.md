# food-calorie-tracker — 卡卡日記（拍照卡路里紀錄）

個人飲食記錄 PWA，單檔前端、無後端，2026-09-21 建立（原名「拍照卡路里紀錄」，同日改名「卡卡日記」；repo 名與網址不變）。本機預覽 port 8819。

## 功能
- 拍照或上傳食物照片（手機 `<input capture="environment">` 開原生相機；桌機可用即時鏡頭快照）→ BYOK 視覺 AI（Claude／OpenAI／Gemini／OpenRouter，`callLLM` 沿用 `product-title-generator`）估算品項與卡路里。
- **100% 依賴 AI 圖片辨識，沒有規則式備援**；沒填金鑰無法估算，畫面要誠實說明。
- AI 結果先放進**可編輯表格**（可改品項、份量、卡路里，可增刪列），使用者確認後才存進 IndexedDB（`foodCalorieTrackerDB`），不直接信任 AI 數字。
- 歷史紀錄可展開、原地編輯、刪除；今日總卡路里自動加總。
- **月份飲食分析**：統計數字（記錄天數、總攝取、平均、最高最低日、常見食物）全部在本機算好，只把這些數字交給 AI 做質性建議，AI 不重新計算數字。之後加功能（週報、營養素）沿用這個分工。
- JSON 完整備份（含照片）／CSV 匯出（不含照片），手法比照 `expense-tracker-pwa` 的 backup.js。

## 注意
- 健康相關：只做飲食紀錄與一般參考，**不可宣稱醫療或營養診斷**。
- Gemini 呼叫已套 `geminiModelFix()`。

## 部署
公開 repo，GitHub Actions 部署 Pages：<https://m255525.github.io/food-calorie-tracker/>。無序號、無 exe。

## 標準配備
跑馬燈（滑鼠移入暫停）、`manual.html`、使用警語、PWA（SW 只刪自己前綴的快取）、訪客計數器。

## 驗證
無自動化測試；改動後用工具健康檢查重查。測拍照流程時可用上傳圖片代替相機。
