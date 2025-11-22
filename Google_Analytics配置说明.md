# Google Analytics 配置说明

## 🎯 配置步骤

### 1. 创建 Google Analytics 账户

1. 访问 [Google Analytics](https://analytics.google.com/)
2. 使用 Google 账号登录
3. 点击"开始测量"

### 2. 创建媒体资源

1. 输入媒体资源名称：`FaceJam 贴脸酱`
2. 选择时区：`中国`
3. 选择币种：`人民币 (CNY)`
4. 点击"下一步"

### 3. 设置数据流

1. 选择平台：**网站**
2. 输入网站 URL：你的域名（例如：`facejam.cc`）
3. 输入数据流名称：`FaceJam Website`
4. 点击"创建数据流"

### 4. 获取跟踪 ID

创建完成后，你会看到一个类似 `G-XXXXXXXXXX` 的测量 ID

### 5. 替换代码中的 ID

在 `index.html` 文件中，找到以下两处并替换：

```html
<!-- 第一处：在 <head> 标签内 -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
<script>
    window.dataLayer = window.dataLayer || [];
    function gtag(){dataLayer.push(arguments);}
    gtag('js', new Date());
    gtag('config', 'G-XXXXXXXXXX', {  ← 替换这里
        'page_title': 'FaceJam 贴脸酱',
        'page_location': window.location.href
    });
</script>
```

将 `G-XXXXXXXXXX` 替换为你的实际测量 ID。

## 📊 追踪的事件

代码中已经配置了以下关键事件追踪：

| 事件名称 | 触发时机 | 分类 | 标签 |
|---------|---------|------|------|
| `upload_image` | 用户上传图片 | User Interaction | Image Upload |
| `face_detected` | AI成功检测到人脸 | AI Processing | Face Detection Success |
| `download_image` | 用户下载图片 | User Interaction | Image Download |
| `activation_success` | 用户成功激活去水印 | Monetization | Watermark Removal |
| `switch_tab` | 用户切换标签页 | User Interaction | 标签名 |
| `apply_multi_select` | 用户应用多选模式 | Feature Usage | Multi Select |

## 📈 查看统计数据

### 实时数据
1. 登录 Google Analytics
2. 选择你的媒体资源
3. 点击左侧"报告" → "实时"
4. 可以看到当前在线用户数和活动

### 事件报告
1. 点击"报告" → "互动" → "事件"
2. 查看所有自定义事件
3. 点击具体事件名称查看详细数据

### 用户报告
1. 点击"报告" → "用户"
2. 查看用户统计信息：
   - 新用户 vs 回访用户
   - 用户来源
   - 地理位置
   - 设备类型（桌面/移动）

### 转化追踪
1. 点击"管理" → "数据显示" → "事件"
2. 将 `activation_success` 标记为转化事件
3. 在报告中查看转化率

## 🔧 高级配置（可选）

### 1. 设置目标漏斗
追踪用户从上传到下载的完整流程：
1. 上传图片 → 2. 人脸检测 → 3. 应用贴纸 → 4. 下载图片

### 2. 用户属性
可以追踪更多用户信息：
- 是否激活去水印
- 常用的标签页
- 使用的语言

### 3. 设置警报
当以下情况发生时接收通知：
- 用户数突然下降
- 转化率异常
- 错误率过高

## 📱 移动端追踪

Google Analytics 会自动区分：
- 📱 移动设备访问
- 💻 桌面设备访问
- 📊 平板设备访问

## 🚀 部署后验证

1. 部署网站后，访问你的网站
2. 打开浏览器开发者工具（F12）
3. 切换到"网络"标签
4. 查找 `google-analytics.com` 或 `googletagmanager.com` 的请求
5. 如果看到请求成功，说明 GA 已正常工作

或者：
1. 登录 Google Analytics
2. 查看"实时"报告
3. 在网站上执行操作
4. 实时报告应该立即显示活动

## ⚠️ 注意事项

1. **隐私合规**：
   - 考虑添加 Cookie 同意横幅
   - 在隐私政策中说明使用 Google Analytics

2. **国内访问**：
   - Google Analytics 在中国可能加载较慢
   - 可以考虑同时使用百度统计或 CNZZ

3. **广告拦截**：
   - 部分用户使用广告拦截插件会阻止 GA
   - 实际用户数可能比统计数据多 10-30%

4. **数据延迟**：
   - 实时数据：即时
   - 标准报告：24-48 小时延迟

## 🔗 相关资源

- [Google Analytics 帮助中心](https://support.google.com/analytics)
- [GA4 事件参考](https://developers.google.com/analytics/devguides/collection/ga4/events)
- [GA4 调试](https://support.google.com/analytics/answer/7201382)

