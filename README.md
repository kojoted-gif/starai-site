# starai.tw 網站上線包

星算 Star Counter 官方網站（純靜態網站，中英雙語）。

## 內容
| 檔案 | 用途 |
|---|---|
| `index.html` | 網站本體（首頁、`#bare-metal` 裸機租賃、`#campuses` 園區） |
| `privacy.html` | 隱私權政策與個資蒐集告知（上線前請法務確認） |
| `404.html` | 找不到頁面 |
| `insights/` | 兩篇工程觀點文章 |
| `docs/` | 規格書 PDF（中、英） |
| `img/` | 9 張 3D 渲染圖（WebP 800/1600/2400 + JPEG 備援）、社群分享圖 `og.jpg`、圖示 |
| `favicon.svg` / `favicon-32.png` / `apple-touch-icon.png` | 網站圖示 |
| `robots.txt` / `sitemap.xml` | 搜尋引擎 |
| `site.webmanifest` | 手機加入主畫面用的圖示與名稱 |
| `.nojekyll` | 讓 GitHub Pages 原樣發佈所有檔案 |
| `CNAME` | GitHub Pages 自訂網域用 |
| `_headers` | Cloudflare Pages / Netlify 的安全與快取標頭 |

## 上線前要完成的三件事
1. 建立信箱 `sales@starai.tw`（GoDaddy 郵件、Google Workspace 或 Microsoft 365 皆可）。
2. 表單後端：到 Formspree 或 Web3Forms 建立表單，把網址填進 `index.html` 的 `const FORM_ENDPOINT = '';`。
   未填時，送出按鈕會改開訪客的郵件程式寄到 sales@starai.tw，仍可運作。
3. `privacy.html` 補上公司登記名稱、統一編號與地址，並請法務確認。

## 部署方式（擇一）

### A. GitHub Pages（DNS 留在 GoDaddy）
1. 建立 GitHub repository，把本資料夾全部內容放到根目錄。
2. Settings → Pages → Source 選 `main` 分支根目錄；Custom domain 填 `starai.tw`，勾選 Enforce HTTPS。
3. GoDaddy DNS 設定：
   | 類型 | 名稱 | 值 |
   |---|---|---|
   | A | @ | 185.199.108.153 |
   | A | @ | 185.199.109.153 |
   | A | @ | 185.199.110.153 |
   | A | @ | 185.199.111.153 |
   | CNAME | www | `<GitHub 帳號>.github.io` |
   刪除 GoDaddy 預設指向停放頁的 @ 記錄（Parked）。

### B. Netlify（DNS 留在 GoDaddy）
1. Netlify → Add new site → Deploy manually，把資料夾拖進去。
2. Domain settings 加入 `starai.tw`。
3. GoDaddy DNS：`A @ 75.2.60.5`、`CNAME www <站名>.netlify.app`。

### C. Cloudflare Pages（需把 DNS 移到 Cloudflare）
1. Cloudflare 新增網站 `starai.tw`，到 GoDaddy 把 Nameservers 改成 Cloudflare 提供的兩組。
2. Workers & Pages → Create → Pages → Upload assets，上傳本資料夾。
3. Custom domains 加入 `starai.tw` 與 `www.starai.tw`。

DNS 生效通常數分鐘到數小時；HTTPS 憑證由主機商自動簽發。

## 流量分析與轉換追蹤
網站已內建事件追蹤，只要在 `index.html` 的 `<head>` 加入任一套分析工具即可自動收到：
- Plausible：`<script defer data-domain="starai.tw" src="https://plausible.io/js/script.js"></script>`
- 或 Google Analytics 4 / Google Tag Manager 的官方程式碼

追蹤的事件：`lead_submit`（送出詢價）、`cta_click`、`calculator_used`、`download_spec_zh` / `download_spec_en`、`read_cooling` / `read_dr4n3`、`gallery_open`、`language_switch`。

## 文件與文章
- `docs/`：第一期規格書 PDF（中文、英文）
- `insights/`：工程觀點文章（溫水液冷、DR4N3），已列入 sitemap

## 語言
- 第一次造訪會依瀏覽器語言自動選擇中文或英文，之後記住訪客的選擇。
- 分享英文版請用 `https://starai.tw/?lang=en`。

## 上線後
- Google Search Console 驗證 `starai.tw` 並提交 `https://starai.tw/sitemap.xml`。
- 用 https://www.opengraph.xyz 檢查分享預覽圖。
