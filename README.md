# Test Automation Skill

一个综合性的测试自动化技能，能够根据自然语言描述自动生成测试用例、执行测试并提供测试覆盖率分析。支持多种测试框架包括 Playwright、Pytest 和 JUnit。

## 安装

### 从 Marketplace 安装（推荐）

如果你已将此仓库发布到 GitHub，可以使用以下命令安装：

```bash
# 添加此仓库作为 marketplace
/plugin marketplace add visionxu0630-code/test-skills

# 安装插件
/plugin install test-skills@test-automation
```

### 从本地安装（开发用）

1. 确保已安装依赖：
   ```bash
   npm install
   pip install pytest
   npm install -g playwright
   playwright install
   ```

2. 在 Claude Code 中运行以下命令：
   ```bash
   /plugin install local /Users/visionhsu/Documents/ai_agent_demo/test-skills
   ```

3. 运行设置命令：
   ```bash
   npm run setup
   ```

## 使用方法

安装完成后，您可以使用以下命令：

### /test create - 创建测试用例
根据自然语言描述创建测试用例：
```bash
/test create "验证用户登录功能，输入正确的用户名和密码后应成功跳转到仪表板页面"
/test create "测试API端点/api/users的GET请求，应返回状态码200和JSON格式的数据"
/test create "当输入无效邮箱格式时，注册表单应显示错误提示信息"
```

### /test run - 执行测试
运行测试用例：
```bash
/test run all                  # 运行所有测试
/test run failed              # 只运行失败的测试
/test run login_tests         # 运行特定测试
/test run --framework playwright  # 使用特定框架运行
/test run --tags auth         # 运行带auth标签的测试
/test run --priority high     # 只运行高优先级测试
```

### /test report - 生成报告
生成测试报告：
```bash
/test report                    # 生成基本报告
/test report --detailed         # 生成详细报告
/test report --format html      # 生成HTML格式报告
/test report --coverage         # 生成覆盖率报告
```

### /test suggest - 建议测试
建议额外的测试场景：
```bash
/test suggest --edge-cases "登录功能"
/test suggest --security "支付功能"
/test suggest --performance "搜索功能"
```

## 支持的测试框架

- **Playwright**: 适用于UI测试，支持所有主流浏览器
- **Pytest**: 适用于API和单元测试，具有灵活的测试组织方式
- **JUnit**: 适用于Java单元测试，与Java开发工具链无缝集成

## 配置

可通过 `.test-automation-config.yaml` 文件配置默认参数：
```yaml
# .test-automation-config.yaml
framework: playwright      # 默认测试框架
language: en-US           # 默认语言
priority: high            # 默认优先级
browser: chrome           # UI测试默认浏览器
timeout: 30               # 默认超时时间（秒）
report_format: detailed   # 报告格式（basic/detailed/html）
```

## 功能特性

- 自然语言处理，从描述生成测试用例
- 智能框架选择和测试类型识别
- 完整的测试生命周期管理
- 支持多种测试类型（UI、API、单元测试）
- 可扩展的插件架构
- 模板驱动的测试生成
- 测试覆盖率分析

## 项目结构

```
test-automation-skill/
├── package.json              # 插件配置
├── setup.js                 # 初始化脚本
├── README.md                # 主说明文档
├── INSTALL.md               # 安装指南
├── skills/
│   └── test-automation/      # 技能定义
│       └── SKILL.md
├── config/
│   └── manifest.json        # 技能元数据
├── templates/
│   └── template_definitions.yaml # 测试模板
└── GUIDE.md                 # 详细使用指南
```

## 依赖

- Node.js 14+
- Python 3.8+
- Playwright, Pytest, JUnit 相关依赖

## 贡献

欢迎提交 Issue 和 Pull Request 来改进此技能。

### 开发

1. Fork 仓库
2. 创建功能分支
3. 提交更改
4. 发起 Pull Request

## 许可证

MIT License