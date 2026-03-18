# Boss直聘简历采集插件

## 功能介绍

本插件是一个OpenClaw智能体插件，用于批量采集Boss直聘牛人管理列表的候选人信息并自动导出为Excel、CSV或JSON格式。

### 核心能力

- ✅ 无浏览器界面：纯后端API请求
- ✅ 批量采集牛人管理列表候选人信息
- ✅ 多种Cookie获取方式：支持参数传入、文件读取
- ✅ 适配OpenClaw智能体
- ✅ 精准采集核心字段：姓名、年龄、期望薪资、工作经验、学历、学校、专业、公司、简历链接
- ✅ 多页数据获取：支持获取多页数据，默认前5页，页数可配置
- ✅ 自动导出多种格式：支持Excel、CSV、JSON格式
- ✅ 一键部署到OpenClaw

---

## 🚀 一键安装（推荐）

### 方式一：GitHub一键安装

将项目发布到GitHub后，用户可以通过以下命令直接安装：

#### Linux/macOS 用户：
```bash
git clone https://github.com/你的用户名/bosszhipin-scraper-plugin.git ~/.openclaw/plugins/bosszhipin-scraper-plugin
cd ~/.openclaw/plugins/bosszhipin-scraper-plugin && npm install
openclaw restart
```

#### Windows 用户（PowerShell）：
```powershell
git clone https://github.com/你的用户名/bosszhipin-scraper-plugin.git $env:USERPROFILE\.openclaw\plugins\bosszhipin-scraper-plugin
cd $env:USERPROFILE\.openclaw\plugins\bosszhipin-scraper-plugin; npm install
openclaw restart
```

---

## 📦 手动部署步骤

### 步骤 1: 确定插件目录

OpenClaw插件目录位置：
- **Linux/macOS**: `~/.openclaw/plugins/`
- **Windows**: `%USERPROFILE%\.openclaw\plugins\`

### 步骤 2: 复制插件文件

```bash
# Linux/macOS
cp -r bosszhipin-scraper-plugin ~/.openclaw/plugins/

# Windows (PowerShell)
Copy-Item -Path bosszhipin-scraper-plugin -Destination $env:USERPROFILE\.openclaw\plugins\ -Recurse
```

### 步骤 3: 安装依赖

```bash
cd ~/.openclaw/plugins/bosszhipin-scraper-plugin
npm install
```

### 步骤 4: 配置 Cookie

将你的 `bingan-cookies.json` 文件复制到插件目录

### 步骤 5: 重启 OpenClaw

```bash
openclaw restart
```

---

## 🍪 Cookie获取方式

### 方式一：通过参数传入

#### 1. cookieString 参数
直接传入Cookie字符串，格式为 `key1=value1; key2=value2`

#### 2. cookieObject 参数
传入Cookie对象，支持多种格式

### 方式二：通过Cookie文件

插件会自动查找以下文件名的Cookie文件：
- bingan-cookies.json（默认）
- cookies.json
- cookie.json
- zhipin-cookies.json
- boss-cookies.json

---

## 💡 在 OpenClaw 中使用插件

### 通过对话使用

```
帮我采集Boss直聘的候选人信息
帮我采集Boss直聘的候选人信息，获取10页数据，导出为JSON格式
```

### 通过 API 调用

```javascript
const result = await openclaw.callPlugin('bosszhipin-scraper', 'bosszhipin:execute', {
  maxPages: 10,
  outputFormat: 'json',
  cookieString: 'zp_at=xxx; HMACCOUNT=xxx'
});

console.log(result.candidates);
```

---

## 📊 数据格式

### JSON 输出格式

插件返回的JSON数据结构：

```json
{
  "success": true,
  "message": "采集并导出成功，共 30 个候选人信息",
  "outputPath": "/path/to/resumes_xxx.json",
  "outputFormat": "json",
  "candidates": [
    {
      "id": "xxx",
      "name": "张三",
      "age": "28岁",
      "position": "高级前端工程师",
      "company": "字节跳动",
      "salary": "25-35K",
      "experience": "5-10年",
      "education": "本科",
      "school": "北京大学",
      "major": "专业不限",
      "resumeUrl": "https://www.zhipin.com/...",
      "lastMsgTime": "2024-01-14",
      "rawData": { ... }
    }
  ]
}
```

---

## ⚙️ 配置选项

| 配置项 | 类型 | 默认值 | 描述 |
|--------|------|--------|------|
| cookieFile | string | bingan-cookies.json | Cookie 文件路径 |
| cookieString | string | null | Cookie字符串 |
| cookieObject | object | null | Cookie对象 |
| outputFormat | string | excel | 导出格式 (excel/csv/json) |
| outputPath | string | . | 导出文件路径 |
| maxPages | number | 5 | 要获取的页数 |
| pageSize | number | 15 | 每页记录数 |

---

## 📋 接口说明

### OpenClaw 插件接口

- **bosszhipin:scrape**：采集候选人信息
- **bosszhipin:export**：导出数据到文件
- **bosszhipin:execute**：执行完整的采集和导出流程
- **bosszhipin:setCookie**：预先设置Cookie
- **bosszhipin:getCookieHelp**：获取Cookie帮助信息

---

## ⚠️ 注意事项

1. Cookie有一定的有效期，过期后需要重新获取
2. 请合理控制采集频率，避免被平台限制
3. Cookie包含个人登录信息，请妥善保管
4. 建议根据实际需求设置合理的页数

---

## 📝 许可证

MIT
