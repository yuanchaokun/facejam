# GitHub + Cloudflare Pages 部署完整教程

## 📋 前置准备

已完成：
- ✅ Git仓库已初始化
- ✅ 所有代码已提交到本地Git
- ✅ Google Analytics代码已集成（需要替换ID）
- ✅ 本地模型文件已下载加速国内访问

待完成：
- ⬜ 创建GitHub仓库
- ⬜ 推送代码到GitHub
- ⬜ 在Cloudflare Pages配置部署
- ⬜ 绑定自定义域名

---

## 第一步：创建GitHub仓库并推送代码

### 方式一：通过GitHub网站创建（推荐）

1. **创建新仓库**
   - 访问：https://github.com/new
   - 仓库名：`facejam` 或 `facejam-app`
   - 描述：`🥰 FaceJam 贴脸酱 - AI表情贴纸生成器`
   - 设置为：**Public**（公开，Cloudflare Pages需要）
   - ⚠️ **不要**勾选 "Add a README file"
   - ⚠️ **不要**勾选 "Add .gitignore"
   - ⚠️ **不要**选择 "Choose a license"
   - 点击 "Create repository"

2. **连接远程仓库并推送**
   
   创建完成后，GitHub会显示命令，复制类似这样的命令在终端执行：
   
   ```bash
   cd "/Users/yuanchaokun/Documents/bd个人Anki项目/贴脸酱 FaceJam"
   
   # 添加远程仓库（替换为你的GitHub用户名）
   git remote add origin https://github.com/你的用户名/facejam.git
   
   # 推送代码
   git push -u origin main
   ```
   
   如果推送时需要输入凭据：
   - 用户名：你的GitHub用户名
   - 密码：需要使用 Personal Access Token（不是GitHub密码）
   
   **如何创建Personal Access Token：**
   1. 访问：https://github.com/settings/tokens
   2. 点击 "Generate new token" → "Generate new token (classic)"
   3. Note: `FaceJam Deploy`
   4. Expiration: `No expiration` 或选择时长
   5. 勾选权限：`repo` (所有子选项)
   6. 点击底部 "Generate token"
   7. **立即复制token**（只显示一次！）
   8. 将token作为密码使用

### 方式二：使用GitHub CLI（如果已配置）

```bash
cd "/Users/yuanchaokun/Documents/bd个人Anki项目/贴脸酱 FaceJam"

# 使用gh CLI创建仓库并推送
gh repo create facejam --public --source=. --push
```

---

## 第二步：配置Google Analytics

1. **获取GA测量ID**
   - 访问：https://analytics.google.com/
   - 创建新的媒体资源
   - 获取类似 `G-XXXXXXXXXX` 的ID

2. **替换代码中的ID**
   
   在 `index.html` 中搜索 `G-XXXXXXXXXX`，替换为你的实际ID（共2处）：
   
   ```html
   <script async src="https://www.googletagmanager.com/gtag/js?id=G-你的实际ID"></script>
   <script>
       window.dataLayer = window.dataLayer || [];
       function gtag(){dataLayer.push(arguments);}
       gtag('js', new Date());
       gtag('config', 'G-你的实际ID', {
           'page_title': 'FaceJam 贴脸酱',
           'page_location': window.location.href
       });
   </script>
   ```

3. **提交更新**
   ```bash
   git add index.html
   git commit -m "🔧 配置Google Analytics ID"
   git push
   ```

详细说明请查看：`Google_Analytics配置说明.md`

---

## 第三步：在Cloudflare Pages部署

### 1. 登录Cloudflare

访问：https://dash.cloudflare.com/

### 2. 进入Pages

左侧菜单选择 "Workers & Pages" → 点击 "Create application" → 选择 "Pages" → "Connect to Git"

### 3. 连接GitHub

1. 点击 "Connect GitHub"
2. 授权Cloudflare访问你的GitHub账户
3. 选择刚才创建的仓库（例如：`facejam`）
4. 点击 "Begin setup"

### 4. 配置构建设置

**项目名称：** `facejam` （这将成为默认域名：facejam.pages.dev）

**生产分支：** `main`

**构建设置：**
- Framework preset: `None` （选择"无"）
- Build command: **留空**
- Build output directory: `/` （或留空）
- Root directory: `/` （或留空）

⚠️ **重要**：因为这是纯静态HTML项目，不需要构建命令！

**环境变量：** 无需配置

点击 **"Save and Deploy"**

### 5. 等待部署完成

- 首次部署约需 1-3 分钟
- 部署成功后会显示绿色 ✅
- 获得临时域名：`https://facejam.pages.dev`

---

## 第四步：绑定自定义域名

### 1. 在Cloudflare Pages中添加域名

1. 进入你的项目：Workers & Pages → 选择 `facejam`
2. 点击 "Custom domains" 标签
3. 点击 "Set up a custom domain"
4. 输入你的域名：`facejam.cc` 或 `www.facejam.cc`
5. 点击 "Continue"

### 2. 配置DNS

如果你的域名已经在Cloudflare托管：
- Cloudflare会自动添加所需的DNS记录
- 通常几分钟内生效

如果域名不在Cloudflare：
1. 进入你的域名注册商
2. 将域名的NS记录指向Cloudflare的NS服务器
3. 或手动添加CNAME记录指向 `facejam.pages.dev`

### 3. 启用HTTPS

- Cloudflare会自动提供SSL证书
- 通常5-15分钟内完成
- 强制HTTPS已默认启用

---

## 第五步：优化CDN和缓存

你的项目已包含 `_headers` 文件，Cloudflare会自动应用这些优化：

```
/*
  Cache-Control: public, max-age=3600
  X-Frame-Options: SAMEORIGIN
  X-Content-Type-Options: nosniff
  Referrer-Policy: strict-origin-when-cross-origin

/libs/*
  Cache-Control: public, max-age=31536000, immutable

/models/*
  Cache-Control: public, max-age=31536000, immutable

/assets/*
  Cache-Control: public, max-age=31536000, immutable
```

这将确保：
- HTML 缓存 1 小时
- 静态资源（模型、库、图片）缓存 1 年
- 安全头部自动应用

---

## 🔄 后续更新流程

当你需要修改代码时：

### 1. 本地修改代码

```bash
# 1. 修改文件（如 index.html）

# 2. 查看修改
git status

# 3. 添加修改
git add .

# 4. 提交
git commit -m "✨ 描述你的修改"

# 5. 推送到GitHub
git push
```

### 2. 自动部署

- Cloudflare Pages会自动检测到GitHub推送
- 自动触发新的部署
- 约1-2分钟后更新生效
- 你会收到邮件通知部署状态

### 3. 查看部署历史

在Cloudflare Pages项目页面：
- "Deployments" 标签可查看所有部署记录
- 可以回滚到任何历史版本
- 可以查看每次部署的预览链接

---

## 📊 查看统计数据

### Google Analytics

1. 访问：https://analytics.google.com/
2. 选择 FaceJam 媒体资源
3. 查看实时数据和报告

**可查看的数据：**
- 实时在线用户数
- 每日/每周/每月访问量
- 用户来源（直接、搜索、社交媒体等）
- 用户地理位置
- 设备类型（手机/电脑/平板）
- 自定义事件：
  - 上传图片次数
  - 人脸检测成功率
  - 下载次数
  - 激活去水印次数
  - 最受欢迎的标签页
  - 多选模式使用率

### Cloudflare Analytics

在Cloudflare Pages项目中：
1. 点击 "Analytics" 标签
2. 查看：
   - 请求数量
   - 带宽使用
   - 地理分布
   - 响应时间
   - 错误率

---

## 🐛 常见问题

### Q1: 推送到GitHub时要求输入密码，但密码不对

**A:** GitHub不再支持密码认证，需要使用Personal Access Token：
1. 创建Token：https://github.com/settings/tokens
2. 使用Token作为密码

### Q2: Cloudflare Pages部署失败

**A:** 检查：
1. GitHub仓库是否设置为Public
2. Build command是否留空
3. Build output directory是否为 `/`

### Q3: 网站显示404或白屏

**A:** 检查：
1. 确认 `index.html` 在仓库根目录
2. 清除浏览器缓存
3. 在Cloudflare中查看部署日志

### Q4: Google Analytics没有数据

**A:** 检查：
1. 是否替换了正确的GA ID
2. 浏览器是否启用了广告拦截
3. 使用无痕模式测试
4. 查看浏览器控制台是否有错误

### Q5: 国内访问很慢

**A:** 已优化：
1. ✅ Face-api.js模型已本地化（models/目录）
2. ✅ Cloudflare CDN全球加速
3. ✅ 静态资源缓存策略
4. 如果仍慢，可以考虑：
   - 使用Cloudflare的中国网络（需要ICP备案）
   - 或使用国内CDN服务（七牛云、阿里云）

---

## 📦 项目文件结构

```
facejam/
├── index.html                    # 主页面
├── .gitignore                    # Git忽略文件
├── _headers                      # Cloudflare缓存配置
├── assets/                       # Kay的原创贴纸
│   ├── kay_happy.png
│   ├── kay_smug.png
│   ├── kay_sweat.png
│   └── kay_elephant.png
├── libs/                         # 本地库文件
│   └── face-api.min.js
├── models/                       # AI模型文件（本地加速）
│   ├── face_expression_model-*
│   └── ssd_mobilenetv1_model-*
├── 部署说明.md
├── CDN说明.md
├── Cloudflare部署教程.md        # 本文件
├── Google_Analytics配置说明.md
└── Kay专区说明.md
```

---

## 🎉 完成！

按照以上步骤，你的FaceJam应该已经成功部署！

**访问地址：**
- 临时域名：https://facejam.pages.dev
- 自定义域名：https://facejam.cc（配置后）

**下一步：**
1. 测试所有功能是否正常
2. 配置Google Analytics查看数据
3. 分享给用户使用
4. 根据统计数据优化功能

有任何问题都可以查看对应的说明文档！

