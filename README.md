# CI/CD Cheatsheets (GitLab CI/CD, GitHub Actions)

## **GitLab CI/CD Cheatsheet**

### **GitLab CI/CD Overview**
GitLab CI/CD is a built-in continuous integration and continuous deployment tool in GitLab. It allows you to automate the process of building, testing, and deploying your applications.

### **Defining a `.gitlab-ci.yml` Pipeline**
A GitLab CI/CD pipeline is defined in a `.gitlab-ci.yml` file placed at the root of your repository.
```yaml
stages:
  - build
  - test
  - deploy

build_job:
  stage: build
  script:
    - echo "Building the application"

test_job:
  stage: test
  script:
    - echo "Running tests"

deploy_job:
  stage: deploy
  script:
    - echo "Deploying the application"
```

### **Common GitLab CI/CD Commands**
```sh
gitlab-runner register        # Register a new GitLab Runner
gitlab-runner start           # Start the GitLab Runner
gitlab-runner stop            # Stop the GitLab Runner
gitlab-runner unregister      # Unregister a GitLab Runner
gitlab-runner list            # List all registered GitLab Runners
gitlab-runner verify          # Verify the status of a GitLab Runner
```

### **Artifacts and Caching in GitLab CI/CD**
```yaml
build:
  stage: build
  script:
    - echo "Compiling code"
  artifacts:
    paths:
      - build/
  cache:
    key: build-cache
    paths:
      - .m2/repository/
```

---

## **GitHub Actions Cheatsheet**

### **GitHub Actions Overview**
GitHub Actions allows you to automate workflows for CI/CD directly within GitHub repositories.

### **Defining a Workflow (`.github/workflows/main.yml`)**
Workflows are YAML files defining the automation steps for GitHub Actions.
```yaml
name: CI/CD Pipeline

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v3
      - name: Set up Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '16'
      - name: Install dependencies
        run: npm install
      - name: Build application
        run: npm run build

  test:
    runs-on: ubuntu-latest
    steps:
      - name: Run tests
        run: echo "Running tests"

  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Deploy application
        run: echo "Deploying application"
```

### **Reusable Workflows in GitHub Actions**
Reusable workflows help streamline CI/CD pipelines by allowing modular workflow definitions.
```yaml
name: Reusable Workflow
on:
  workflow_call:
    inputs:
      environment:
        required: true
        type: string
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Deploy to environment
        run: echo "Deploying to ${{ inputs.environment }}"
```

### **GitHub Actions Secrets & Environment Variables**
```yaml
env:
  NODE_ENV: production

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Use Secret
        run: echo "Using a secret: ${{ secrets.MY_SECRET }}"
```

---

## **Useful CI/CD Resources**
- [GitLab CI/CD Docs](https://docs.gitlab.com/ee/ci/)
- [GitHub Actions Docs](https://docs.github.com/en/actions)
- [GitHub Actions Marketplace](https://github.com/marketplace?type=actions)
- [GitLab Runner Docs](https://docs.gitlab.com/runner/)

---

This cheatsheet provides an extensive reference for GitLab CI/CD and GitHub Actions. Let me know if you have any suggestions or improvements!
