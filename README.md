# yunfeng-booth

雲峰展位（Yunfeng Booth）專案。目前以靜態頁面為基礎，透過 **GitHub Actions** 在推送到 `main` 時自動部署到 GitHub Pages。

## 線上預覽

啟用 Pages 並完成第一次成功 workflow 後：

https://prefcoai-hue.github.io/yunfeng-booth/

## 自動化流程

| Workflow | 觸發 | 作用 |
| --- | --- | --- |
| `CI` | PR、push | 檢查必要檔案與頁面內容 |
| `Deploy GitHub Pages` | `main` push、手動 | 發布靜態站 |
| `Build & Push Docker` | tag `v*`、手動 | 建置映像並推到 GHCR（可選） |

### 第一次啟用 GitHub Pages

1. 打開 repo → **Settings → Pages**
2. Source 選 **GitHub Actions**
3. 推送 `main`，或到 **Actions** 手動跑 `Deploy GitHub Pages`

### 之後怎麼發布

```bash
git add .
git commit -m "update booth"
git push origin main
```

Actions 會自動建置並上線。也可在 Actions 頁面按 **Run workflow**。

## 部署到自己的伺服器（可選）

若要 SSH + Docker 部署，在 repo **Settings → Secrets and variables → Actions** 新增：

- `SSH_HOST`
- `SSH_USER`
- `SSH_PRIVATE_KEY`
- `SSH_PORT`（可選，預設 22）

然後把 `.github/workflows/deploy-docker.yml` 裡註解掉的 `deploy` job 打開。

## 本機預覽

直接開 `index.html`，或：

```bash
python3 -m http.server 8080
```

瀏覽器開 http://localhost:8080
