# GitHub Actions 工作流说明

## 工作流文件

- `hugo.yml` - 主要工作流，使用最新的 GitHub Pages Actions（推荐）
- `gp.yml` - 备用工作流
- `gh-pages.yml` - 部署到 gh-pages 分支的工作流

## 使用 hugo.yml（推荐）

这个工作流会自动：
1. 构建 Hugo 站点
2. 部署到 GitHub Pages

### 前提条件

1. **仓库设置**
   - 进入 Settings → Pages
   - Source 选择 **"GitHub Actions"**（重要！）
   - 不要选择分支作为源

2. **权限设置**
   - 进入 Settings → Actions → General
   - Workflow permissions 选择 **"Read and write permissions"**
   - 勾选 "Allow GitHub Actions to create and approve pull requests"

3. **触发构建**
   - 推送代码到 `main` 或 `master` 分支
   - 或手动在 Actions 标签页运行工作流

## 如果仍然 404

1. 检查 Actions 标签页，看是否有失败的构建
2. 查看构建日志，确认是否有错误
3. 确认仓库名称是 `bryanleungds.github.io`（小写）
4. 等待 1-2 分钟让 GitHub Pages 更新
