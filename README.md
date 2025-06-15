# LibreTV - 免費線上影片搜尋與觀看平台

<div align="center">
  <img src="image/logo.png" alt="LibreTV Logo" width="120">
  <br>
  <p><strong>自由觀影，享受精彩</strong></p>
</div>

## 📺 專案簡介

LibreTV 是一個輕量級、免費的線上影片搜尋與觀看平台，提供來自多個影片來源的內容搜尋與播放服務。無需註冊，即開即用，支援多種裝置存取。專案結合了前端技術和後端代理功能，可部署在支援服務端功能的各類網站託管服務上。

本項目基於 [bestK/tv](https://github.com/bestK/tv) 進行重構與增強。

<details>
  <summary>點擊查看專案截圖</summary>
  <img src="https://github.com/user-attachments/assets/df485345-e83b-4564-adf7-0680be92d3c7" alt="專案截圖" style="max-width:600px">
</details>

## 🥇 感謝贊助

- **[YXVM](https://yxvm.com)**  
- **[ZMTO/VTEXS](https://zmto.com)**

## 🚀 快速部署

選擇以下任一平台，點選一鍵部署按鈕，即可快速建立自己的 LibreTV 實例：

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https%3A%2F%2Fgithub.com%2FLibreSpark%2FLibreTV)  
[![Deploy to Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/LibreSpark/LibreTV)  
[![Deploy to Render](https://render.com/images/deploy-to-render-button.svg)](https://render.com/deploy?repo=https://github.com/LibreSpark/LibreTV) 

## ⚠️ 安全與隱私提醒

### 🔒 強烈建議設定密碼保護

為了您的安全和避免潛在的法律風險，我們**強烈建議**在部署時設定密碼保護：

- **避免公開訪問**：不設定密碼的實例任何人都可以訪問，可能被惡意利用
- **防範版權風險**：公開的影片搜尋服務可能面臨版權方的投訴舉報
- **保護個人隱私**：設定密碼可以限制存取範圍，保護您的使用記錄

### 📝 部署建議

1. **設定環境變數 `PASSWORD`**：為您的實例設定一個強密碼
2. **僅供個人使用**：請勿將您的實例連結公開分享或傳播
3. **遵守當地法律**：請確保您的使用行為符合當地法律法規

### 🚨 重要聲明

- 本項目僅供學習和個人使用
- 請勿將部署的執行個體用於商業用途或公開服務
- 如因公開分享而導致的任何法律問題，用戶需自行承擔責任
- 專案開發者不對使用者的使用行為承擔任何法律責任

## ⚠️ 請勿使用 Pull Bot 自動同步

Pull Bot 會重複觸發無效的 PR 和垃圾郵件，嚴重干擾專案維護。作者可能會直接拉黑所有 Pull Bot 自動發起的同步請求的倉庫所有者。

**推薦做法：**

建議在 fork 的倉庫中啟用本倉庫自帶的 GitHub Actions 自動同步功能（請參閱 `.github/workflows/sync.yml`）。 

如需手動同步主倉庫更新，也可以使用 GitHub 官方的 [Sync fork](https://docs.github.com/cn/github/collaborating-with-issues-and-pull-requests/syncing-a-fork) 功能。


## 📋 詳細部署指南

### Cloudflare Pages

1. Fork 或複製本倉庫到您的 GitHub 帳戶
2. 登錄 [Cloudflare Dashboard](https://dash.cloudflare.com/)，進入 Pages 服務
3. 點擊"建立專案"，連接您的 GitHub 倉庫
4. 使用以下設定：
   - 建置命令：留空（無需建置）
   - 輸出目錄：留空（預設為根目錄）
5. **⚠️ 重要：在"設定" > "環境變量"中添加 `PASSWORD` 變量**
6. **可選：在"Settings" > "Environment Variables"中添加 `ADMINPASSWORD` 變量**
7. 點擊"儲存並部署"

### Vercel

1. Fork 或複製本倉庫到您的 GitHub/GitLab 帳戶
2. 登錄 [Vercel](https://vercel.com/)，點擊"New Project"
3. 導入您的倉庫，使用預設設定
4. **⚠️ 重要：在"Settings" > "Environment Variables"中添加 `PASSWORD` 變量**
5. **可選：在"Settings" > "Environment Variables"中添加 `ADMINPASSWORD` 變量**
6. 点击"Deploy"
7. 可选：在"Settings" > "Environment Variables"中配置密码保护和设置按钮密码保护

### Docker
```
docker run -d \
  --name libretv \
  --restart unless-stopped \
  -p 8899:8080 \
  -e PASSWORD=your_password \
  -e ADMINPASSWORD=your_adminpassword \
  bestzwei/libretv:latest
```

### Docker Compose

`docker-compose.yml` 文件：

```yaml
services:
  libretv:
    image: bestzwei/libretv:latest
    container_name: libretv
    ports:
      - "8899:8080" # 將內部 8080 端口映射到主機的 8899 端口
    environment:
      - PASSWORD=${PASSWORD:-your_password} # 可將 your_password 修改為你想要的密碼，預設為 your_password
      - ADMINPASSWORD=${PASSWORD:-your_adminpassword} # 可將 your_adminpassword 修改為你想要的密碼，預設為 your_adminpassword
    restart: unless-stopped
```
啟動 LibreTV：

```bash
docker compose up -d
```
造訪 `http://localhost:8899` 即可使用。

### 本地開發環境

專案包含後端代理功能，需要支援伺服器端功能的環境：

```bash
# 首先，透過複製範例來設定 .env 檔案（可選）
cp .env.example .env

# 安裝依賴
npm install

# 啟動開發伺服器
npm run dev
```

造訪 `http://localhost:8080` 即可使用（連接埠可在.env檔案中透過PORT變數修改）。

> ⚠️ 注意：使用簡單靜態伺服器（如 `python -m http.server` 或 `npx http-server`）時，視訊代理功能將不可用，影片無法正常播放。完整功能測試請使用 Node.js 開發伺服器。
> 
## 🔧 自訂配置

### 密碼保護

若要為您的 LibreTV 執行個體新增密碼保護，可以在部署平台上設定環境變數：

**環境變數名**: `PASSWORD` 
**值**: 您想設定的密碼

**環境變數名**: `ADMINPASSWORD` 
**值**: 您想設定的密碼

各平台設定方式：

- **Cloudflare Pages**: Dashboard > 您的專案 > 設定 > 環境變數
- **Vercel**: Dashboard > 您的專案 > Settings > Environment Variables
- **Netlify**: Dashboard > 您的專案 > Site settings > Build & deploy > Environment
- **Docker**: 修改 `docker run` 中 `your_password` 為你的密碼
- **Docker Compose**: 修改 `docker-compose.yml` 中的 `your_password` 為你的密碼
- **本地開發**: SET PASSWORD=your_password

### API相容性

LibreTV 支援標準的蘋果 CMS V10 API 格式。新增自訂 API 時需遵循以下格式：
- 搜尋介面: `https://example.com/api.php/provide/vod/?ac=videolist&wd=關鍵字`
- 詳情介面: `https://example.com/api.php/provide/vod/?ac=detail&ids=視訊ID`

**新增 CMS 來源**:
1. 在設定面板中選擇"自訂介面"
2. 接口地址: `https://example.com/api.php/provide/vod`

## ⌨️ 鍵盤快速鍵

播放器支援以下鍵盤快捷鍵：

- **空格键**: 播放/暫停
- **左右箭头**: 快退/快轉
- **上下箭头**: 音量增加/減小
- **M 键**: 靜音/取消靜音
- **F 键**: 全螢幕/退出全螢幕
- **Esc 键**: 退出全螢幕

## 🛠️ 技術堆疊

- HTML5 + CSS3 + JavaScript (ES6+)
- Tailwind CSS
- HLS.js 用于 HLS 架構
- DPlayer 影片播放器核心
- Cloudflare/Vercel/Netlify Serverless Functions
- 服務端 HLS 代理和處理技術
- localStorage 本地儲存

## ⚠️ 免責聲明

LibreTV 僅作為影片搜尋工具，不儲存、上傳或散佈任何影片內容。所有影片均來自第三方 API 介面提供的搜尋結果。如有侵權內容，請聯絡對應的內容提供者。

本專案開發者不對使用本專案產生的任何後果負責。使用本項目時，您必須遵守當地的法律法規。

## 💝 支援專案

如果您想支持本專案，可以考慮進行捐款：

[![捐赠](https://img.shields.io/badge/%E6%84%9B%E5%BF%83%E6%8D%90%E8%B4%88-%E5%8F%B0%E7%81%A3%E4%B8%96%E7%95%8C%E5%B1%95%E6%9C%9B%E6%9C%83worldvision-red)](https://www.worldvision.org.tw/)
