# 托业单词通 (TOEIC Vocabulary)

一款高效的托业英语单词学习 web 应用，支持单词学习、发音练习和测试。

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Platform](https://img.shields.io/badge/platform-Web-brightgreen.svg)
![Vocabulary](https://img.shields.io/badge/vocabulary-567%2B-orange)

## 功能特点

### 📚 每日学习
- 每日自动推荐 10 个新单词
- 科学的复习间隔帮助记忆
- 进度实时保存到本地

### 🎤 发音练习
- 标准美式发音 (Web Speech API)
- 多语速播放 (0.5x / 1x / 1.5x)
- 录音对比功能（浏览器支持时可用）

### ✏️ 单词测试
- **选择题模式**: 根据中文释义选择正确英文
- **听力拼写模式**: 听音写单词

### 📱 移动端适配
- 响应式设计，完美支持手机浏览器
- 深色主题，护眼舒适
- 本地数据存储，无需登录

---

## 项目设计说明

### 🏗️ 架构设计

本项目采用 **单页面应用 (SPA)** 架构，所有功能集成在一个 HTML 文件中。

```
┌─────────────────────────────────────────────────────┐
│                     index.html                       │
├─────────────────────────────────────────────────────┤
│  ┌─────────┐  ┌─────────┐  ┌──────────────────┐   │
│  │  学习页  │  │  练习页  │  │     测试页       │   │
│  │ (Learn) │  │(Practice)│  │     (Test)       │   │
│  └─────────┘  └─────────┘  └────────────────────┘   │
├─────────────────────────────────────────────────────┤
│                   JavaScript 逻辑                    │
│  ┌─────────────┐  ┌─────────────┐  ┌────────────┐ │
│  │  状态管理   │  │  语音合成   │  │  数据持久化 │ │
│  │ (State)    │  │(Speech API) │  │(localStorage│ │
│  └─────────────┘  └─────────────┘  └────────────┘ │
├─────────────────────────────────────────────────────┤
│                     CSS 样式                         │
│  ┌─────────────┐  ┌─────────────┐  ┌────────────┐ │
│  │  布局系统   │  │  动画效果   │  │  主题配色  │ │
│  └─────────────┘  └─────────────┘  └────────────┘ │
└─────────────────────────────────────────────────────┘
```

### 📊 数据结构

#### 单词数据模型
```javascript
{
    word: "ability",           // 英文单词
    phonetic: "/əˈbɪləti/",    // 发音音标
    meaning: "能力",           // 中文释义
    example: "She has ...",    // 英文例句
    exampleCn: "她有..."       // 例句中文翻译
}
```

#### 应用状态
```javascript
{
    learnedWords: ["ability", "absorb", ...],  // 已学习的单词
    dailyWords: [...],                          // 今日学习的单词
    currentIndex: 3,                            // 当前学习进度
    practiceIndex: 5,                           // 练习页面单词索引
    testMode: 'choice',                         // 测试模式选择
    testQuestions: [...],                       // 当前测试题目
    speechRate: 1                               // 语音语速
}
```

### 🎨 界面设计

#### 配色方案
采用深色主题设计，减少眼睛疲劳：

| 颜色变量 | 颜色值 | 用途 |
|---------|--------|------|
| `--primary` | `#0f0f23` | 页面背景 |
| `--secondary` | `#1a1a3e` | 卡片背景 |
| `--accent` | `#6366f1` | 主题强调色 |
| `--success` | `#10b981` | 正确/认识按钮 |
| `--warning` | `#f59e0b` | 提示信息 |
| `--error` | `#ef4444` | 错误提示 |

#### 响应式断点
```
移动端: < 480px (最大宽度适配)
平板/桌面: >= 480px (居中显示，最大520px)
```

### 🔄 数据流

#### 学习流程
```
用户打开应用
       ↓
判断 localStorage 是否有数据
       ↓
是 → 读取历史学习进度
否 → 初始化新用户状态
       ↓
获取今日单词 (从剩余未学习单词中随机抽取10个)
       ↓
显示单词卡片 (仅显示英文和音标)
       ↓
用户点击"认识" → 标记为已学习，进入下一个
用户点击"不认识" → 跳过当前，进入下一个
       ↓
每日学习完成 → 显示完成页面
```

#### 测试流程
```
选择测试模式 (选择题/听力拼写)
       ↓
生成10道题目 (从已学习单词中随机抽取)
       ↓
选择题: 显示中文释义 → 用户选择英文 → 立即反馈
听写: 播放读音 → 用户输入英文 → 立即反馈
       ↓
10题完成后 → 显示成绩统计
       ↓
保存成绩到历史记录 (保留最近20条)
```

### 🧩 核心模块

| 模块 | 职责 |
|------|------|
| `VOCABULARY` | 单词数据常量，包含567+托业词汇 |
| `loadState()` | 从 localStorage 加载用户进度 |
| `saveState()` | 保存用户进度到 localStorage |
| `getDailyWords()` | 获取今日学习单词（随机10个） |
| `switchPage()` | 页面切换逻辑 |
| `speakWord()` | 语音合成播放 |
| `toggleRecording()` | 麦克风录音功能 |

### ⚡ 性能优化

1. **单文件部署**: 所有代码整合在一个 HTML 文件，减少 HTTP 请求
2. **本地存储**: 使用 localStorage，无服务器端依赖
3. **懒加载**: 语音数据在需要时加载
4. **CSS 变量**: 使用 CSS 变量便于主题切换

### 🔐 安全考虑

- 所有数据存储在用户本地 localStorage
- 不收集任何个人信息
- 无需网络请求即可离线使用
- 录音功能仅在用户授权后启用

---

## 技术栈

- 纯 HTML / CSS / JavaScript (无框架依赖)
- Web Speech API (语音合成)
- Web Audio API (录音功能)
- localStorage (数据持久化)
- GitHub Pages (免费托管)

---

## 快速开始

### 本地运行
```bash
# 克隆仓库
git clone https://github.com/codergbg/TOEIC-vocabulary.git

# 使用任意 HTTP 服务器打开
# 例如使用 Python
cd TOEIC-vocabulary
python -m http.server 8080

# 浏览器访问 http://localhost:8080
```

### 在线访问
访问 → [https://codergbg.github.io/TOEIC-vocabulary/](https://codergbg.github.io/TOEIC-vocabulary/)

---

## 词库

收录 **567+** 核心托业词汇，按字母分类：

- **A**: ability, absorb, academic, accept...
- **B**: background, balance, barrier, benefit...
- **C**: calculate, candidate, career, challenge...
- **D**: damage, data, deadline, deal...
- **E**: ease, economic, effective, efficient...

涵盖领域：商务、管理、沟通、分析、技术等

---

## 目录结构

```
.
├── index.html    # 主应用文件 (单页面应用)
├── README.md     # 项目说明文档
└── .gitignore    # Git 忽略配置
```

---

## 常见问题

### Q: 手机上点击发音没有声音？
A: 部分移动浏览器需要用户先与页面交互才能播放音频。请先点击页面任意位置几次，再点击发音按钮。

### Q: 学习进度会丢失吗？
A: 不会。学习进度保存在浏览器 localStorage 中，关闭页面后再次打开会自动恢复。

### Q: 可以自定义单词吗？
A: 目前版本单词库是内置的。如需添加自定义单词，可以编辑 `index.html` 中的 `VOCABULARY` 数组。

---

## 部署到 GitHub Pages

1. Fork 本仓库
2. 进入 Settings → Pages
3. Source 选择 "Deploy from a branch"
4. Branch 选择 "main"，Folder 选择 "/(root)"
5. 保存后等待部署完成

---

## License

MIT License

---

Made with ❤️ for TOEIC learners