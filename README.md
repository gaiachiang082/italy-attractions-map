# 義大利景點互動地圖 · Railway 部署

## 資料夾內容

- `index.html` — 主頁（由 `italy_napoli_firenze_attrazioni.html` 複製）
- `Staticfile` — 告訴 Railway 以靜態網站方式托管（Caddy）

---

## 方法一：GitHub + Railway 網頁（建議）

### 1. 推到 GitHub

在 PowerShell 中：

```powershell
cd C:\Users\user\Desktop\asset\italy-attractions-railway
git init
git add index.html Staticfile .gitignore README.md
git commit -m "Add Italy attractions map for Railway"
```

到 [https://github.com/new](https://github.com/new) 建立新 repo（例如 `italy-attractions-map`），然後：

```powershell
git remote add origin https://github.com/你的帳號/italy-attractions-map.git
git branch -M main
git push -u origin main
```

### 2. 在 Railway 建立專案

1. 登入 [https://railway.com](https://railway.com)
2. **New Project** → **Deploy from GitHub repo**
3. 選剛才的 repository
4. Railway 會自動偵測為靜態站（根目錄有 `index.html`）

### 3. 產生公開網址

1. 點進該 **Service**
2. 分頁 **Settings** → **Networking** → **Generate Domain**
3. 會得到類似：`https://italy-attractions-map-production-xxxx.up.railway.app`

把這個連結傳給客戶即可在外網開啟。

### 4. 之後更新網站

改完 `italy_napoli_firenze_attrazioni.html` 後，複製覆蓋本資料夾的 `index.html`，再：

```powershell
git add index.html
git commit -m "Update map"
git push
```

Railway 會自動重新部署（約 1～2 分鐘）。

---

## 方法二：Railway CLI（不用 GitHub）

### 1. 安裝 CLI

```powershell
npm install -g @railway/cli
railway login
```

### 2. 部署

```powershell
cd C:\Users\user\Desktop\asset\italy-attractions-railway
railway init
railway up
railway domain
```

`railway domain` 會產生公開 URL。

---

## 常見問題

| 問題 | 處理 |
|------|------|
| 打開網址是 404 | 確認 repo 根目錄有 `index.html`，且 **不要** 自訂 Start Command（讓 Railpack 用 Caddy） |
| 地圖有、照片沒有 | 需能連線 `commons.wikimedia.org`；Railway 上一般沒問題 |
| 想用自己的網域 | Railway → Settings → Networking → Custom Domain |

---

## 參考連結

- [Railway 文件](https://docs.railway.com/)
- [Railpack 靜態站](https://railpack.com/languages/staticfile/)
- [Railway 產生網域](https://docs.railway.com/guides/public-networking)
