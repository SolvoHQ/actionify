# Development Guide — actionify

## Adding a New Template

Templates are defined in the `TEMPLATES` object in the JavaScript section of `index.html`.

Each template entry maps keywords to a YAML block. To add a new template:

1. Identify the keywords users would type to trigger this template (e.g., "docker", "container")
2. Add a new entry to `TEMPLATES` with those keywords as keys
3. Map each keyword to the appropriate YAML block

```javascript
const TEMPLATES = {
  // ... existing templates ...
  "docker build": {
    name: "Docker Build",
    yaml: `name: Docker Build
on:
  push:
    branches:
      - main
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: docker/setup-buildx-action@v3
      - uses: docker/build-push-action@v5
        with:
          push: true`,
  },
};
```

## Keyword → YAML Mapping System

The system works by:

1. **Tokenization**: User input is split into lowercase tokens
2. **Keyword matching**: Each token is checked against `TEMPLATES` keys
3. **YAML assembly**: Matching templates are combined into a complete workflow

Key files:
- `index.html` — contains `TEMPLATES` object and the `generateYaml()` function
- Template keywords use simple substring matching (e.g., "docker" matches "docker build")
- Multiple keywords can match and their YAML blocks are merged

## Template Structure

Each template object contains:
- `name`: Human-readable template name (displayed in UI)
- `yaml`: The YAML block to insert when this template matches

YAML blocks are designed to be composable — jobs and steps from different matched templates are combined into a single valid workflow file.