# 安装指南

## 系统要求

- Claude Code 1.0+
- Node.js 14+
- Python 3.8+ (用于测试框架)
- npm/yarn 包管理器

## 安装步骤

### 1. 确保环境就绪

```bash
# 检查 Node.js 版本
node --version

# 检查 Python 版本
python3 --version

# 安装测试框架依赖
pip install pytest
npm install -g playwright
playwright install
```

### 2. 安装插件

在 Claude Code 中运行：

```bash
/plugin install local /Users/visionhsu/Documents/ai_agent_demo/test-skills
```

### 3. 运行设置脚本

```bash
cd ~/.claude/plugins/*/test-automation-skill  # 找到安装位置
npm run setup
```

### 4. 验证安装

安装完成后，应该可以使用以下命令：

```bash
/test create "测试创建功能"
```

如果看到响应而不是"未知命令"，则表示安装成功。

## 疑难解答

### 插件未识别
- 确认 `package.json` 中的配置正确
- 重启 Claude Code 会话
- 检查插件是否出现在 `~/.claude/plugins/` 目录中

### 命令不可用
- 确认技能已正确加载
- 检查是否有错误消息
- 重新安装插件

### 依赖问题
- 确认所有必需的外部依赖已安装
- 检查网络连接（如果需要下载依赖）