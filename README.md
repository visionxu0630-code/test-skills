# Test Automation Skill

一个综合性的测试自动化技能，能够根据自然语言描述自动生成测试用例、执行测试并提供测试覆盖率分析。支持多种测试框架包括 Playwright、Pytest 和 JUnit。

## 功能特性

- 自然语言处理，从描述生成测试用例
- 智能框架选择和测试类型识别
- 完整的测试生命周期管理
- 支持多种测试类型（UI、API、单元测试）
- 可扩展的插件架构
- 模板驱动的测试生成
- 测试覆盖率分析

## 安装

### 从 Marketplace 安装（推荐）

如果你已将此仓库发布到 GitHub，可以使用以下命令安装：

```bash
# 添加此仓库作为 marketplace
/plugin marketplace add visionxu0630-code/test-skills

# 安装插件
/plugin install test-automation
```

## 使用方法

安装完成后，您可以使用以下命令：

### /test-automation create - 创建测试用例
根据自然语言描述创建测试用例：
```bash
/test-automation create "验证用户登录功能，输入正确的用户名和密码后应成功跳转到仪表板页面"
/test-automation create "测试API端点/api/users的GET请求，应返回状态码200和JSON格式的数据"
/test-automation create "当输入无效邮箱格式时，注册表单应显示错误提示信息"
```

### /test-automation run - 执行测试
运行测试用例：
```bash
/test-automation run all                  # 运行所有测试
/test-automation run failed              # 只运行失败的测试
/test-automation run login_tests         # 运行特定测试
/test-automation run --framework playwright  # 使用特定框架运行
/test-automation run --tags auth         # 运行带auth标签的测试
/test-automation run --priority high     # 只运行高优先级测试
```

### /test-automation report - 生成报告
生成测试报告：
```bash
/test-automation report                    # 生成基本报告
/test-automation report --detailed         # 生成详细报告
/test-automation report --format html      # 生成HTML格式报告
/test report --coverage         # 生成覆盖率报告
```

### /test suggest - 建议测试
建议额外的测试场景：
```bash
/test-automation suggest --edge-cases "登录功能"
/test-automation suggest --security "支付功能"
/test-automation suggest --performance "搜索功能"
```

## 支持的测试框架

- **Playwright**: 适用于UI测试，支持所有主流浏览器
- **Pytest**: 适用于API和单元测试，具有灵活的测试组织方式
- **JUnit**: 适用于Java单元测试，与Java开发工具链无缝集成

## 依赖

- Node.js 14+
- Python 3.8+
- Playwright, Pytest, JUnit 相关依赖