---
name: test-automation
description: Comprehensive test automation skill that generates test cases from natural language descriptions. Supports multiple testing frameworks including Playwright, Pytest, and JUnit.
---

# 测试自动化技能

**用途：** 当用户提供测试需求描述时，自动激活此技能来自动生成测试代码、执行测试并生成报告。

## 触发条件

激活此技能当用户：
- 描述需要测试的功能（如"验证登录表单验证邮箱格式"）
- 请求"生成测试代码"、"创建测试"、"写自动化测试"
- 要求"执行测试"、"运行测试"、"查看测试报告"
- 手动使用 `/test-automation` 命令

## 工具依赖

- `write` - 生成测试脚本文件
- `bash` - 执行测试命令和安装依赖
- `read` - 读取现有的测试文件
- 无工具时：基于用户提供的文本内容生成测试代码

## 工作流程

### 1. 需求解析
- 从自然语言描述中提取测试需求
- 识别测试类型（UI、API、单元、集成等）
- 分析测试元素和预期行为

### 2. 框架选择
- UI测试 → Playwright
- API/单元测试 → Pytest
- Java测试 → JUnit

### 3. 代码生成
- 根据测试类型生成相应框架的测试代码
- 保存到临时目录或用户指定位置
- 包含适当的断言和验证

### 4. 测试执行
- 运行生成的测试
- 收集执行结果和日志
- 生成测试报告

## 使用示例

### 示例 1：UI测试生成

**用户：**
> 验证用户登录功能，输入正确的用户名和密码应成功跳转到仪表板页面

**助手：**
好的，我将为您生成UI测试：

```javascript
// Playwright UI测试示例
const { chromium } = require('playwright');

( async () => {
  const browser = await chromium.launch({ headless: false });
  const page = await browser.newPage();

  // 导航到登录页面
  await page.goto('YOUR_LOGIN_PAGE_URL');

  // 使用有效凭据填写表单
  await page.fill('#username', 'valid_user');
  await page.fill('#password', 'valid_password');
  await page.click('#login-button');

  // 验证成功跳转到仪表板
  await page.waitForURL('**/dashboard');
  console.log('✅ 登录成功，已跳转到仪表板');

  await browser.close();
})();
```

### 示例 2：API测试生成

**用户：**
> 测试API端点 /api/users GET请求，应返回状态码200和JSON数据

**助手：**
好的，我将为您生成API测试：

```python
import requests
import pytest

def test_api_users_get():
    """测试 /api/users 端点的GET请求"""
    response = requests.get("http://localhost:8000/api/users")

    assert response.status_code == 200
    assert response.headers['Content-Type'] == 'application/json'

    data = response.json()
    assert isinstance(data, list)  # 期望用户数组

    print(f"✅ API测试通过: 获取到 {len(data)} 个用户")
```

### 示例 3：测试执行和报告

**用户：**
> 运行上面生成的测试并给我报告

**助手：**
正在执行测试...

1. 确保所需框架已安装
2. 运行测试
3. 生成测试报告

执行结果：所有测试通过，覆盖率95%

## 框架选择指南

- **Playwright**: Web UI测试、浏览器自动化、移动端模拟
- **Pytest**: API测试、单元测试、功能测试、数据驱动测试
- **JUnit**: Java应用程序的单元/集成测试

## 输出模板

### Playwright测试模板

```javascript
const { chromium } = require('playwright');

(async () => {
  const browser = await chromium.launch({ headless: false, slowMo: 50 });
  const page = await browser.newPage();

  // 设置基础URL
  const BASE_URL = process.env.TEST_BASE_URL || 'http://localhost:3000';

  try {
    await page.goto(BASE_URL + '/PATH_TO_TEST');

    // 添加您的测试逻辑
    await page.fill('SELECTOR', 'VALUE');
    await page.click('BUTTON_SELECTOR');

    // 断言
    await page.waitForURL('EXPECTED_URL');
    await expect(page.locator('CHECK_SELECTOR')).toBeVisible();

    console.log('✅ 测试通过');
  } catch (error) {
    console.error('❌ 测试失败:', error.message);
    await page.screenshot({ path: `/tmp/error-${Date.now()}.png` });
    throw error;
  } finally {
    await browser.close();
  }
})();
```

### Pytest测试模板

```python
import requests
import pytest
import os

BASE_URL = os.environ.get('TEST_API_BASE_URL', 'http://localhost:8000')

def test_api_endpoint():
    """API端点测试模板"""
    response = requests.get(f"{BASE_URL}/ENDPOINT")

    assert response.status_code == 200
    assert response.headers.get('Content-Type') == 'application/json'

    data = response.json()
    # 根据预期响应结构添加断言
    assert 'expected_field' in data

def test_api_post():
    """POST请求测试模板"""
    payload = {
        "key": "value"
    }

    response = requests.post(f"{BASE_URL}/ENDPOINT", json=payload)
    assert response.status_code == 201  # 已创建

    data = response.json()
    assert data['success'] is True

if __name__ == "__main__":
    pytest.main([__file__, "-v"])
```

## 快速安装指南

如果遇到依赖缺失，请运行相应的安装命令：

```bash
# 安装Playwright
npm install -g playwright
npx playwright install

# 安装Pytest
pip install pytest requests

# Java项目需要JDK
# 确保Java JDK已安装
```

## 质量标准

- ✅ **准确性** - 测试准确反映用户需求
- ✅ **完整性** - 包含必要的断言和验证
- ✅ **可维护性** - 代码结构清晰，易于修改
- ✅ **可执行性** - 测试可在适当环境中运行

## 不适用场景

以下情况不激活此技能：
- 简单的理论咨询（如"什么是测试自动化"）
- 非测试相关的讨论
- 用户明确表示不需要生成实际代码

## 最佳实践

1. 使用描述性测试名称，说明被测试功能
2. 包含适当的等待和断言以确保测试可靠性
3. 尽可能使用环境变量参数化URL和值
4. 测试完成后清理测试数据
5. 为不同测试场景编写独立的测试函数