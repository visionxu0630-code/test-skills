---
name: test-scenario-analysis
description: 将PRD需求文档和开发技术文档进行严格整理，最终输出严谨且可执行的测试场景
---

# 梳理测试场景技能

将产品需求文档(PRD)和开发技术文档转换为严谨且可执行的测试场景，确保测试覆盖所有功能点和边界条件。

## 核心目标

1. **解析需求文档** - 从PRD和技术文档中提取功能点和验收标准
2. **构建测试矩阵** - 创建功能测试、边界测试、异常测试的完整覆盖表
3. **生成可执行测试** - 输出可以直接运行的测试场景

## 工作流程

**步骤1：文档解析**
- 分析PRD文档中的功能需求和用户故事
- 提取业务规则、输入条件和预期结果
- 识别边界条件和异常情况

**步骤2：测试设计**
- 创建基于场景的测试用例
- 定义前置条件、测试步骤和验证点
- 标识数据依赖关系和执行顺序

**步骤3：可执行测试生成**
- 生成具体的测试脚本或测试场景
- 包含测试数据准备、执行步骤和结果验证
- 提供测试执行优先级和分类

## 指令接口

### /analyze-prd - 分析PRD文档

从PRD文档提取测试场景：
```bash
/analyze-prd "用户注册功能要求邮箱验证，支持中文名，密码需包含大小写字母和数字"
/analyze-prd --file /path/to/prd.md "分析指定PRD文档"
/analyze-prd --feature "购物车功能" --output-format gherkin
```

**分析流程：**
1. 解析PRD中的功能描述和验收标准
2. 识别输入参数、处理逻辑和预期输出
3. 生成测试场景列表

### /generate-test-scenarios - 生成测试场景

基于文档生成具体测试场景：
```bash
/generate-test-scenarios --prd /path/to/prd.md --tech-spec /path/to/spec.md
/generate-test-scenarios --feature "登录功能" --boundary-test-only
/generate-test-scenarios --format cucumber --output-dir ./features
```

**生成策略：**
- 功能性测试 - 验证核心功能按预期工作
- 边界值测试 - 测试输入参数的边界条件
- 异常测试 - 验证错误处理和恢复机制
- 性能测试 - 评估系统性能指标
- 安全测试 - 验证安全控制措施

### /create-test-matrix - 创建测试矩阵

建立需求与测试的映射关系：
```bash
/create-test-matrix --requirements /path/to/reqs.md --test-scenarios /path/to/scenarios/
/create-test-matrix --coverage-report
/create-test-matrix --gap-analysis
```

### /export-test-plan - 导出测试计划

导出完整的测试计划：
```bash
/export-test-plan --format markdown --output /tmp/test-plan.md
/export-test-plan --format excel --output test-plan.xlsx
/export-test-plan --with-execution-priority
```

## 文档分析模式

### PRD文档分析
- **功能需求** - 核心功能和子功能
- **非功能需求** - 性能、安全、可用性要求
- **验收标准** - 成功完成的标准条件
- **用户故事** - 用户使用场景和期望

### 技术规格分析
- **接口定义** - API参数、返回值、错误码
- **数据模型** - 数据结构、约束、关系
- **业务流程** - 处理步骤、状态转换
- **异常处理** - 错误情况和恢复策略

## 测试场景模板

### 功能测试场景模板
```gherkin
功能：[功能名称]
  作为[用户角色]
  我希望[功能目的]
  以便[业务价值]

  场景：[场景描述]
    给定 [前置条件]
    当 [执行操作]
    那么 [预期结果]
```

### 边界值测试场景
- 最小值、最大值测试
- 刚好超过边界值的测试
- 等价类划分测试

### 异常测试场景
- 输入异常数据
- 系统资源不足
- 并发冲突情况

## 输出格式

1. **Gherkin格式** - 用于行为驱动开发(BDD)
2. **JSON格式** - 便于自动化工具消费
3. **Markdown格式** - 便于人工审查
4. **表格格式** - 便于跟踪覆盖度

## 质量标准

- **完整性** - 所有需求都有对应测试
- **准确性** - 测试准确反映需求
- **可执行性** - 测试步骤清晰可执行
- **可追溯性** - 需求与测试的明确映射

## 最佳实践

- 每个功能点至少有3个测试场景：正常路径、边界值、异常情况
- 使用明确的数据预设条件
- 定义清晰的成功/失败判定标准
- 标注测试间的依赖关系