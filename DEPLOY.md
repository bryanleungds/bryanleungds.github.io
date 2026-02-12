# 部署指南

## 解决 404 错误的步骤

如果遇到 404 错误，请按以下步骤操作：

### 方法 1：使用 GitHub Actions 自动部署（推荐）

1. **确保仓库名称正确**
   - 仓库名必须是：`bryanleungds.github.io`（注意是小写）
   - 如果仓库名不同，请修改 `config.yml` 中的 `baseURL`

2. **配置 GitHub Pages 设置**
   - 进入 GitHub 仓库
   - 点击 **Settings** → **Pages**
   - 在 **Source** 部分，选择 **GitHub Actions**（不是分支）
   - 保存设置

3. **触发构建**
   - 推送代码到 `main` 或 `master` 分支
   - 或者进入 **Actions** 标签页，手动运行工作流

4. **等待部署完成**
   - 在 **Actions** 标签页查看构建状态
   - 部署成功后，等待 1-2 分钟
   - 访问 `https://bryanleungds.github.io/`

### 方法 2：手动部署到 gh-pages 分支

如果 GitHub Actions 不工作，可以手动部署：

```bash
# 1. 构建站点
hugo --minify --baseURL https://bryanleungds.github.io/

# 2. 进入 public 目录
cd public

# 3. 初始化 git（如果还没有）
git init
git add .
git commit -m "Deploy site"

# 4. 添加远程仓库并推送到 gh-pages 分支
git remote add origin https://github.com/bryanleungds/bryanleungds.github.io.git
git branch -M gh-pages
git push -u origin gh-pages --force
```

然后在 GitHub Pages 设置中选择 `gh-pages` 分支作为源。

### 方法 3：部署到根目录（最简单但需要手动）

```bash
# 1. 构建站点
hugo --minify --baseURL https://bryanleungds.github.io/

# 2. 将 public 目录的内容复制到根目录
# Windows PowerShell:
Copy-Item -Path public\* -Destination . -Recurse -Force

# 3. 提交并推送
git add .
git commit -m "Deploy site to root"
git push origin main
```

然后在 GitHub Pages 设置中选择根目录 `/` 作为源。

## 常见问题

### 1. 404 错误
- 检查 `config.yml` 中的 `baseURL` 是否正确
- 确保仓库名称与 `baseURL` 匹配（大小写敏感）
- 检查 GitHub Pages 设置中的源是否正确

### 2. 样式丢失
- 确保 `baseURL` 以 `/` 结尾
- 检查主题子模块是否正确初始化：`git submodule update --init --recursive`

### 3. GitHub Actions 失败
- 检查 `.github/workflows/` 中的工作流文件是否存在
- 查看 Actions 标签页中的错误信息
- 确保有 `pages: write` 权限（在仓库 Settings → Actions → General → Workflow permissions）

## 验证部署

部署成功后，你应该能看到：
- 首页显示欢迎文章
- 导航菜单正常工作
- 暗黑/明亮模式切换正常
- 所有链接都能正常访问
