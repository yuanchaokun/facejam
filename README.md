# 🥰 FaceJam 贴脸酱

> AI驱动的表情贴纸生成器 | 让照片更有趣

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![JavaScript](https://img.shields.io/badge/JavaScript-ES6+-yellow.svg)](https://www.javascript.com/)
[![Face-api.js](https://img.shields.io/badge/Face--api.js-AI-blue.svg)](https://github.com/justadudewhohacks/face-api.js)

## ✨ 特性

- 🤖 **AI人脸识别** - 自动检测照片中的所有人脸
- 😊 **智能表情匹配** - 根据表情自动选择合适的emoji
- 🎨 **多种贴纸** - 表情、动物、物品、原创插画
- ✂️ **智能去底** - 自定义贴纸自动移除背景
- 🎯 **自选模式** - 手动选择多个emoji批量应用
- 📱 **响应式设计** - 完美适配手机和电脑
- 🌐 **双语支持** - 中文/English
- 🔒 **隐私安全** - 所有处理在本地完成，图片不上传
- 💾 **本地存储** - 自定义贴纸自动保存到浏览器

## 🎨 特色专区

### Kay的原创贴纸
由插画师 [@Kay](https://www.xiaohongshu.com/user/profile/53171ac1b4c4d6226fdcf19a) 创作的可爱贴纸：
- 开心团子 🥟
- 傲娇团子 😤
- 流汗鸭 🦆💦
- 大象 🐘

## 🚀 在线体验

访问：[FaceJam.cc](https://facejam.pages.dev) 

## 🛠️ 技术栈

- **前端框架**: 纯JavaScript (Vanilla JS)
- **UI框架**: Tailwind CSS
- **AI引擎**: Face-api.js (TensorFlow.js)
- **字体**: Fredoka (Google Fonts)
- **部署**: Cloudflare Pages
- **分析**: Google Analytics

## 📦 本地运行

```bash
# 克隆项目
git clone https://github.com/yuanchaokun/facejam.git

# 进入目录
cd facejam

# 使用任何HTTP服务器运行
# 方式1: Python
python -m http.server 8000

# 方式2: Node.js
npx serve

# 方式3: 直接打开
open index.html
```

访问：`http://localhost:8000`

## 📖 使用方法

1. 📸 **上传照片** - 点击上传按钮选择照片
2. 🤖 **AI识别** - 自动检测人脸和表情
3. 🎨 **选择贴纸** - 点击emoji或切换到其他标签
4. 🔄 **再贴一次** - 重新随机生成贴纸
5. ✨ **自选模式** - 打开多选，手动选择多个emoji批量应用
6. 💾 **下载保存** - 点击下载按钮保存图片

## 🎯 高级功能

- **智能去底**: 上传自定义贴纸时自动移除背景
- **自定义贴纸**: 支持上传URL或本地图片
- **自动保存**: 自定义贴纸自动保存到浏览器
- **去水印**: 使用激活码移除水印

## 🌍 部署

### Cloudflare Pages (推荐)

1. Fork 本仓库
2. 访问 [Cloudflare Pages](https://pages.cloudflare.com/)
3. 连接GitHub仓库
4. 构建配置：
   - Framework preset: `None`
   - Build command: 留空
   - Build output directory: `/`
5. 部署完成！

### Vercel / Netlify

同样支持一键部署，配置方式类似。

## 📊 性能优化

- ✅ 本地化AI模型文件 (加速国内访问)
- ✅ Cloudflare CDN全球加速
- ✅ 静态资源永久缓存
- ✅ 渐进式加载
- ✅ 响应式图片处理

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

## 📄 开源协议

[MIT License](LICENSE)

## 💖 致谢

- [Face-api.js](https://github.com/justadudewhohacks/face-api.js) - AI人脸识别
- [Tailwind CSS](https://tailwindcss.com/) - UI框架
- [@Kay](https://www.xiaohongshu.com/user/profile/53171ac1b4c4d6226fdcf19a) - 原创插画贴纸
- [Cloudflare](https://www.cloudflare.com/) - CDN和托管

## 📮 联系方式

- 微信：cupaobaidou
- 公众号：醋泡白豆

---

<div align="center">
  <sub>用 ❤️ 制作 by <a href="https://github.com/yuanchaokun">yuanchaokun</a></sub>
</div>

