# CNEWS weather site

一個簡單的香港天氣頁面：顯示即時天氣、警告及未來預報，並每六小時自動更新。

資料來自香港天文台的官方開放數據 API。選用官方來源是因為出處清楚、可追溯；使用、複製或分發時須遵守 [DATA.GOV.HK 使用條款及條件](https://data.gov.hk/tc/terms-and-conditions)，並保留來源及知識產權聲明。

## 主要檔案

- `scripts/fetch-weather.mjs`：抓取香港天文台資料並原子地寫入 `data/weather.json`。
- `index.html`：無框架的天氣頁面，讀取 JSON 後顯示資料。
- `.github/workflows/update.yml`：每六小時抓取資料；有變化才 commit，然後部署 GitHub Pages。

## 本機使用

先以 Node.js 22+ 更新資料：

```sh
node scripts/fetch-weather.mjs
```

以本機 HTTP server 開啟頁面，例如：

```sh
python -m http.server 8000
```

然後瀏覽 `http://localhost:8000/`。直接 double-click `index.html` 可能因瀏覽器安全限制而不能 `fetch` 本機 JSON；請改用任何簡單的本機 HTTP server。

沒有網絡時，可暫時把 `data/weather.json` 以 `fixtures/weather-sample.json` 取代（或在 `index.html` 的 `fetch(...)` 暫改為該路徑）作示範；完成後還原。

## 需要 GitHub 才能驗證的事

排程、手動 Run workflow、bot push、Pages artifact 和公開部署都必須 push 到 GitHub 後才可驗證。本機只能驗證抓取 script 和頁面佈局。
