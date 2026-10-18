# Rails Migration Notes

這份方法筆記源自一次 Ruby on Rails（RoR）網站更換主機與部署環境的經驗，提供搬家前後的檢查表、切換與驗收模板，以及協助 AI 審閱計畫的 skill。

內容從實務經驗與事後歸納整理，聚焦停寫、資料完整性、回復與驗收，應依自己的環境選用。

## 適用範圍

主要討論既有 Rails 網站更換執行環境，且可以安排維護窗口、停止寫入後搬移資料的情境。內容提供檢查問題與計畫審閱方法；實際指令、還原方式與切換順序，需要依應用版本和部署方式確認。

這份筆記沒有跨框架實測，也不包含自動搬遷程式。Rails 升級、資料庫 schema migration、跨資料庫引擎轉換、無停機切換、多地寫入，以及網域變更的 SEO 遷移，都不在涵蓋範圍內。

## 從這裡開始

| 你想做什麼 | 建議閱讀 |
| --- | --- |
| 留下一張隨時可看的提醒清單 | [搬家前後檢查表](skills/rails-migration-review/assets/readiness.md) |
| 請 AI 幫忙找出計畫中的盲點 | [rails-migration-review skill](skills/rails-migration-review/SKILL.md) |
| 審閱停寫與回復安排 | [切換與回復](skills/rails-migration-review/references/cutover.md) |
| 確認驗收證據是否足夠 | [驗證方法](skills/rails-migration-review/references/verification.md) |
| 記錄切換步驟與停止條件 | [切換計畫模板](skills/rails-migration-review/assets/cutover-plan.md) |
| 記錄驗收結果與待處理項目 | [驗收紀錄模板](skills/rails-migration-review/assets/acceptance.md) |

## 從經驗提煉的提醒

| 經驗帶來的問題 | 下次可以怎麼問 |
| --- | --- |
| 有備份，仍可能漏掉備份後的資料 | 最後一筆允許寫入的資料，在哪裡劃線？ |
| 維護頁已開，其他程序仍可能工作 | 還有哪些地方能繼續寫入？ |
| 文件寫得完整，現場仍可能不同 | 這個結論是查到的，還是推測的？ |
| 新站看起來正常，業務未必全部完成 | 使用者要完成的事情，最後一步是什麼？ |
| 舊主機留著，仍不一定能直接回去 | 新站產生的資料，回復時怎麼保留？ |
| 省下主機費，仍可能增加其他代價 | 省掉了什麼，也接受了哪些限制？ |

檢查表適合快速檢視計畫；需要分工或留下驗收依據時，再選用完整模板。填寫後的文件可能包含環境資訊與操作證據，請存放於自己的私有工作區。

## 使用 skill

將整個 `skills/rails-migration-review` 資料夾放到目標專案的 `.agents/skills/` 中；若已有同名 skill，先比較再合併。這是 Codex 支援的專案內 skill 位置，詳見 [OpenAI 官方說明](https://learn.chatgpt.com/docs/build-skills)。

範例請求：

> 使用 $rails-migration-review，幫我看看這份 Rails 網站搬家計畫有哪些盲點。我們可以安排停寫維護窗口，請先說最需要注意的問題、原因，以及我該補問什麼。

提供計畫時，可附上預計的維護窗口、資料搬移方式、背景工作安排與驗收條件。Skill 會指出重要缺口、說明原因，並提出需要確認的問題；它不會自動操作正式環境。

參考資料中的公開技術文件用於說明原則，不代表原案例使用過該產品。

## 授權

本 repo 的文件、檢查表、模板與 skill 採用 [MIT License](LICENSE)。歡迎使用、修改、轉分享與商業使用；重用時請保留著作權與授權聲明。外部連結內容依各來源的授權規定。
