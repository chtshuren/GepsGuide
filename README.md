# 政府電子採購網操作導覽

本專案是一個純 HTML、CSS、圖片與 Markdown 素材組成的靜態網站，用來說明政府電子採購網的操作方式。

網站發布網址：

https://chtshuren.github.io/GepsGuide/

## 目錄說明

```text
source/     原始素材、截圖與說明文件
 target/    實際要發布的靜態網站
```

- `source/`：存放原始截圖與中英文說明素材。
- `target/`：存放可直接由瀏覽器開啟的網站檔案。GitHub Pages 發布的內容就是這個目錄。
- `main`：保存完整專案原始檔案與修改紀錄。
- `gh-pages`：只保存 `target/` 的網站內容，作為 GitHub Pages 的發布分支。

## GitHub Pages 設定

在 GitHub repository 開啟：

`Settings` → `Pages`

設定為：

```text
Source: Deploy from a branch
Branch: gh-pages
Folder: / (root)
```

設定完成後，網站網址為：

```text
https://chtshuren.github.io/GepsGuide/
```

## 第一次設定本地 Git

如果尚未初始化 Git，可在專案根目錄執行：

```powershell
cd D:\work\guide_video
git init
git branch -M main
git config user.name "chtshuren"
git config user.email "shuren@cht.com.tw"
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/chtshuren/GepsGuide.git
git push -u origin main
```

若 GitHub repository 已經存在，直接設定 `origin` 即可：

```powershell
git remote add origin https://github.com/chtshuren/GepsGuide.git
```

## 日常修改與推送流程

### 1. 修改素材或網站

依照需求修改：

- `source/`：新增或修改原始素材。
- `target/`：更新網站頁面、樣式與圖片。

如果修改了 `source/`，請同步將對應內容更新到 `target/`，因為 GitHub Pages 只會發布 `target/` 的內容。

### 2. 檢查變更

```powershell
git status
git diff
```

### 3. Commit 到 main

```powershell
git add .
git commit -m "描述這次修改內容"
git push origin main
```

例如：

```powershell
git add .
git commit -m "Add vendor login guide"
git push origin main
```

### 4. 更新 gh-pages

每次 `target/` 有變更，都要執行：

```powershell
git subtree push --prefix target origin gh-pages
```

這個指令會將 `target/` 的內容放到 `gh-pages` 分支根目錄，GitHub Pages 會從該分支發布網站。

完整日常流程如下：

```powershell
cd D:\work\guide_video
git status
git add .
git commit -m "描述這次修改內容"
git push origin main
git subtree push --prefix target origin gh-pages
```

如果顯示 `Everything up-to-date`，表示該分支已經是最新狀態。

## 檢查發布結果

確認遠端分支：

```powershell
git ls-remote --heads origin main
git ls-remote --heads origin gh-pages
```

查看網站：

```text
https://chtshuren.github.io/GepsGuide/
```

GitHub Pages 更新可能需要幾分鐘。如果瀏覽器仍顯示舊內容，可以重新整理，或使用無痕視窗測試。

## 常見問題

### 網站顯示 404

請確認：

1. GitHub repository 已經存在。
2. `gh-pages` 分支已經推送到 GitHub。
3. `Settings` → `Pages` 的 Branch 設定為 `gh-pages`。
4. Folder 設定為 `/ (root)`。
5. `gh-pages` 分支根目錄內有 `index.html`。

### 網站內容沒有更新

確認是否執行了兩個 push：

```powershell
git push origin main
git subtree push --prefix target origin gh-pages
```

只推送 `main` 不會自動更新 `gh-pages`，因為本專案沒有使用 GitHub Actions。

### GitHub 要求登入

執行 push 時，GitHub 可能要求瀏覽器登入或授權。完成授權後，再重新執行原本的 push 指令即可。

## 注意事項

- 不要將密碼、Token 或其他機密資料放入 repository。
- `target/` 內的檔案會公開出現在 GitHub Pages 網站上。
- 不需要建立 GitHub Actions；本專案採用手動 commit 與手動發布方式。
