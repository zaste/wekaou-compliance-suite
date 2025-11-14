# WEKAOU Compliance Suite

[![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![WEKAOU Spec](https://img.shields.io/badge/WEKAOU-Spec%202.5-brightgreen)](https://github.com/zaste/wekaou-specification)

> Comprehensive validation toolkit for ensuring WEKAOU compliance across implementations.

The WEKAOU Compliance Suite provides reference validators, test harnesses, and certification tools to verify that systems correctly implement the [WEKAOU Specification](https://github.com/zaste/wekaou-specification) v2.5. This suite ensures interoperability, correctness, and quality across the WEKAOU ecosystem.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Components](#components)
- [Usage](#usage)
- [Certification](#certification)
- [Contributing](#contributing)
- [License](#license)

---

## 🎯 Overview

### What is Compliance?

WEKAOU compliance means a system:

1. **Correctly implements** META-2.5 Core primitives (SPOC-M, CRL, K-Cycle)
2. **Validates against** canonical schemas and grammars
3. **Passes** standardized test cases
4. **Maintains** quality standards defined in the specification

### Why Use This Suite?

- ✅ **Validation**: Automated checking of SPOC-M representations
- ✅ **Testing**: Comprehensive test cases for K-Cycle implementations
- ✅ **Certification**: Official compliance badges for verified systems
- ✅ **Quality Assurance**: Continuous compliance monitoring
- ✅ **Interoperability**: Ensure compatibility across implementations

---

## ✨ Features

### Core Validators

- **SPOC-M Validator**: JSON Schema-based validation of knowledge representations
- **CRL Parser**: Grammar-based validation of Canonical Representation Language
- **K-Cycle Validator**: Process conformance checking for knowledge cycles

### Test Suites

- **Unit Tests**: Atomic validation of individual components
- **Integration Tests**: Multi-component interaction validation
- **Conformance Tests**: Official WEKAOU specification compliance tests
- **Performance Tests**: Efficiency and scalability benchmarks

### Tools

- **CLI Interface**: Command-line validation and testing
- **CI/CD Integration**: GitHub Actions, GitLab CI, Jenkins support
- **Report Generation**: Detailed compliance reports in multiple formats
- **Badge Generation**: Create compliance badges for documentation

---

## 🚀 Installation

### Prerequisites

- **Python**: 3.9 or higher
- **Node.js**: 16 or higher (for CRL parser)
- **Git**: For cloning the repository

### Using pip

```bash
pip install wekaou-compliance-suite
```

### From Source

```bash
git clone https://github.com/zaste/wekaou-compliance-suite.git
cd wekaou-compliance-suite
pip install -e .
```

### Using Docker

```bash
docker pull wekaou/compliance-suite:latest
docker run -v $(pwd):/data wekaou/compliance-suite validate /data/my-spoc.json
```

---

## ⚡ Quick Start

### Validate a SPOC-M File

```bash
wekaou-validate spoc examples/sample.json
```

### Run Conformance Tests

```bash
wekaou-test conformance --suite meta-2.5-core
```

### Generate Compliance Report

```bash
wekaou-report --input my-implementation/ --output compliance-report.html
```

### Check K-Cycle Implementation

```bash
wekaou-validate k-cycle --implementation ./my_kcycle.py
```

---

## 🧩 Components

### 1. Schema Validators (`/schemas`)

Canonical JSON Schemas for WEKAOU primitives:

```
schemas/
├── spoc-m/
│   ├── v2.5/
│   │   ├── spoc-m-core.schema.json
│   │   ├── spoc-m-extended.schema.json
│   │   └── examples/
│   └── README.md
├── crl/
│   ├── grammar/
│   │   ├── crl.ebnf
│   │   ├── parser.js
│   │   └── tests/
│   └── README.md
└── k-cycle/
    ├── stages.schema.json
    ├── transitions.schema.json
    └── README.md
```

### 2. Test Cases (`/test-cases`)

Comprehensive test suite organized by tier:

```
test-cases/
├── tier-1-core/
│   ├── spoc-m/
│   │   ├── valid/
│   │   ├── invalid/
│   │   └── edge-cases/
│   ├── crl/
│   │   └── parsing/
│   └── k-cycle/
│       └── conformance/
├── tier-2-stable/
│   └── integration/
└── tier-3-experimental/
    └── performance/
```

### 3. Validators (`/validators`)

Implementation of validation logic:

```
validators/
├── python/
│   ├── wekaou_validators/
│   │   ├── spoc_m.py
│   │   ├── k_cycle.py
│   │   └── quality.py
│   └── tests/
├── javascript/
│   ├── src/
│   │   └── crl-validator.js
│   └── tests/
└── rust/
    └── (future implementation)
```

### 4. CLI Tools (`/cli`)

Command-line interface for all validation operations:

```bash
wekaou-validate   # Validate files against schemas
wekaou-test       # Run test suites
wekaou-certify    # Generate certification reports
wekaou-report     # Create compliance reports
```

---

## 📖 Usage

### SPOC-M Validation

```python
from wekaou_validators import SPOCMValidator

validator = SPOCMValidator(version="2.5")
result = validator.validate_file("my-knowledge.json")

if result.is_valid:
    print("✅ Valid SPOC-M representation")
else:
    print("❌ Validation errors:")
    for error in result.errors:
        print(f"  - {error.message} at {error.path}")
```

### CRL Parsing

```javascript
const { CRLParser } = require('wekaou-compliance-suite');

const parser = new CRLParser();
const ast = parser.parse('DISTINCTION(entity: "User", aspect: "Identity")');

if (parser.isValid()) {
  console.log('✅ Valid CRL expression');
  console.log('AST:', ast);
}
```

### K-Cycle Conformance

```python
from wekaou_validators import KCycleValidator

validator = KCycleValidator()
implementation = MyKCycleImplementation()

result = validator.check_conformance(implementation)
print(f"Conformance: {result.score}%")
print(f"Missing stages: {result.missing_stages}")
```

---

## 🏆 Certification

### Compliance Levels

The suite defines three compliance levels:

1. **Level 1 - Core Compliant** 
   - ✅ SPOC-M validation passes
   - ✅ CRL parsing correct
   - ✅ K-Cycle stages implemented

2. **Level 2 - Stable Compliant**
   - ✅ Level 1 requirements
   - ✅ Integration tests pass
   - ✅ Quality validation (VQF) implemented

3. **Level 3 - Full Compliant**
   - ✅ Level 2 requirements
   - ✅ Performance benchmarks met
   - ✅ Extended features implemented

### Getting Certified

```bash
# Run full certification suite
wekaou-certify --implementation ./my-system --output cert.json

# Generate certification badge
wekaou-badge --cert cert.json --output badge.svg
```

### Certification Badge

Once certified, add to your README:

```markdown
[![WEKAOU Compliant](https://img.shields.io/badge/WEKAOU-Level%202%20Compliant-brightgreen)](cert.json)
```

---

## 🧪 Testing Your Implementation

### Run All Tests

```bash
# Run all conformance tests
wekaou-test all --implementation ./my-system

# Run specific test suite
wekaou-test conformance --suite spoc-m

# Run with verbose output
wekaou-test all --verbose --report junit.xml
```

### CI/CD Integration

#### GitHub Actions

```yaml
name: WEKAOU Compliance
on: [push, pull_request]

jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Run WEKAOU Compliance Suite
        run: |
          pip install wekaou-compliance-suite
          wekaou-test all --implementation . --report compliance.xml
      - name: Upload results
        uses: actions/upload-artifact@v3
        with:
          name: compliance-report
          path: compliance.xml
```

---

## 📊 Reports

Generate comprehensive compliance reports:

```bash
# HTML report with visual charts
wekaou-report --format html --output report.html

# JSON report for programmatic access
wekaou-report --format json --output report.json

# Markdown report for documentation
wekaou-report --format markdown --output COMPLIANCE.md
```

### Report Contents

- ✅ Validation results by component
- ✅ Test pass/fail statistics
- ✅ Conformance score breakdown
- ✅ Recommendations for improvement
- ✅ Comparison with specification

---

## 🛠️ Development

### Running Tests

```bash
# Install dev dependencies
pip install -e ".[dev]"

# Run test suite
pytest tests/

# Run with coverage
pytest --cov=wekaou_validators tests/

# Run linters
ruff check .
mypy wekaou_validators/
```

### Adding New Validators

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on:

- Adding new schema definitions
- Creating test cases
- Implementing validators
- Submitting for review

---

## 🤝 Contributing

We welcome contributions! Please see:

- [CONTRIBUTING.md](CONTRIBUTING.md) - Contribution guidelines
- [GOVERNANCE](https://github.com/zaste/wekaou-governance) - Project governance
- [RFC Process](https://github.com/zaste/wekaou-rfc) - Proposing changes

---

## 📚 Resources

- **Specification**: [WEKAOU Specification](https://github.com/zaste/wekaou-specification)
- **Community**: [Discussions](https://github.com/zaste/wekaou-community/discussions)
- **Issues**: [Bug Reports](https://github.com/zaste/wekaou-compliance-suite/issues)
- **Documentation**: [Full Docs](docs/)

---

## 📄 License

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at:

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

---

## 🙏 Acknowledgments

This compliance suite is maintained by the WEKAOU community and Technical Steering Committee.

For questions or support:
- Open an [issue](https://github.com/zaste/wekaou-compliance-suite/issues)
- Join the [discussion](https://github.com/zaste/wekaou-community/discussions)
- Read the [documentation](docs/)

---

**Made with ❤️ by the WEKAOU Community**
