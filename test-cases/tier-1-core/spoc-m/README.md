# SPOC-M Test Cases

## Overview

Comprehensive test cases for validating SPOC-M implementations.

## Structure

- `valid/` - Valid SPOC-M representations that should pass validation
- `invalid/` - Invalid representations that should fail validation
- `edge-cases/` - Edge cases and boundary conditions

## Test Categories

### Valid Cases

1. **minimal.json** - Minimal valid SPOC-M with only required fields
2. **complete.json** - Complete SPOC-M with all optional fields
3. **modal-variations.json** - Different modal qualifications
4. **temporal-examples.json** - Various temporal specifications

### Invalid Cases

1. **missing-subject-id.json** - Subject without required ID
2. **missing-predicate.json** - Missing predicate object
3. **invalid-modality.json** - Invalid modality value
4. **malformed-temporal.json** - Incorrectly formatted dates

## Usage

```python
import json
import jsonschema
import glob

# Load schema
with open('schemas/spoc-m/v2.5/spoc-m-core.schema.json') as f:
    schema = json.load(f)

# Test valid cases
for path in glob.glob('test-cases/tier-1-core/spoc-m/valid/*.json'):
    with open(path) as f:
        data = json.load(f)
    try:
        jsonschema.validate(instance=data, schema=schema)
        print(f"✅ {path} - VALID")
    except jsonschema.ValidationError as e:
        print(f"❌ {path} - FAILED: {e.message}")

# Test invalid cases (should fail)
for path in glob.glob('test-cases/tier-1-core/spoc-m/invalid/*.json'):
    with open(path) as f:
        data = json.load(f)
    try:
        jsonschema.validate(instance=data, schema=schema)
        print(f"❌ {path} - SHOULD HAVE FAILED")
    except jsonschema.ValidationError:
        print(f"✅ {path} - CORRECTLY REJECTED")
```

## Expected Results

- All files in `valid/` should pass validation
- All files in `invalid/` should fail validation with appropriate error messages
- Edge cases should test boundary conditions
