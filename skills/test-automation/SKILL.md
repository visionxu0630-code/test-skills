---
name: test-automation
description: Comprehensive test automation skill that generates test cases from natural language descriptions. Supports multiple testing frameworks including Playwright, Pytest, and JUnit.
---

# Test Automation Skill

Automates test creation, execution, and reporting based on natural language descriptions. I'll write custom test scripts for any testing scenario you describe using appropriate frameworks (Playwright for UI, Pytest for API/unit, JUnit for Java).

**CRITICAL WORKFLOW - Follow these steps in order:**

1. **Parse user request** - Extract testing requirements from natural language
2. **Identify test type** - Determine UI, API, unit, integration, etc.
3. **Choose framework** - Select Playwright, Pytest, or JUnit appropriately
4. **Write test script** to `/tmp/test-*.js` or `/tmp/test-*.py` or `/tmp/Test.java`
5. **Execute test** and report results

## How It Works

1. You describe what you want to test ("Verify login form validates email format")
2. I identify test type (UI test) and select Playwright framework
3. I write custom test script to `/tmp/test-*.js`
4. I execute the test using the appropriate runner
5. I report results and any screenshots/logs

## Setup (Prerequisites)

First-time setup to install testing frameworks:

```bash
# Install Playwright
npm install -g playwright
npx playwright install

# Install Pytest
pip install pytest

# Install JUnit (if using Java tests)
# Ensure Java JDK is installed
```

## Framework Selection Logic

- **Playwright**: UI testing (web browsers, mobile emulation)
- **Pytest**: API testing, unit testing, functional testing
- **JUnit**: Java unit/integration testing

## Command Interface

### /test create - Create Test Cases

Generate test cases from natural language descriptions:

```bash
/test create "Validate user login function, entering correct username and password should successfully navigate to dashboard page"
/test create "Test API endpoint /api/users GET request, should return status code 200 and JSON data"
/test create "When entering invalid email format, registration form should display error message"
```

**Step 1: Parse user requirement**

Analyze the natural language description and identify:
- Test type (UI, API, unit, integration)
- Elements to test (login form, API endpoint, form validation)
- Expected behavior (successful navigation, status 200, error message)

**Step 2: Choose appropriate framework**

Based on analysis:
- UI interactions → Playwright
- API calls → Pytest with requests
- Java classes → JUnit
- Database → Pytest with database connectors

**Step 3: Write test script to `/tmp`**

For UI test example:
```javascript
// /tmp/test-login-validation.js
const { chromium } = require('playwright');

( async () => {
  const browser = await chromium.launch({ headless: false });
  const page = await browser.newPage();

  // Navigate to login page
  await page.goto('YOUR_LOGIN_PAGE_URL');

  // Fill form with valid credentials
  await page.fill('#username', 'valid_user');
  await page.fill('#password', 'valid_password');
  await page.click('#login-button');

  // Verify successful navigation to dashboard
  await page.waitForURL('**/dashboard');
  console.log('✅ Login successful, redirected to dashboard');

  await browser.close();
})();
```

For API test example:
```python
# /tmp/test-api-users.py
import requests
import pytest

def test_api_users_get():
    """Test GET request to /api/users endpoint"""
    response = requests.get("http://localhost:8000/api/users")

    assert response.status_code == 200
    assert response.headers['Content-Type'] == 'application/json'

    data = response.json()
    assert isinstance(data, list)  # Expecting array of users

    print(f"✅ API test passed: Got {len(data)} users")
```

### /test run - Execute Tests

Execute existing test files:

```bash
/test run all                    # Run all tests
/test run failed                 # Run only failed tests
/test run login_tests          # Run specific test file/directory
/test run --framework playwright # Run with specific framework
/test run --tags auth          # Run tests with specific tags
/test run --priority high      # Run high priority tests only
```

**Execution workflow:**

1. Identify test file based on pattern (glob for `*login*`, or exact filename)
2. Determine framework from file extension
3. Execute with appropriate command:
   - `.js` files → `npx playwright test` or `node`
   - `.py` files → `pytest`
   - `.java` files → `javac` then `java`

### /test report - Generate Reports

Generate test reports:

```bash
/test report                   # Basic report
/test report --detailed        # Detailed report
/test report --format html     # HTML report
/test report --coverage        # Coverage report
```

**Reporting workflow:**

1. Collect output from test execution
2. Parse test results and generate summary
3. Calculate metrics (pass/fail ratio, execution time)
4. Optionally generate formatted report files

### /test suggest - Suggest Test Scenarios

Suggest additional test scenarios:

```bash
/test suggest --edge-cases "login function"
/test suggest --security "payment feature"
/test suggest --performance "search functionality"
```

**Analysis workflow:**

1. Review existing tests for coverage gaps
2. Apply testing heuristics (boundary values, error conditions, etc.)
3. Generate recommendations in natural language

## Common Testing Patterns

### Playwright UI Test Template

```javascript
// /tmp/test-template-playwright.js
const { chromium } = require('playwright');

( async () => {
  const browser = await chromium.launch({ headless: false, slowMo: 50 });
  const page = await browser.newPage();

  // Set up base URL from environment or user input
  const BASE_URL = process.env.TEST_BASE_URL || 'http://localhost:3000';

  try {
    await page.goto(BASE_URL + '/PATH_TO_TEST');

    // Add your test logic here
    await page.fill('SELECTOR', 'VALUE');
    await page.click('BUTTON_SELECTOR');

    // Assertions
    await page.waitForURL('EXPECTED_URL');
    await expect(page.locator('CHECK_SELECTOR')).toBeVisible();

    console.log('✅ Test passed');
  } catch (error) {
    console.error('❌ Test failed:', error.message);
    await page.screenshot({ path: `/tmp/error-${Date.now()}.png` });
    throw error;
  } finally {
    await browser.close();
  }
})();
```

### Pytest API Test Template

```python
# /tmp/test-template-pytest.py
import requests
import pytest
import os

BASE_URL = os.environ.get('TEST_API_BASE_URL', 'http://localhost:8000')

def test_api_endpoint():
    """Template for API endpoint testing"""
    response = requests.get(f"{BASE_URL}/ENDPOINT")

    assert response.status_code == 200
    assert response.headers.get('Content-Type') == 'application/json'

    data = response.json()
    # Add assertions based on expected response structure
    assert 'expected_field' in data

def test_api_post():
    """Template for POST request testing"""
    payload = {
        "key": "value"
    }

    response = requests.post(f"{BASE_URL}/ENDPOINT", json=payload)
    assert response.status_code == 201  # Created

    data = response.json()
    assert data['success'] is True

if __name__ == "__main__":
    pytest.main([__file__, "-v"])
```

### JUnit Java Test Template

```java
// /tmp/TestTemplate.java
import org.junit.jupiter.api.*;
import static org.junit.jupiter.api.Assertions.*;

public class TestTemplate {

    @Test
    public void testCase() {
        // Add your test logic here
        String result = performOperation();
        assertEquals("expected", result);

        System.out.println("✅ Test passed");
    }

    @Test
    public void edgeCaseTest() {
        // Test boundary conditions
        assertThrows(IllegalArgumentException.class, () -> {
            performOperationWithInvalidInput(null);
        });
    }

    private String performOperation() {
        // Operation to test
        return "expected";
    }

    private void performOperationWithInvalidInput(String input) {
        if (input == null) {
            throw new IllegalArgumentException("Input cannot be null");
        }
    }
}
```

## Best Practices

- Write tests to `/tmp` directory to avoid cluttering projects
- Use descriptive test names that explain the functionality being tested
- Include appropriate waits and assertions for reliable tests
- Parameterize URLs and values using environment variables when possible
- Clean up test data after tests complete

## Troubleshooting

- If Playwright tests fail, ensure browsers are installed: `npx playwright install`
- For Pytest tests, verify packages are installed: `pip install pytest requests`
- For Java tests, ensure JDK is properly installed and configured
- Check file permissions if tests cannot be executed from `/tmp`