# Contributing to WEKAOU Compliance Suite

Thank you for your interest in contributing! This document provides guidelines for contributing to the WEKAOU Compliance Suite.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [How to Contribute](#how-to-contribute)
- [Development Setup](#development-setup)
- [Adding Validators](#adding-validators)
- [Adding Test Cases](#adding-test-cases)
- [Adding Schemas](#adding-schemas)
- [Pull Request Process](#pull-request-process)
- [Coding Standards](#coding-standards)

---

## Code of Conduct

This project follows the WEKAOU [Code of Conduct](https://github.com/zaste/wekaou-.github/blob/main/CODE_OF_CONDUCT.md). By participating, you agree to uphold this code.

---

## How to Contribute

### Types of Contributions

- **Bug Reports**: Found a validation bug? Open an issue
- **Feature Requests**: Need new validation capabilities? Propose via RFC
- **Test Cases**: Add new test cases to improve coverage
- **Validators**: Implement validators in new languages
- **Documentation**: Improve docs and examples
- **Schemas**: Enhance or extend validation schemas

---

## Development Setup

### Prerequisites

```bash
# Python 3.9+
python --version

# Node.js 16+
node --version

# Git
git --version
```

### Clone and Install

```bash
git clone https://github.com/zaste/wekaou-compliance-suite.git
cd wekaou-compliance-suite

# Install Python dependencies
pip install -e ".[dev]"

# Install Node.js dependencies
cd validators/javascript
npm install
```

### Run Tests

```bash
# Python tests
pytest tests/ -v

# JavaScript tests
cd validators/javascript
npm test

# All tests
make test
```

---

## Adding Validators

### Python Validator

1. Create validator in `validators/python/wekaou_validators/`
2. Implement validator class following the interface:

```python
from abc import ABC, abstractmethod
from typing import Dict, Any
from dataclasses import dataclass

@dataclass
class ValidationResult:
    is_valid: bool
    errors: list
    warnings: list

class BaseValidator(ABC):
    @abstractmethod
    def validate(self, data: Dict[str, Any]) -> ValidationResult:
        pass
```

3. Add tests in `validators/python/tests/`
4. Update documentation

### JavaScript Validator

1. Create validator in `validators/javascript/src/`
2. Follow the validator interface
3. Add tests in `validators/javascript/tests/`
4. Update documentation

---

## Adding Test Cases

### Directory Structure

Place test cases in the appropriate tier:

```
test-cases/
├── tier-1-core/          # Core specification compliance
├── tier-2-stable/        # Stable features
└── tier-3-experimental/  # Experimental features
```

### Test Case Format

Each test case should include:

1. **JSON file** with test data
2. **Metadata** describing expected behavior
3. **README** explaining the test

### Example Test Case

```json
{
  "$test": {
    "description": "Valid SPOC-M with temporal context",
    "expected": "pass",
    "validator": "spoc-m-core",
    "version": "2.5"
  },
  "subject": {
    "id": "test:001",
    "type": "TestEntity"
  },
  "predicate": {
    "relation": "hasProperty",
    "temporality": {
      "start": "2024-01-01T00:00:00Z"
    }
  },
  "object": {
    "value": "test-value"
  }
}
```

---

## Adding Schemas

### Schema Guidelines

1. Follow [JSON Schema Draft 07](https://json-schema.org/draft-07/schema)
2. Include comprehensive descriptions
3. Add examples in schema documentation
4. Version schemas according to WEKAOU spec

### Schema Versioning

- Major version changes require RFC approval
- Minor version changes can be proposed via PR
- Always maintain backwards compatibility

### Schema Structure

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "$id": "https://wekaou.org/schemas/[component]/v[version]/[name]",
  "title": "Schema Title",
  "description": "Detailed description",
  "type": "object",
  "required": ["field1", "field2"],
  "properties": {
    "field1": {
      "type": "string",
      "description": "Field description"
    }
  }
}
```

---

## Pull Request Process

### Before Submitting

1. ✅ Run all tests: `make test`
2. ✅ Run linters: `make lint`
3. ✅ Update documentation
4. ✅ Add test cases for new features
5. ✅ Follow conventional commits

### PR Template

```markdown
## Description

[Brief description of changes]

## Type of Change

- [ ] Bug fix
- [ ] New feature
- [ ] Test case addition
- [ ] Documentation update
- [ ] Schema change

## Testing

- [ ] All tests pass
- [ ] New tests added
- [ ] Manual testing performed

## Checklist

- [ ] Code follows style guidelines
- [ ] Documentation updated
- [ ] Tests added/updated
- [ ] No breaking changes (or documented)
```

### Review Process

1. Automated checks must pass
2. At least one maintainer approval required
3. Address all review comments
4. Squash commits before merge

---

## Coding Standards

### Python

- Follow PEP 8
- Use type hints
- Maximum line length: 100 characters
- Use `ruff` for linting
- Use `mypy` for type checking

```bash
ruff check .
mypy wekaou_validators/
```

### JavaScript

- Follow StandardJS style
- Use ES6+ features
- Document with JSDoc comments
- Use ESLint

```bash
npm run lint
```

### Commit Messages

Use [Conventional Commits](https://www.conventionalcommits.org/):

```
feat(validators): add K-Cycle conformance checker
fix(schemas): correct SPOC-M temporal validation
docs(readme): update installation instructions
test(spoc-m): add edge case for nested contexts
```

---

## Questions?

- **General questions**: [Community Discussions](https://github.com/zaste/wekaou-community/discussions)
- **Bug reports**: [Issues](https://github.com/zaste/wekaou-compliance-suite/issues)
- **Feature proposals**: [RFC Process](https://github.com/zaste/wekaou-rfc)

---

Thank you for contributing to WEKAOU! 🎉
