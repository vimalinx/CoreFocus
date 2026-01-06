# GitHub Pages 部署指南

## 快速部署步骤

### 1. 创建 GitHub 仓库

1. 访问 [GitHub](https://github.com) 并登录
2. 点击右上角的 "+" 号，选择 "New repository"
3. 仓库名称填写：`final-exam-cram`（或其他你喜欢的名字）
4. 选择 Public（公开）或 Private（私有）
5. 勾选 "Add a README file"
6. 点击 "Create repository"

### 2. 上传文件

#### 方法 A：通过网页界面上传（推荐新手）

1. 在新创建的仓库页面，点击 "Add file" → "Upload files"
2. 将以下文件拖拽到上传区域：
   - `index.html`
   - `flashcards.html`
   - `concepts.html`
   - `unlock.html`
   - `js/data.js`
   - `README.md`
   - `.gitignore`
3. 在 "Commit changes" 框中输入：`Initial commit`
4. 点击 "Commit changes"

#### 方法 B：通过命令行上传（推荐有经验的用户）

```bash
# 进入项目目录
cd e:\Programs\FlashCard

# 初始化 git 仓库
git init

# 添加所有文件
git add .

# 提交
git commit -m "Initial commit"

# 添加远程仓库（替换为你的仓库地址）
git remote add origin https://github.com/your-username/final-exam-cram.git

# 推送到 GitHub
git branch -M main
git push -u origin main
```

### 3. 启用 GitHub Pages

1. 在仓库页面，点击 "Settings" 标签
2. 在左侧菜单中找到 "Pages"
3. 在 "Source" 下：
   - Branch 选择：`main`
   - Folder 选择：`/ (root)`
4. 点击 "Save"

### 4. 等待部署

- 等待 1-3 分钟，GitHub 会自动构建和部署
- 刷新页面，会看到类似这样的链接：
  - `https://your-username.github.io/final-exam-cram/`

### 5. 访问网站

点击显示的链接，即可访问你的网站！

## 自定义域名（可选）

如果你想使用自己的域名：

1. 在仓库的 Settings → Pages 中
2. 在 "Custom domain" 中输入你的域名（如 `exam.yourdomain.com`）
3. 在你的域名 DNS 设置中添加 CNAME 记录：
   - 主机记录：`exam`
   - 记录值：`your-username.github.io`
4. 等待 DNS 生效（通常需要几分钟到几小时）

## 更新网站

当你需要更新网站内容时：

### 方法 A：通过网页界面

1. 在仓库页面点击要修改的文件
2. 点击右上角的铅笔图标
3. 修改内容
4. 在底部输入提交信息
5. 点击 "Commit changes"

### 方法 B：通过命令行

```bash
# 修改文件后
git add .
git commit -m "Update content"
git push
```

GitHub Pages 会自动检测到更改并重新部署。

## 常见问题

### Q: 部署后网站显示 404 错误
A: 检查文件名是否正确，特别是 `index.html` 是否存在

### Q: 更改后没有立即生效
A: GitHub Pages 部署需要 1-3 分钟，请耐心等待

### Q: 如何查看部署状态
A: 在仓库的 "Actions" 标签中可以查看部署日志

### Q: 可以使用私有仓库吗
A: 可以，但私有仓库的 GitHub Pages 只能通过登录 GitHub 的用户访问

### Q: 如何添加自定义域名
A: 参考上面的"自定义域名"部分

## 性能优化建议

1. **压缩图片**：使用工具如 TinyPNG 压缩图片
2. **使用 CDN**：将大文件托管到 CDN
3. **启用 Gzip**：GitHub Pages 默认已启用
4. **缓存策略**：在 HTML 中添加缓存头

## 安全建议

1. 不要在代码中硬编码敏感信息
2. 定期更新依赖（如果有）
3. 使用 HTTPS（GitHub Pages 默认提供）
4. 定期备份代码

## 下一步

部署成功后，你可以：

1. 分享链接给同学
2. 在社交媒体上推广
3. 根据用户反馈优化内容
4. 添加更多学科的内容

## 需要帮助？

如果遇到问题，可以：
- 查看 [GitHub Pages 官方文档](https://docs.github.com/en/pages)
- 在 GitHub 社区搜索类似问题
- 联系 GitHub 支持