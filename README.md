# GitHub First Actions

A learning repository for getting started with GitHub Actions CI/CD automation and workflow orchestration.

## 📋 Description

This repository contains examples and tutorials for GitHub Actions, demonstrating how to create automated workflows for continuous integration, continuous deployment, testing, and build automation.

## 🛠️ Tech Stack

- **CI/CD Platform:** GitHub Actions
- **Workflow Orchestration:** YAML
- **Languages:** JavaScript, Python, Go (examples)
- **Testing:** Jest, Pytest, Go testing
- **Deployment:** Docker, Kubernetes

## 📚 Learning Topics

- ✅ Workflow basics and syntax
- ✅ Event triggers (push, pull_request, schedule, manual)
- ✅ Jobs and steps
- ✅ Actions (official and community)
- ✅ Environment variables and secrets
- ✅ Artifacts and caching
- ✅ Matrix builds
- ✅ Conditional execution
- ✅ Deployment workflows
- ✅ Self-hosted runners

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/Marcin4356/gh-first-actions.git
cd gh-first-actions
```

### 2. Explore Workflows

Workflows are located in `.github/workflows/`:

```bash
ls -la .github/workflows/
```

### 3. Create Your First Workflow

```bash
mkdir -p .github/workflows
touch .github/workflows/hello-world.yml
```

### 4. Add Workflow Content

```yaml
name: Hello World

on: push

jobs:
  hello:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - run: echo "Hello, World!"
```

### 5. Commit and Push

```bash
git add .github/workflows/
git commit -m "Add first workflow"
git push
```

## 📁 Project Structure

```
gh-first-actions/
├── .github/
│   └── workflows/
│       ├── hello-world.yml
│       ├── test.yml
│       ├── build.yml
│       ├── deploy.yml
│       ├── schedule.yml
│       ├── matrix-build.yml
│       └── release.yml
├── src/
│   ├── app.js
│   ├── app.py
│   └── main.go
├── tests/
│   ├── app.test.js
│   ├── test_app.py
│   └── app_test.go
├── docker/
│   └── Dockerfile
├── package.json
├── requirements.txt
└── README.md
```

## 📖 Example Workflows

### Basic Trigger (Hello World)

```yaml
name: Hello World
on: push
jobs:
  hello:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Hello, World!"
```

### Testing Workflow

```yaml
name: Test
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: 18
      - run: npm ci
      - run: npm test
```

### Build & Deploy Workflow

```yaml
name: Build & Deploy
on:
  push:
    branches: [main]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: docker/setup-buildx-action@v2
      - uses: docker/login-action@v2
        with:
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}
      - uses: docker/build-push-action@v4
        with:
          push: true
          tags: user/app:latest
```

### Scheduled Workflow

```yaml
name: Scheduled
on:
  schedule:
    - cron: '0 0 * * *'  # Daily at midnight
jobs:
  job:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Scheduled job"
```

### Matrix Build

```yaml
name: Matrix Build
on: push
jobs:
  build:
    runs-on: ${{ matrix.os }}
    strategy:
      matrix:
        os: [ubuntu-latest, macos-latest, windows-latest]
        node-version: [14, 16, 18]
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: ${{ matrix.node-version }}
      - run: npm ci && npm test
```

## 🔐 Secrets Management

### Set Repository Secrets

1. Go to repository Settings
2. Navigate to Secrets and variables → Actions
3. Click "New repository secret"
4. Add secret (e.g., `DOCKER_PASSWORD`)

### Use in Workflow

```yaml
- run: docker login -u ${{ secrets.DOCKER_USERNAME }} -p ${{ secrets.DOCKER_PASSWORD }}
```

## 📊 Common Actions

### Official Actions

- `actions/checkout@v3` - Check out code
- `actions/setup-node@v3` - Setup Node.js
- `actions/setup-python@v4` - Setup Python
- `actions/setup-go@v4` - Setup Go
- `actions/upload-artifact@v3` - Upload artifacts
- `actions/download-artifact@v3` - Download artifacts
- `actions/cache@v3` - Cache dependencies

### Useful Third-party Actions

- `docker/build-push-action` - Build and push Docker
- `actions-rs/toolchain` - Rust toolchain
- `codecov/codecov-action` - Code coverage

## ⚙️ Workflow Syntax

### Events

```yaml
on: push
on: [push, pull_request]
on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]
```

### Jobs & Steps

```yaml
jobs:
  job-id:
    runs-on: ubuntu-latest
    steps:
      - uses: action@v1  # Use an action
      - run: command     # Run a command
      - name: Step name
        run: echo "Named step"
```

### Conditionals

```yaml
- if: github.ref == 'refs/heads/main'
  run: echo "Main branch"

- if: contains(github.event.head_commit.message, '[skip ci]')
  run: echo "Skipping CI"
```

## 📚 Resources

- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [GitHub Actions Marketplace](https://github.com/marketplace?type=actions)
- [Workflow Syntax Reference](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions)
- [GitHub Actions Best Practices](https://docs.github.com/en/actions/guides)

## 🧪 Testing

The repository includes test examples for different languages:

```bash
# JavaScript
npm test

# Python
pytest

# Go
go test ./...
```

## 🤝 Contributing

Feel free to add more examples and workflows!

## 📝 License

This project is open source and available under the MIT License.

## 👤 Author

**Marcin4356** - [GitHub Profile](https://github.com/Marcin4356)

---

*Last updated: 2026-04-28*
