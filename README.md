# Rails Migration Notes

Ruby on Rails（RoR）網站搬遷指南，說明如何準備目標環境、停止寫入、搬移資料、驗證結果、輪替憑證與安排回復。搭配檢查表、切換與驗收模板，以及 AI 計畫審閱 skill，逐步完成搬遷規劃。

## 適用範圍

適用於既有 Rails 網站更換主機或部署環境，且可以安排維護窗口、停止寫入後搬移資料的情境。使用前確認應用版本、資料庫、背景工作與部署方式，據此選擇實際指令、還原方式與切換順序。

本指南提供流程、檢查方法與模板，不含自動搬遷程式。Rails 升級、資料庫 schema migration、跨資料庫引擎轉換、無停機切換、多地寫入，以及網域變更的 SEO 遷移，不在涵蓋範圍內。

## 從這裡開始

| 你想做什麼 | 建議閱讀 |
| --- | --- |
| 留下一張隨時可看的提醒清單 | [搬家前後檢查表](skills/rails-migration-review/assets/readiness.md) |
| 請 AI 幫忙找出計畫中的盲點 | [rails-migration-review skill](skills/rails-migration-review/SKILL.md) |
| 審閱停寫與回復安排 | [切換與回復](skills/rails-migration-review/references/cutover.md) |
| 檢查環境設定與敏感憑證輪替 | [環境設定與憑證輪替](skills/rails-migration-review/references/cutover.md#環境設定與憑證輪替) |
| 確認驗收證據是否足夠 | [驗證方法](skills/rails-migration-review/references/verification.md) |
| 記錄切換步驟與停止條件 | [切換計畫模板](skills/rails-migration-review/assets/cutover-plan.md) |
| 記錄驗收結果與待處理項目 | [驗收紀錄模板](skills/rails-migration-review/assets/acceptance.md) |

## 搬遷流程

| 階段 | 要完成的工作 |
| --- | --- |
| 盤點與準備 | 列出服務、資料、附件與外部相依，準備目標環境並演練備份還原 |
| 安排切換 | 訂出維護窗口、停止條件、回復方式、驗收範圍與憑證輪替時程 |
| 停止寫入 | 控制網站、背景工作、排程與外部事件，處理在途操作，確認最終資料邊界 |
| 搬移與驗證 | 取得最終資料、還原至目標環境，比對資料與附件並驗證主要功能 |
| 開放與觀察 | 切換入口、啟用預定的工作與排程，確認使用者流程、背景結果與監測 |
| 收尾與交接 | 完成應輪替的憑證與舊存取撤銷，確認備份及後續部署，再依條件退役舊環境 |

憑證輪替依使用端相依安排在切換前、切換中或切換後；疑似洩漏時立即處理。新站開始接受寫入後，回復必須納入新產生的資料。

檢查表適合快速檢視計畫；需要分工或留下驗收依據時，再選用完整模板。填寫後的文件可能包含環境資訊與操作證據，請存放於自己的私有工作區。

## 使用 skill

將整個 `skills/rails-migration-review` 資料夾放到目標專案的 `.agents/skills/` 中；若已有同名 skill，先比較再合併。這是 Codex 支援的專案內 skill 位置，詳見 [OpenAI 官方說明](https://learn.chatgpt.com/docs/build-skills)。

範例請求：

> 使用 $rails-migration-review，幫我看看這份 Rails 網站搬家計畫有哪些盲點。我們可以安排停寫維護窗口，請先說最需要注意的問題、原因，以及我該補問什麼。

提供計畫時，可附上預計的維護窗口、資料搬移方式、背景工作安排與驗收條件。Skill 會指出重要缺口、說明原因，並提出需要確認的問題；它不會自動操作正式環境。

## 授權

本 repo 的文件、檢查表、模板與 skill 採用 [MIT License](LICENSE)。歡迎使用、修改、轉分享與商業使用；重用時請保留著作權與授權聲明。外部連結內容依各來源的授權規定。
