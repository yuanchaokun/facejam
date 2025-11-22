# 🚀 Cloudflare Pages 部署完整教程

## ✅ 前提条件
- [x] 已在Cloudflare购买域名
- [x] 所有项目文件准备好

---

## 📋 部署步骤（5分钟完成）

### 第1步：登录Cloudflare
访问：https://dash.cloudflare.com
使用你购买域名的账号登录

### 第2步：创建Pages项目
1. 点击左侧 **"Workers & Pages"**
2. 点击 **"Create application"**
3. 选择 **"Pages"** 标签
4. 点击 **"Upload assets"**

### 第3步：上传文件
1. 项目名称：`facejam`
2. 拖拽整个文件夹到上传区
3. 确保包含：
   - ✅ index.html
   - ✅ assets/ (Kay的贴纸)
   - ✅ libs/ (face-api.min.js)
   - ✅ models/ (AI模型)
   - ✅ _headers (缓存配置)
4. 点击 **"Deploy site"**

### 第4步：绑定域名
1. 部署完成后，点击 **"Custom domains"**
2. 点击 **"Set up a custom domain"**
3. 输入你的域名（如：facejam.cc）
4. Cloudflare自动配置DNS
5. 等待几分钟生效

### 第5步：验证
访问你的域名，测试所有功能！

---

## ⚡ CDN加速说明

### 自动启用的功能：
- ✅ 全球200+节点CDN
- ✅ 自动HTTPS证书
- ✅ 边缘缓存
- ✅ 自动压缩
- ✅ DDoS防护
- ✅ 无限带宽

### 缓存策略（已配置）：
- 静态资源（assets/libs/models）：缓存1年
- HTML文件：缓存5分钟
- 其他文件：缓存1小时

---

## 🔄 更新网站

### 方法1：Web界面
1. Pages项目页面
2. "Create new deployment"
3. 上传新文件

### 方法2：Git自动部署
```bash
# 初始化Git
git init
git add .
git commit -m "Initial commit"

# 连接GitHub
git remote add origin https://github.com/username/FaceJam.git
git push -u origin main

# 以后更新只需：
git add .
git commit -m "更新"
git push
```

在Cloudflare连接GitHub仓库后，每次push自动部署！

---

## 📊 监控和分析

### 查看访问数据：
1. Pages项目页面
2. 点击 **"Analytics"**
3. 查看访问量、带宽等数据

### 查看部署历史：
1. **"Deployments"** 标签
2. 查看所有部署记录
3. 可以回滚到之前的版本

---

## 🎯 性能优化建议

### 1. 启用Rocket Loader（可选）
在域名设置 → Speed → Optimization
- 开启 Auto Minify
- 开启 Brotli

### 2. 配置Page Rules（可选）
为你的域名添加规则：
- Cache Level: Cache Everything
- Browser Cache TTL: 1 year

### 3. 开启HTTP/3
在域名设置 → Network
- 开启 HTTP/3 (with QUIC)
- 开启 0-RTT Connection Resumption

---

## 🔐 安全设置

### SSL/TLS模式：
域名设置 → SSL/TLS
- 设置为 **"Full (strict)"**

### 安全头部（已在_headers配置）：
- X-Content-Type-Options: nosniff
- X-Frame-Options: DENY
- X-XSS-Protection: 1; mode=block

---

## 💡 常见问题

### Q: 部署后图片不显示？
A: 检查assets文件夹是否上传完整

### Q: AI功能不工作？
A: 确保models和libs文件夹都上传了

### Q: 域名访问不了？
A: 等待DNS生效（最多5分钟）

### Q: 如何查看错误？
A: 浏览器按F12，查看Console

### Q: 速度还是慢？
A: 清除浏览器缓存，首次访问会慢一点

---

## 📝 部署清单

- [ ] Cloudflare账号已登录
- [ ] 域名已购买
- [ ] 项目文件已准备
- [ ] Pages项目已创建
- [ ] 文件已上传
- [ ] 域名已绑定
- [ ] DNS已生效
- [ ] 网站可以访问
- [ ] 功能测试通过
- [ ] CDN加速已启用

---

## 🎉 完成！

恭喜！你的FaceJam现在已经：
- ✅ 部署在Cloudflare全球CDN
- ✅ 拥有专业域名
- ✅ 自动HTTPS加密
- ✅ 无限流量免费使用
- ✅ 自动备份和版本控制

**总成本：$0 + 域名费用！**

---

需要帮助？检查：
- Cloudflare文档：https://developers.cloudflare.com/pages/
- 项目状态：https://dash.cloudflare.com/pages

