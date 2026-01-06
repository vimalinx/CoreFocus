# 期末突击 - 政治经济学学习系统

一个为大学生期末考试准备的静态学习网站，包含闪卡学习、核心概念解析和重点文档下载功能。

## 功能特点

- **闪卡学习**：67个高频考点闪卡，支持翻转、随机打乱
- **核心概念**：15个核心概念详细解析，包含定义、特征、公式等
- **重点文档**：完整版重点文档下载
- **付费解锁**：验证码系统，支持微信/支付宝支付
- **响应式设计**：完美适配手机、平板、电脑

## 技术栈

- HTML5 + CSS3 + JavaScript
- Tailwind CSS（通过CDN）
- Alpine.js（轻量级交互框架）
- 纯静态部署，无需后端

## 本地运行

1. 克隆或下载本项目
2. 直接用浏览器打开 `index.html` 即可

## 部署到 GitHub Pages

### 方法一：通过 GitHub 网页界面

1. 创建一个新的 GitHub 仓库
2. 将所有文件上传到仓库
3. 进入仓库的 Settings → Pages
4. 在 Source 下选择 `main` 分支，点击 Save
5. 等待几分钟，GitHub 会生成访问链接

### 方法二：通过命令行

```bash
# 初始化 git 仓库
git init

# 添加所有文件
git add .

# 提交
git commit -m "Initial commit"

# 添加远程仓库（替换为你的仓库地址）
git remote add origin https://github.com/your-username/your-repo.git

# 推送到 GitHub
git branch -M main
git push -u origin main
```

然后在 GitHub 仓库设置中启用 Pages 功能。

## 收费方案

### 免费版
- 前 10 个闪卡
- 前 5 个核心概念
- 预览重点文档

### 完整版（¥9.9/永久）
- 全部 67 个闪卡
- 全部 15 个核心概念
- 重点文档完整版下载
- 思维导图高清版
- 永久免费更新
- 优先客服支持

## 验证码系统

1. 用户在 `unlock.html` 页面选择支付方式
2. 扫描二维码支付 ¥9.9
3. 支付后获得验证码
4. 输入验证码解锁全部内容
5. 解锁状态保存在 localStorage 中

### 生成验证码

在 `js/data.js` 中修改验证码：

```javascript
function unlock(code) {
    if (code === 'YOUR_CODE_HERE') {
        localStorage.setItem('unlocked', 'true');
        return true;
    }
    return false;
}
```

## 文件结构

```
FlashCard/
├── index.html          # 主页
├── flashcards.html     # 闪卡学习页面
├── concepts.html       # 核心概念展示页面
├── unlock.html         # 付费解锁页面
├── js/
│   └── data.js         # 数据文件（闪卡、概念、验证码）
├── assets/             # 静态资源（图片、文档等）
└── README.md           # 说明文档
```

## 自定义内容

### 添加新的闪卡

在 `js/data.js` 中的 `flashcardsData` 数组添加：

```javascript
{ question: "你的问题", answer: "你的答案" }
```

### 添加新的核心概念

在 `js/data.js` 中的 `conceptsData` 数组添加：

```javascript
{
    name: "概念名称",
    definition: "定义",
    chapter: "章节",
    features: "特征",
    formula: "公式",
    significance: "意义"
}
```

## 支付设置

1. 在 `unlock.html` 中替换支付二维码
2. 修改 `js/data.js` 中的验证码
3. 设置支付回调或手动发放验证码

## 注意事项

- 验证码存储在浏览器 localStorage 中，清除缓存会丢失解锁状态
- 建议用户截图保存验证码，以便在其他设备使用
- 静态网站无法实现真正的服务器端验证，仅适用于小规模使用

## 扩展建议

如需更完善的支付系统，可以考虑：
- 使用 Stripe 或支付宝开放平台
- 部署后端服务验证支付状态
- 使用数据库存储用户信息

## 许可证

MIT License