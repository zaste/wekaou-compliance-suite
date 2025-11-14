# SPOC-M Schema

## Overview

This directory contains the canonical JSON Schema definitions for SPOC-M (Subject-Predicate-Object-Context-Mechanism) knowledge representations in WEKAOU.

## Structure

```
spoc-m/
├── v2.5/
│   ├── spoc-m-core.schema.json      # Core SPOC-M schema
│   ├── spoc-m-extended.schema.json  # Extended features
│   └── examples/
│       ├── valid/                    # Valid SPOC-M examples
│       └── invalid/                  # Invalid examples (for testing)
└── README.md
```

## Usage

### Python

```python
import jsonschema
import json

with open('spoc-m-core.schema.json') as f:
    schema = json.load(f)

with open('my-knowledge.json') as f:
    data = json.load(f)

jsonschema.validate(instance=data, schema=schema)
```

### JavaScript

```javascript
const Ajv = require('ajv');
const schema = require('./spoc-m-core.schema.json');

const ajv = new Ajv();
const validate = ajv.compile(schema);

const valid = validate(data);
if (!valid) console.log(validate.errors);
```

## Validation Rules

### Required Fields

- `subject.id`: Must be a non-empty string
- `subject.type`: Must be a non-empty string
- `predicate.relation`: Must be a non-empty string
- `object.value`: Required but can be any type

### Optional Fields

- `context`: Provides domain, scope, and perspective
- `mechanism`: Describes the process or causality
- `metadata`: Information about the statement itself

## Examples

### Minimal Valid SPOC-M

```json
{
  "subject": {
    "id": "user:12345",
    "type": "Person"
  },
  "predicate": {
    "relation": "hasRole"
  },
  "object": {
    "value": "Administrator"
  }
}
```

### Full SPOC-M with All Fields

```json
{
  "subject": {
    "id": "org:acme",
    "type": "Organization",
    "label": "ACME Corporation",
    "attributes": {
      "founded": 1995,
      "employees": 5000
    }
  },
  "predicate": {
    "relation": "implements",
    "modality": "actuality",
    "temporality": {
      "start": "2024-01-01T00:00:00Z"
    }
  },
  "object": {
    "value": "WEKAOU",
    "type": "Framework"
  },
  "context": {
    "domain": "Enterprise Architecture",
    "scope": "Company-wide",
    "perspective": "Technical Leadership"
  },
  "mechanism": {
    "type": "Incremental Adoption",
    "causality": "causal"
  },
  "metadata": {
    "version": "2.5",
    "created": "2024-11-14T00:00:00Z",
    "author": "system",
    "confidence": 0.95
  }
}
```

## Versioning

Schemas are versioned according to the WEKAOU specification version. The current version is **2.5**.

## Contributing

Changes to schemas must go through the RFC process. See [WEKAOU RFC](https://github.com/zaste/wekaou-rfc).
