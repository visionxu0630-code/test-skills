# Custom Test Skill 使用指南

## 概述

Custom Test Skill 是一个强大的自动化测试工具，能够理解自然语言描述并自动生成相应的测试用例。本技能支持多种测试框架，包括 Playwright、Pytest 和 JUnit，并提供了完整的测试生命周期管理。

## 安装与配置

### 1. 环境要求
- Python 3.8 或更高版本
- Node.js (如果使用 Playwright 框架)

### 2. 依赖安装
```bash
pip install pytest playwright
npm install -g playwright
playwright install
```

### 3. 技能配置

创建 `.custom-test-config.yaml` 文件来自定义默认设置：

```yaml
# .custom-test-config.yaml
framework: playwright      # 默认测试框架
language: en-US           # 默认语言
priority: high            # 默认优先级
browser: chrome           # UI测试默认浏览器
timeout: 30               # 默认超时时间（秒）
report_format: detailed   # 报告格式（basic/detailed/html）
```

## 命令使用

### /test create

根据自然语言描述创建新的测试用例。

**语法：**
```bash
/test create "描述你的测试需求"
```

**示例：**
```bash
/test create "验证用户登录功能，输入正确的用户名和密码后应成功跳转到仪表板页面"
/test create "测试API端点/api/users的GET请求，应返回状态码200和JSON格式的数据"
/test create "当输入无效邮箱格式时，注册表单应显示错误提示信息"
```

### /test run

运行测试用例。

**语法：**
```bash
/test run [all|failed|specific_test_name]
/test run --framework [playwright|pytest|junit]
/test run --tags [tag1,tag2]
/test run --priority [high|medium|low]
```

**示例：**
```bash
/test run all                  # 运行所有测试
/test run failed              # 只运行失败的测试
/test run login_tests         # 运行名为login_tests的测试
/test run --tags auth         # 运行带有auth标签的测试
/test run --priority high     # 只运行高优先级测试
```

### /test report

生成测试报告。

**语法：**
```bash
/test report
/test report --detailed
/test report --format [html|json|xml]
/test report --coverage
```

**示例：**
```bash
/test report                    # 生成基本报告
/test report --detailed         # 生成详细报告
/test report --format html      # 生成HTML格式报告
/test report --coverage         # 生成覆盖率报告
```

### /test suggest

建议额外的测试场景。

**语法：**
```bash
/test suggest --edge-cases [feature_name]
/test suggest --security [feature_name]
/test suggest --performance [feature_name]
```

**示例：**
```bash
/test suggest --edge-cases "登录功能"
/test suggest --security "支付功能"
/test suggest --performance "搜索功能"
```

## 智能功能

### 上下文感知
技能会分析项目中已有的测试用例，学习项目特有的测试模式，并根据项目类型（Web应用、API、桌面应用）调整生成策略。

### 智能推荐
基于类似功能的历史测试用例进行推荐，并自动生成边界条件和异常场景的测试。

### 覆盖率分析
分析测试用例对需求的覆盖情况，计算覆盖率指标，并识别遗漏的测试场景。

## 模板系统

技能内置了多种预定义模板，可根据不同类型的测试需求自动选择合适的模板：

- **UI 测试模板**：登录、表单验证、导航等常见UI测试场景
- **API 测试模板**：CRUD操作、认证等API测试场景
- **单元测试模板**：业务逻辑、边界条件等单元测试场景

## 框架支持

### Playwright (UI测试)
- 支持所有主流浏览器
- 提供强大的自动化功能
- 支持移动端测试

### Pytest (API和单元测试)
- 灵活的测试组织方式
- 强大的断言库
- 丰富的插件生态系统

### JUnit (Java单元测试)
- Java项目的标准测试框架
- 与Java开发工具链无缝集成

## 最佳实践

1. **清晰的需求描述**：提供尽可能详细的测试需求描述，以便技能准确理解您的意图。

2. **合理使用标签**：为测试用例添加适当的标签，便于后续管理和筛选。

3. **定期审查生成的测试**：虽然技能能智能生成测试，但仍需人工审查以确保符合具体需求。

4. **利用智能建议**：使用 `/test suggest` 命令发现可能遗漏的测试场景。

5. **配置个性化选项**：根据项目需求调整配置文件中的默认设置。

## 故障排除

### 常见问题

Q: 生成的测试用例不符合预期
A: 尝试提供更具体的描述，或使用特定的关键词引导技能生成特定类型的测试

Q: 测试运行失败
A: 检查环境配置是否正确，特别是浏览器驱动和依赖库

Q: 性能较慢
A: 检查是否同时运行过多测试，考虑按优先级或标签分批运行

## 扩展性

此技能设计为可扩展，您可以：
- 添加自定义测试框架适配器
- 创建项目特定的测试模板
- 开发定制的分析规则
- 集成CI/CD工具
- 连接项目管理工具如Jira

## 贡献

如果您有改进建议或发现了问题，请通过以下方式贡献：
- 提交GitHub Issue
- 提交Pull Request
- 更新相关文档