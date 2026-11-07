# 相片預備工具 v1.0 — © SCOUT SYSTEM

公開工具站：瀏覽器本地相片預備。上載一張相，在你部機上重新編碼成 JPEG／WebP／PNG，壓到目標大小（預設 500KB）、揀最長邊，前後大小對照，然後下載。

## 用途

- 相片重新編碼／轉格式：JPEG、WebP、PNG
- 壓到目標大小（KB），預設 500KB
- 揀最長邊（px），空着則不改變尺寸
- 前後大小對照，處理後下載

## 點用

1. 點選或把相片拖曳到上載區（每次一張）。
2. 揀格式、目標大小 KB（預設 500）、最長邊 px（不填＝不變）。
3. 按「預備相片」——全部處理喺你嘅瀏覽器本地，相片不上載去任何伺服器。
4. 對照原圖與處理後大小／尺寸，按「下載處理後相片」儲存。

## 限制（誠實寫明，唔扮可以做到嘅事）

- **做唔到無損壓縮**：JPEG／WebP 重新編碼會捨畫質；PNG 本身無損，但要達到細目標大小必須縮圖。
- **壓得太細會起格**：目標設得過低，輸出會出現壓縮噪點／色塊，請視可接受畫質調高目標大小。
- **EXIF 自動移除**：經 Canvas 重新編碼時 EXIF 段不會被拷貝，輸出檔不帶 EXIF（拍攝參數、GPS 等會遺失，係設計行為，處理後唔可恢復）。
- **每次一張相**：單一 HTML 工具，不設批次。

## 私隱承諾（呢個工具嘅最大賣點）

全部處理喺你嘅瀏覽器本地（FileReader + Canvas + toBlob），相片**不會上載去任何伺服器，不離開你部機**。本工具**無後端、不設 API、唔 call 任何 AI 模型**（壓縮、轉格式、去 EXIF 係死運算），絕不將用戶相片傳出去。

## 技術規定

- Type A 單一 HTML：`photo_prep_v1.0.html`，無後端、無外部依賴、零 CDN、離線打開亦可用。
- 雙版號 v1.0（真理倉 docs/13 規矩）：檔名同內文（`<meta name="app-version">`、標題、`APP_VERSION` 常數、頁尾、檔頭註解）同步。
- 版權：`© SCOUT SYSTEM`（真理倉 W1 規矩，見頁尾同 `<meta name="copyright">`）。
- 授權：可自由使用／改作，須保留版權標示；請勿移除版權標示。

## 測試結果（2026-11-07）

| 項目 | 結果 | 備註 |
|---|---|---|
| `scripts/audit_single_html_v1.0.mjs` 靜態審計 | ✅ PASS | 0 FAIL（見下方輸出） |
| `scripts/guard.mjs` | ✅ PASS | 0 項錯 |
| JPEG 輸出 ≤ 500KB | 未測 | 需真實相片＋瀏覽器；沙箱未有瀏覽器 |
| WebP 輸出 ≤ 500KB | 未測 | 同上 |
| PNG 輸出 ≤ 500KB | 未測 | 同上 |
| 壓完 EXIF 確認移除 | 未測 | 頁面內建了本機 APP1/EXIF 段掃描，待實機驗證 |
| 手機瀏覽器打開／流暢度 | 未測 | 沒有實機／行動瀏覽器可用 |

未測項目明寫未測，並未扮測過。實測後請把結果補進此表。

## 建立說明

真理倉 `github.com/playerkousas-rgb/readme` 的 `templates/iconmaker/photo_prep_v1.0.html` 在該倉內**未找到**（該倉 `templates/` 內只有 canvas/gas/git/github/repo-starter/reverse-api-demo/supabase/vercel/watermark）。故此 repo 的 `photo_prep_v1.0.html` 是按本 README 規格新建的 Type A 單一 HTML，**未從真理倉複製現成檔案，也未在真理倉內作任何改動**（真理倉只供參考規範：scripts/guard.mjs、audit_single_html_v1.0.mjs、.gitignore、vercel.json 等）。

## Vercel 部署

- 靜態站，無登入即可使用；`vercel.json` 已設 `regions: ["hkg1"]` 同安全響應頭。
- 根目錄首頁以 `index.html` 提供（內容與 `photo_prep_v1.0.html` 一致），`photo_prep_v1.0.html` 為交付主頁。
- `.vercelignore` 已擋 `node_modules/.git/docs/*.md` 等不上載項目。

> 真理倉 W1：© SCOUT SYSTEM · 相片預備工具 v1.0
