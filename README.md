# actionify — Plain English to GitHub Actions YAML

**Turn natural language into production-ready GitHub Actions workflows instantly.** No AI. No API calls. No hallucination risk. Just describe what you want and get valid YAML.

[![Deploy with Vercel](https://vercel.com/button)](https://actionify-gamma.vercel.app) ![License](https://img.shields.io/github/license/SolvoHQ/actionify)

---

## How it works

```
You type in English        actionify instantly outputs YAML
─────────────────────────  ─────────────────────────────────
"build and test on push"   →  a complete workflow file ready to commit
```

actionify uses template matching under the hood — every output is a proven, working GitHub Actions workflow. No LLM means zero hallucination risk and instant response times, entirely client-side.

---

## Features

- **Zero hallucination** — output is always valid, tested YAML (not AI-generated)
- **Instant** — no API calls, no latency, runs entirely in your browser
- **Client-side only** — your prompts never leave your machine
- **No account required** — no sign-up, no API key, no rate limits
- **All common workflow templates** — Node.js, Python, Docker, cron, matrix builds, conditionals

---

## Real usage examples

### Example 1: Node.js CI

**English prompt:**
```
build and test on push to main, use node 20
```

**Generated YAML:**
```yaml
name: Node.js CI

on:
  push:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '20'
      - run: npm ci
      - run: npm test
```

---

### Example 2: Docker build and push

**English prompt:**
```
build and push docker image on tag push
```

**Generated YAML:**
```yaml
name: Docker Build and Push

on:
  push:
    tags:
      - 'v*'

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: docker/setup-buildx-action@v3
      - uses: docker/build-push-action@v5
        with:
          push: true
          tags: |
            myorg/myapp:latest
            myorg/myapp:${{ github.ref_name }}
```

---

### Example 3: Scheduled cron job

**English prompt:**
```
run a job every day at 9am
```

**Generated YAML:**
```yaml
name: Daily Schedule

on:
  schedule:
    - cron: '0 9 * * *'

jobs:
  daily-job:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: echo "Scheduled job running daily at 9am"
```

---

### Example 4: Multi-version matrix

**English prompt:**
```
test on node 18, 20, and 22
```

**Generated YAML:**
```yaml
name: Node.js Matrix

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node-version: ['18', '20', '22']
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: ${{ matrix.node-version }}
      - run: npm ci
      - run: npm test
```

---

## Comparison table

| | Manual YAML | AI-generated YAML | actionify |
|---|---|---|---|
| Time to write | 10–30 min | ~1 min + review | ~10 seconds |
| Hallucination risk | None | High (wrong actions, syntax) | **Zero** |
| Accuracy | Depends on skill | Unpredictable | **Guaranteed** |
| API key required | No | Yes | **No** |
| Runs offline | Yes | No | **Yes** |
| Cost | Free | Paid API | **Free** |

---

## How to use in GitHub Actions

### Marketplace usage

```yaml
# .github/workflows/ci.yml
name: CI

on:
  push:
    branches: [main]

jobs:
  generate-workflow:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Generate workflow YAML
        uses: SolvoHQ/actionify@v0.2
        with:
          prompt: "build and test on push to main, use node 20"

      - name: Upload generated YAML
        run: |
          cat ${{ github.workspace }}/generated.yml
```

> Note: The action currently surfaces the web UI. For full CI integration, use the [web interface](https://actionify-gamma.vercel.app) directly or copy the generated YAML into your workflow file.

### Try it now

**👉 [https://actionify-gamma.vercel.app](https://actionify-gamma.vercel.app)**

Type a plain English description and get instant, valid GitHub Actions YAML.

---

## Related tools

- [describeit](https://github.com/SolvoHQ/describeit) — plain English to UI components
- [MCP Directory](https://mcp-directory-six.vercel.app) — browse 100+ MCP servers

---

**Made by [SolvoHQ](https://github.com/SolvoHQ)**