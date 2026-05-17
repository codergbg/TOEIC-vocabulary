# 托业单词通 (TOEIC Vocabulary)

一款高效的托业英语单词学习 web 应用，支持单词学习、发音练习和测试。

![Preview](https://img.shields.io/badge/dynamic/json?label=词汇量&query=count&url=https://raw.githubusercontent.com/codergbg/TOEIC-vocabulary/main/index.json&color=6366f1&style=flat)
![License](https://img.shields.io/badge/license-MIT-blue.svg)

## 功能特点

### 📚 每日学习
- 每日自动推荐 10 个新单词
- 科学的复习间隔帮助记忆
- 进度实时保存

### 🎤 发音练习
- 标准美式发音
- 多语速播放 (0.5x / 1x / 1.5x)
- 录音对比功能

### ✏️ 单词测试
- **选择题模式**: 根据中文释义选择正确英文
- **听力拼写模式**: 听音写单词

### 📱 移动端适配
- 响应式设计，完美支持手机浏览器
- 深色主题，护眼舒适
- 本地数据存储，无需登录

## 技术栈

- 纯 HTML / CSS / JavaScript
- Web Speech API (语音合成)
- localStorage (数据持久化)
- GitHub Pages (免费托管)

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

## 词库

收录 **567+** 核心托业词汇，涵盖:
- 商务管理类
- 沟通协作类
- 分析决策类
- 常用形容词/动词

## 目录结构

```
.
├── index.html    # 主应用文件 (单页面应用)
├── README.md     # 项目说明文档
└── .gitignore    # Git 忽略配置
```

## 部署到 GitHub Pages

1. Fork 本仓库
2. 进入 Settings → Pages
3. Source 选择 "Deploy from a branch"
4. Branch 选择 "main"，Folder 选择 "/(root)"
5. 保存后等待部署完成

## License

MIT License - 欢迎自由使用和修改

---

Made with ❤️ for TOEIC learners