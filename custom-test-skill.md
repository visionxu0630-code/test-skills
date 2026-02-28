# Custom Test Skill

## 名称
custom-test-skill

## 描述
一个综合性的测试技能，能够根据自然语言描述自动生成测试用例、执行测试并提供测试覆盖率分析。

## 目标
创建一个综合性的测试技能，能够：
- 根据自然语言描述自动生成测试用例
- 执行测试并报告结果
- 提供测试覆盖率分析

## 核心功能模块

### 1. 测试用例生成模块 (generator)

```python
class TestCaseGenerator:
    def __init__(self):
        self.framework_adapters = {
            'playwright': PlaywrightAdapter(),
            'pytest': PytestAdapter(),
            'junit': JUnitAdapter(),
            # ... 更多框架
        }

    def generate_from_natural_language(self, description: str) -> TestCase:
        """
        从自然语言描述生成测试用例
        """
        # 解析用户需求
        parsed_requirement = self.parse_requirement(description)

        # 识别测试类型 (UI, API, Unit等)
        test_type = self.identify_test_type(parsed_requirement)

        # 选择合适的测试框架
        framework = self.select_framework(test_type)

        # 生成具体的测试代码
        test_code = self.generate_test_code(parsed_requirement, framework)

        return TestCase(
            code=test_code,
            framework=framework,
            priority=self.calculate_priority(parsed_requirement)
        )
```

### 2. 测试执行模块 (runner)

```python
class TestRunner:
    def run_test(self, test_case: TestCase) -> TestResult:
        """
        执行测试用例
        """
        # 设置测试环境
        env = self.setup_environment(test_case)

        # 执行测试
        result = self.execute_with_framework(test_case, env)

        # 清理资源
        self.cleanup_environment(env)

        return result

    def run_multiple_tests(self, test_suite: TestSuite) -> TestReport:
        """
        批量执行测试套件
        """
        results = []
        for test_case in test_suite:
            result = self.run_test(test_case)
            results.append(result)

        return self.generate_report(results)
```

### 3. 智能分析模块 (analyzer)

```python
class TestAnalyzer:
    def analyze_requirements(self, description: str) -> RequirementAnalysis:
        """
        分析测试需求，提取关键要素
        """
        # 使用NLP技术提取实体和关系
        entities = self.extract_entities(description)

        # 识别前置条件、操作步骤、预期结果
        steps = self.parse_test_steps(description)

        # 识别测试边界条件和异常场景
        boundary_conditions = self.identify_boundary_conditions(description)

        return RequirementAnalysis(
            entities=entities,
            steps=steps,
            boundary_conditions=boundary_conditions
        )
```

## 实现流程

### 用户交互流程
1. 用户输入自然语言需求
2. 需求解析与分析模块
3. 测试类型识别
4. 框架选择
5. 测试用例生成
6. 测试执行
7. 结果分析
8. 生成测试报告

## 命令接口

```bash
/test create "用户登录功能需要验证邮箱格式正确性"
/test run all
/test run --failed
/test report --detailed
/test suggest --edge-cases "登录功能"
```

## 配置选项

```yaml
# .custom-test-config.yaml
framework: playwright  # 默认测试框架
language: en-US        # 默认语言
priority: high         # 默认优先级
browser: chrome        # UI测试默认浏览器
timeout: 30            # 默认超时时间
```

## 模板示例

以下是一个登录测试的模板示例：

```yaml
# templates/ui/login.yaml
name: "登录功能测试"
steps:
- action: "导航到登录页面"
  selector: "{{ login_url }}"
- action: "填写用户名"
  selector: "{{ username_field }}"
  value: "{{ username }}"
- action: "填写密码"
  selector: "{{ password_field }}"
  value: "{{ password }}"
- action: "点击登录按钮"
  selector: "{{ login_button }}"
- action: "验证登录成功"
  selector: "{{ success_indicator }}"
expected_results:
- condition: "URL变化"
  value: "{{ dashboard_url }}"
- condition: "元素可见"
  selector: "{{ welcome_message }}"
```

## 扩展性设计

- 支持自定义测试框架插件
- 支持自定义模板插件
- 支持自定义分析规则插件
- 与CI/CD工具集成
- 与项目管理工具集成（Jira, Azure DevOps等）
- 与监控系统集成

## 使用方法

当您想要创建测试用例时，只需提供自然语言描述，技能将自动完成：
1. 分析需求
2. 选择合适的测试框架
3. 生成相应的测试代码
4. 执行测试
5. 提供结果报告和覆盖率分析