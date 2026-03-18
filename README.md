# 简历采集插件

## 功能介绍

本插件是一个专业级的OpenClaw智能体插件，用于批量采集Boss直聘牛人管理列表的候选人信息并自动导出为Excel或CSV格式。

### 核心能力

- ✅ **无浏览器界面**：纯后端API请求，不启动任何浏览器
- ✅ **批量采集牛人管理列表**：自动获取牛人管理页面的候选人信息
- ✅ **外部文件读取Cookie**：从bingan-cookies.json加载鉴权信息
- ✅ **适配OpenClaw智能体**：提供标准接口，可直接链接/部署
- ✅ **精准采集核心字段**：姓名、年龄、期望薪资、工作经验、学历、学校、专业、公司、简历链接
- ✅ **多页数据获取**：支持获取多页数据，默认前5页，页数可配置
- ✅ **自动导出Excel/CSV**：结构化数据，可直接用于分析
- ✅ **一键部署到OpenClaw**：支持通过bash/PowerShell命令一键安装，跨平台支持

---

## 🚀 一键安装（推荐）

### 方式一：GitHub一键安装（最简便）

将项目发布到GitHub后，用户可以通过以下**一行命令**直接安装：

#### Linux/macOS 用户：
```bash
# 一键安装到OpenClaw
bash <(curl -s https://raw.githubusercontent.com/你的用户名/resume-scraper-plugin/main/deploy-to-openclaw.sh)
```

或者分步安装：
```bash
# 克隆仓库
git clone https://github.com/你的用户名/resume-scraper-plugin.git ~/.openclaw/plugins/resume-scraper-plugin

# 安装依赖
cd ~/.openclaw/plugins/resume-scraper-plugin && npm install

# 重启OpenClaw
openclaw restart
```

#### Windows 用户（PowerShell）：
```powershell
# 一键安装到OpenClaw
iex (New-Object System.Net.WebClient).DownloadString('https://raw.githubusercontent.com/你的用户名/resume-scraper-plugin/main/deploy-to-openclaw.ps1')
```

或者分步安装：
```powershell
# 克隆仓库
git clone https://github.com/你的用户名/resume-scraper-plugin.git $env:USERPROFILE\.openclaw\plugins\resume-scraper-plugin

# 安装依赖
cd $env:USERPROFILE\.openclaw\plugins\resume-scraper-plugin; npm install

# 重启OpenClaw
openclaw restart
```

---

### 方式二：使用部署脚本安装

#### 从GitHub下载脚本并运行

**Linux/macOS:**
```bash
# 下载部署脚本
curl -o deploy-to-openclaw.sh https://raw.githubusercontent.com/你的用户名/resume-scraper-plugin/main/deploy-to-openclaw.sh

# 添加执行权限
chmod +x deploy-to-openclaw.sh

# 运行脚本（从GitHub安装）
./deploy-to-openclaw.sh
```

**Windows (PowerShell):**
```powershell
# 下载部署脚本
Invoke-WebRequest -Uri "https://raw.githubusercontent.com/你的用户名/resume-scraper-plugin/main/deploy-to-openclaw.ps1" -OutFile "deploy-to-openclaw.ps1"

# 运行脚本（从GitHub安装）
powershell -ExecutionPolicy Bypass -File deploy-to-openclaw.ps1
```

#### 本地安装（开发者模式）

如果你已经下载了源码，可以从本地安装：

**Linux/macOS:**
```bash
cd resume-scraper-plugin
./deploy-to-openclaw.sh --local
```

**Windows (PowerShell):**
```powershell
cd resume-scraper-plugin
powershell -ExecutionPolicy Bypass -File deploy-to-openclaw.ps1 -Local
```

---

### 方式三：使用 npm 脚本安装

```bash
# 进入项目目录
cd resume-scraper-plugin

# 自动安装（跨平台）
npm run install:local

# 然后进入插件目录安装依赖
# Linux/macOS:
cd ~/.openclaw/plugins/resume-scraper-plugin && npm install

# Windows:
cd $env:USERPROFILE\.openclaw\plugins\resume-scraper-plugin; npm install
```

---

## 📦 手动部署步骤

如果以上自动化方式不适用，可以手动部署：

### 步骤 1: 确定插件目录

OpenClaw插件目录位置：

| 系统 | 路径 |
|------|------|
| Linux/macOS | `~/.openclaw/plugins/` |
| Windows | `%USERPROFILE%\.openclaw\plugins\` |

### 步骤 2: 复制插件文件

**Linux/macOS:**
```bash
# 从GitHub克隆
git clone https://github.com/你的用户名/resume-scraper-plugin.git ~/.openclaw/plugins/resume-scraper-plugin

# 或从本地复制
cp -r resume-scraper-plugin ~/.openclaw/plugins/
```

**Windows (PowerShell):**
```powershell
# 从GitHub克隆
git clone https://github.com/你的用户名/resume-scraper-plugin.git $env:USERPROFILE\.openclaw\plugins\resume-scraper-plugin

# 或从本地复制
Copy-Item -Path resume-scraper-plugin -Destination $env:USERPROFILE\.openclaw\plugins\ -Recurse
```

### 步骤 3: 安装依赖

```bash
# 进入插件目录
# Linux/macOS:
cd ~/.openclaw/plugins/resume-scraper-plugin

# Windows:
cd $env:USERPROFILE\.openclaw\plugins\resume-scraper-plugin

# 安装依赖
npm install
```

### 步骤 4: 配置 Cookie

将你的 `bingan-cookies.json` 文件复制到插件目录：

**Linux/macOS:**
```bash
cp /path/to/your/bingan-cookies.json ~/.openclaw/plugins/resume-scraper-plugin/
```

**Windows:**
```powershell
Copy-Item -Path C:\path\to\bingan-cookies.json -Destination $env:USERPROFILE\.openclaw\plugins\resume-scraper-plugin\
```

### 步骤 5: 重启 OpenClaw

```bash
openclaw restart
```

### 步骤 6: 验证安装

```bash
openclaw plugins list
```

你应该能看到 `resume-scraper-plugin` 在列表中。

---

## 💡 在 OpenClaw 中使用插件

### 通过对话使用

在 OpenClaw 的对话界面中：

#### 示例 1: 采集默认页数（5页）
```
帮我采集Boss直聘的候选人信息
```

#### 示例 2: 采集指定页数
```
帮我采集Boss直聘的候选人信息，获取10页数据
```

#### 示例 3: 导出数据
```
将刚才采集的候选人信息导出为Excel
```

### 通过 API 调用

```javascript
// 调用采集接口
const result = await openclaw.callPlugin('resume-scraper', 'resume:execute', {
  maxPages: 10
});

console.log(result);
```

---

## ⚙️ 配置选项

插件支持以下配置：

| 配置项 | 类型 | 默认值 | 描述 |
|--------|------|--------|------|
| cookieFile | string | bingan-cookies.json | Cookie 文件路径 |
| outputFormat | string | excel | 导出格式 (excel/csv) |
| outputPath | string | . | 导出文件路径 |
| maxPages | number | 5 | 要获取的页数 |
| pageSize | number | 15 | 每页记录数 |

---

## 📋 接口说明

### OpenClaw 插件接口

- **resume:scrape**：采集候选人信息
  - 参数：`maxPages`（可选，指定页数）
  - 返回：候选人信息数组

- **resume:export**：导出数据到文件
  - 参数：`data`（候选人信息数组）
  - 返回：导出文件路径

- **resume:execute**：执行完整的采集和导出流程
  - 参数：`maxPages`（可选，指定页数）
  - 返回：包含成功状态、消息、输出路径和候选人信息的对象

---

## 📊 数据字段说明

导出的数据包含以下字段：

- **姓名**：候选人姓名
- **年龄**：候选人年龄
- **工作时长**：工作经验年限
- **学历**：学历（本科/硕士/大专等）
- **学校**：毕业院校
- **专业**：专业（如无则显示"专业不限"）
- **职位**：期望职位
- **公司**：当前/最近公司
- **期望薪资**：期望薪资
- **简历链接**：简历详情页链接
- **最后消息日期**：最后沟通日期

---

## 🔄 更新插件

### 从 GitHub 更新

**Linux/macOS:**
```bash
cd ~/.openclaw/plugins/resume-scraper-plugin
git pull
npm install
openclaw restart
```

**Windows:**
```powershell
cd $env:USERPROFILE\.openclaw\plugins\resume-scraper-plugin
git pull
npm install
openclaw restart
```

### 本地更新

重新运行部署脚本即可：

**Linux/macOS:**
```bash
./deploy-to-openclaw.sh --local
```

**Windows:**
```powershell
powershell -ExecutionPolicy Bypass -File deploy-to-openclaw.ps1 -Local
```

---

## ⚠️ 注意事项

1. **Cookie 有效期**：Cookie 有一定的有效期，过期后需要重新获取
2. **API 限制**：请合理控制采集频率，避免被平台限制
3. **数据安全**：Cookie 包含个人登录信息，请妥善保管
4. **页数限制**：建议根据实际需求设置合理的页数，避免过度采集
5. **OpenClaw 版本**：确保你的 OpenClaw 版本支持插件功能

---

## ❓ 常见问题

### Q1: 采集失败，提示 Cookie 无效

**A**: 重新获取 Cookie 并更新 `bingan-cookies.json` 文件

### Q2: 导出文件为空

**A**: 检查 Cookie 是否有效，以及 Boss 直聘牛人管理页面是否有数据

### Q3: API 请求失败

**A**:
- 确认 Cookie 有效
- 检查网络连接
- 查看控制台错误信息

### Q4: OpenClaw 中找不到插件

**A**:
- 确认插件已正确复制到 OpenClaw 插件目录
- 检查是否运行了 `npm install`
- 重启 OpenClaw
- 检查 `openclaw.plugin.json` 文件是否存在且格式正确

### Q5: 权限被拒绝（Windows）

**A**: 在 PowerShell 中使用 `-ExecutionPolicy Bypass` 参数运行脚本

---

## 🛠️ 技术实现

- 使用 `axios` 进行 HTTP 请求
- 使用 `xlsx` 导出 Excel 文件
- 使用 `csv-writer` 导出 CSV 文件
- 直接调用 Boss 直聘 API 接口获取数据

---

## 📁 项目结构

```
resume-scraper-plugin/
├── index.js                  # 主插件文件
├── package.json              # 项目依赖配置
├── package-lock.json         # 依赖锁定文件
├── openclaw.plugin.json      # OpenClaw 插件配置
├── .gitignore               # Git 忽略规则
├── deploy-to-openclaw.sh    # Linux/macOS 一键部署脚本
├── deploy-to-openclaw.ps1   # Windows PowerShell 一键部署脚本
├── README.md                # 使用说明文档
└── bingan-cookies.json      # Cookie 文件（需要用户提供，不提交到 Git）
```

---

## 🚀 发布到 GitHub 前的检查清单

在发布到 GitHub 之前，请确保：

- [ ] 删除了所有包含真实数据的文件（`resumes_*.xlsx`, `resumes_*.csv`）
- [ ] 删除了 `bingan-cookies.json` 文件
- [ ] 确认 `.gitignore` 文件正确配置
- [ ] 更新了 `README.md` 中的 GitHub 仓库地址
- [ ] 更新了 `deploy-to-openclaw.sh` 中的 GitHub 仓库地址
- [ ] 更新了 `deploy-to-openclaw.ps1` 中的 GitHub 仓库地址
- [ ] 更新了 `package.json` 中的仓库信息
- [ ] 测试了插件功能正常
- [ ] 测试了一键部署脚本

---

## 📝 许可证

MIT
