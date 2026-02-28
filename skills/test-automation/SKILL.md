# Test Automation Skill

## 名称
test-automation

## 描述
一个综合性的测试自动化技能，能够根据自然语言描述自动生成测试用例、执行测试并提供测试覆盖率分析。支持多种测试框架包括 Playwright、Pytest 和 JUnit。

## 目标
创建一个综合性的测试技能，能够：
- 根据自然语言描述自动生成测试用例
- 智能选择合适的测试框架
- 执行测试并报告结果
- 提供测试覆盖率分析
- 建议额外的测试场景

## 命令接口
```bash
/test create "描述你的测试需求"                 # 根据描述创建测试用例
/test run [all|failed|specific_test_name]      # 运行测试
/test run --framework [playwright|pytest|junit] # 使用特定框架运行测试
/test run --tags [tag1,tag2]                  # 运行带特定标签的测试
/test run --priority [high|medium|low]        # 运行特定优先级的测试
/test report                                  # 生成基本测试报告
/test report --detailed                       # 生成详细测试报告
/test report --format [html|json|xml]         # 生成指定格式的报告
/test report --coverage                       # 生成覆盖率报告
/test suggest --edge-cases "功能名称"          # 建议边界测试场景
/test suggest --security "功能名称"            # 建议安全测试场景
/test suggest --performance "功能名称"         # 建议性能测试场景
```

## 实现细节

### /test create - 创建测试用例
根据自然语言描述自动生成测试用例。技能将：
1. 解析用户需求描述
2. 识别测试类型（UI测试、API测试、单元测试等）
3. 智能选择最合适的测试框架
4. 生成相应的测试代码
5. 为测试分配适当的优先级和标签

**示例：**
- `/test create "验证用户登录功能，输入正确的用户名和密码后应成功跳转到仪表板页面"`
- `/test create "测试API端点/api/users的GET请求，应返回状态码200和JSON格式的数据"`
- `/test create "当输入无效邮箱格式时，注册表单应显示错误提示信息"`

### /test run - 执行测试
运行一个或多个测试用例。支持多种过滤选项：
- `all`: 运行所有测试
- `failed`: 只运行失败的测试
- `test_name`: 运行特定名称的测试
- `--framework`: 指定使用特定框架运行
- `--tags`: 运行带特定标签的测试
- `--priority`: 运行特定优先级的测试

### /test report - 生成报告
生成详细的测试执行报告，包含通过/失败统计、执行时间、覆盖率信息等。

### /test suggest - 建议测试
基于功能分析，建议额外的测试场景，包括边界条件、安全测试和性能测试。

## 实现逻辑
当用户调用技能时：

1. 解析命令和参数
2. 如果是 `/test create`:
   - 使用自然语言处理分析用户描述
   - 确定测试类型（UI、API、单元测试）
   - 选择合适的测试框架（Playwright、Pytest、JUnit）
   - 使用预定义模板生成测试代码
   - 将生成的测试保存到测试库

3. 如果是 `/test run`:
   - 加载相应的测试文件
   - 根据参数筛选测试
   - 执行测试并收集结果
   - 返回执行结果

4. 如果是 `/test report`:
   - 收集最近的测试执行结果
   - 生成格式化的报告

5. 如果是 `/test suggest`:
   - 分析现有测试覆盖范围
   - 提出可能遗漏的测试场景

## 支持的测试框架
- **Playwright**: 适用于UI测试，支持所有主流浏览器
- **Pytest**: 适用于API和单元测试，具有灵活的测试组织方式
- **JUnit**: 适用于Java单元测试，与Java开发工具链无缝集成

## 配置选项
技能支持以下配置参数：
- 默认测试框架
- 默认语言
- 默认优先级
- UI测试默认浏览器
- 默认超时时间
- 报告格式偏好

## 模板库
使用项目中的模板库定义 (templates/template_definitions.yaml) 作为基础，为常见测试场景提供标准化的测试结构。

## 使用方法
1. 使用 `/test create` 创建新测试用例
2. 使用 `/test run` 执行测试
3. 使用 `/test report` 获取结果
4. 使用 `/test suggest` 获取额外的测试建议