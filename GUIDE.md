# Test Automation Skill 使用指南

## 概述

Test Automation Skill 是一个强大的自动化测试工具，能够理解自然语言描述并自动生成相应的测试用例。本技能支持多种测试框架，包括 Playwright、Pytest 和 JUnit，并提供了完整的测试生命周期管理。

## 安装与配置

### 1. 环境要求

- Claude Code 1.0+
- Node.js 14+ (用于插件系统)
- Python 3.8+ (用于测试框架)
- npm 包管理器

### 2. 依赖安装

```bash
# 安装测试框架依赖
pip install pytest
npm install -g playwright
playwright install
```

### 3. 插件安装

在 Claude Code 中运行以下命令：

```bash
/plugin install local /Users/visionhsu/Documents/ai_agent_demo/test-skills
```

### 4. 运行设置

安装后运行设置脚本：

```bash
npm run setup
```

### 5. 技能配置

创建 `.test-automation-config.yaml` 文件来自定义默认设置：

```yaml
# .test-automation-config.yaml
framework: playwright      # 默认测试框架
language: en-US           # 默认语言
priority: high            # 默认优先级
browser: chrome           # UI测试默认浏览器
timeout: 30               # 默认超时时间（秒）
report_format: detailed   # 报告格式（basic/detailed/html）
```