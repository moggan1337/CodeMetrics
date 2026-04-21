# CodeMetrics

<div align="center">

![CodeMetrics Logo](https://img.shields.io/badge/CodeMetrics-v2.0.0-blue.svg)
![Python](https://img.shields.io/badge/Python-3.9+-green.svg)
![License](https://img.shields.io/badge/License-MIT-orange.svg)
![Build Status](https://img.shields.io/badge/Build-Passing-brightgreen.svg)
[![Documentation](https://img.shields.io/badge/Documentation-Complete-cyan.svg)](docs/)
[![API Reference](https://img.shields.io/badge/API-Reference-purple.svg)](#api-reference)

**Enterprise-Grade Code Quality & Complexity Analysis Platform**

*Analyze. Measure. Improve. Repeat.*

[Features](#features) • [Quick Start](#quick-start) • [Installation](#installation) • [Usage](#usage) • [API Reference](#api-reference) • [Configuration](#configuration) • [Metrics](#metrics-explained) • [Troubleshooting](#troubleshooting)

</div>

---

## 🎬 Demo
![CodeMetrics Demo](demo.gif)

*Comprehensive code analysis with visual complexity maps*

## Screenshots
| Component | Preview |
|-----------|---------|
| Complexity Map | ![map](screenshots/complexity-map.png) |
| Dependency Graph | ![deps](screenshots/deps-graph.png) |
| Quality Dashboard | ![dashboard](screenshots/quality-dash.png) |

## Visual Description
Complexity maps color-code functions by cyclomatic complexity with size representing line count. Dependency graphs show module relationships as force-directed layouts. Quality dashboards display trend lines for technical debt over time.

---


## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Architecture](#architecture)
- [Supported Languages](#supported-languages)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Usage](#usage)
  - [Command Line Interface](#command-line-interface)
  - [Python API](#python-api)
  - [CI/CD Integration](#cicd-integration)
  - [GitHub Actions](#github-actions)
  - [GitLab CI](#gitlab-ci)
  - [Jenkins](#jenkins)
- [Configuration](#configuration)
  - [Configuration File](#configuration-file)
  - [Environment Variables](#environment-variables)
  - [Command Line Options](#command-line-options)
- [Metrics Explained](#metrics-explained)
  - [Lines of Code (LOC)](#lines-of-code-loc)
  - [Cyclomatic Complexity](#cyclomatic-complexity)
  - [Cognitive Complexity](#cognitive-complexity)
  - [Maintainability Index](#maintainability-index)
  - [Code Duplication](#code-duplication)
  - [Technical Debt](#technical-debt)
  - [Halstead Metrics](#halstead-metrics)
- [API Reference](#api-reference)
  - [Analyzer Class](#analyzer-class)
  - [MetricsCollector Class](#metricscollector-class)
  - [ReportGenerator Class](#reportgenerator-class)
  - [Configuration Class](#configuration-class)
- [Output Formats](#output-formats)
- [Advanced Usage](#advanced-usage)
  - [Incremental Analysis](#incremental-analysis)
  - [Baseline Comparison](#baseline-comparison)
  - [Custom Rules](#custom-rules)
  - [Plugins](#plugins)
- [Troubleshooting](#troubleshooting)
  - [Common Issues](#common-issues)
  - [FAQ](#faq)
  - [Debug Mode](#debug-mode)
- [Contributing](#contributing)
- [Changelog](#changelog)
- [License](#license)
- [Support](#support)

---

## Overview

CodeMetrics is a comprehensive, enterprise-grade code quality and complexity analysis platform designed to help development teams measure, monitor, and improve their codebase quality over time. Built with scalability and extensibility in mind, CodeMetrics supports multiple programming languages and provides actionable insights through detailed metrics analysis.

### Why CodeMetrics?

- **Comprehensive Analysis**: From simple line counts to advanced cognitive complexity metrics
- **Multi-Language Support**: Analyze projects written in various programming languages
- **CI/CD Ready**: Seamlessly integrate into your existing continuous integration pipelines
- **Extensible Architecture**: Add custom rules, plugins, and reporters
- **Historical Tracking**: Track metrics over time to identify trends
- **Actionable Reports**: Get clear, actionable recommendations for improvement
- **Performance Optimized**: Fast analysis with incremental support for large codebases

---

## Features

### Core Features

| Feature | Description |
|---------|-------------|
| **Lines of Code (LOC)** | Accurate code, comment, and blank line counting |
| **Cyclomatic Complexity** | McCabe complexity measurement for all functions/methods |
| **Cognitive Complexity** | Cognitive load measurement beyond traditional complexity |
| **Maintainability Index** | Composite score predicting maintainability |
| **Code Duplication** | Detection of duplicate and similar code blocks |
| **Technical Debt** | Estimation of refactoring effort required |
| **Halstead Metrics** | Program difficulty, volume, and effort metrics |
| **Dependency Analysis** | Module and package dependency tracking |

### Advanced Features

- **Incremental Analysis**: Only analyze changed files for faster feedback
- **Baseline Comparison**: Compare current metrics against historical baselines
- **Quality Gates**: Set thresholds and fail builds when exceeded
- **Multiple Output Formats**: JSON, XML, HTML, Markdown, and SARIF
- **Custom Rules Engine**: Define project-specific quality rules
- **Plugin System**: Extend functionality with custom plugins
- **Web Dashboard**: Visualize metrics with interactive charts
- **API Server**: REST API for programmatic access

---

## Architecture

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                              CodeMetrics Architecture                        │
└─────────────────────────────────────────────────────────────────────────────┘

                              ┌─────────────────────┐
                              │     Entry Points     │
                              │  ┌─────────────────┐ │
                              │  │   CLI Interface │ │
                              │  └────────┬────────┘ │
                              │  ┌────────┴────────┐ │
                              │  │   Python API    │ │
                              │  └────────┬────────┘ │
                              │  ┌────────┴────────┐ │
                              │  │   REST API      │ │
                              │  └────────┬────────┘ │
                              └───────────┬──────────┘
                                          │
                    ┌─────────────────────┼─────────────────────┐
                    │                     │                     │
                    ▼                     ▼                     ▼
        ┌───────────────────┐ ┌───────────────────┐ ┌───────────────────┐
        │    Core Engine    │ │   Config Manager  │ │   Report Engine   │
        │  ┌─────────────┐  │ │  ┌─────────────┐  │ │  ┌─────────────┐  │
        │  │   Parser    │  │ │  │    YAML     │  │ │  │   JSON      │  │
        │  │   Manager   │  │ │  │   Parser    │  │ │  │   Writer    │  │
        │  └─────────────┘  │ │  └─────────────┘  │ │  └─────────────┘  │
        │  ┌─────────────┐  │ │  ┌─────────────┐  │ │  ┌─────────────┐  │
        │  │   Metric    │◄─┼─┼──│   Loader    │  │ │  │   HTML      │  │
        │  │  Calculator │  │ │  │             │  │ │  │   Writer    │  │
        │  └─────────────┘  │ │  └─────────────┘  │ │  └─────────────┘  │
        │  ┌─────────────┐  │ │  ┌─────────────┐  │ │  ┌─────────────┐  │
        │  │   Rule     │  │ │  │   Env       │  │ │  │   Markdown  │  │
        │  │   Engine   │  │ │  │   Variables │  │ │  │   Writer    │  │
        │  └─────────────┘  │ │  └─────────────┘  │ │  └─────────────┘  │
        │  ┌─────────────┐  │ │  ┌─────────────┐  │ │  ┌─────────────┐  │
        │  │   Cache    │  │ │  │   Defaults  │  │ │  │   XML       │  │
        │  │   Manager  │  │ │  │             │  │ │  │   Writer    │  │
        │  └─────────────┘  │ │  └─────────────┘  │ │  └─────────────┘  │
        └─────────┬─────────┘ └───────────────────┘ └───────────────────┘
                  │
    ┌─────────────┼─────────────┬─────────────┬─────────────┐
    │             │             │             │             │
    ▼             ▼             ▼             ▼             ▼
┌────────┐  ┌────────┐  ┌────────┐  ┌────────┐  ┌────────┐
│ Python │  │   Go   │  │JavaScript│ │  Java  │  │   C/C++│
│ Parser │  │ Parser │  │ Parser  │  │ Parser │  │ Parser │
└────────┘  └────────┘  └────────┘  └────────┘  └────────┘
    │             │             │             │             │
    └─────────────┴─────────────┼─────────────┴─────────────┘
                                │
                                ▼
                    ┌───────────────────────┐
                    │   Metrics Database   │
                    │  ┌─────────────────┐  │
                    │  │  SQLite/JSON   │  │
                    │  │   Storage       │  │
                    │  └─────────────────┘  │
                    │  ┌─────────────────┐  │
                    │  │  Trend Analysis │  │
                    │  │    Engine       │  │
                    │  └─────────────────┘  │
                    └───────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────┐
│                         Language-Specific Parsers                           │
├─────────────────────────────────────────────────────────────────────────────┤
│  Python  │  JavaScript  │    TypeScript   │    Java     │     Go          │
│  ──────  │  ─────────  │   ──────────    │   ─────     │    ───          │
│  AST解析  │  Babel解析   │   TSCompiler   │  javac解析  │  go/parser      │
│  ├─函数   │  ├─函数      │   ├─函数        │  ├─方法      │  ├─函数         │
│  ├─类    │  ├─类       │   ├─类          │  ├─类       │  ├─类型         │
│  ├─模块   │  ├─模块      │   ├─接口        │  ├─包       │  ├─包          │
│  └─装饰器  │  └─导出      │   └─类型        │  └─注解     │  └─接口         │
├─────────────────────────────────────────────────────────────────────────────┤
│  Ruby    │   C/C++      │     C#          │   Rust      │   PHP          │
│  ──────  │   ─────      │     ──          │   ────      │   ───          │
│  Parser  │   Clang      │   Roslyn        │   rustc     │   PHP-Parser   │
│  ├─方法   │   ├─函数     │   ├─方法        │   ├─函数     │   ├─函数        │
│  ├─类    │   ├─结构体   │   ├─类          │   ├─结构体  │   ├─类         │
│  ├─模块   │   └─宏      │   └─命名空间    │   └─Trait  │   └─命名空间   │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Component Descriptions

| Component | Purpose |
|-----------|---------|
| **CLI Interface** | Command-line tool for quick analysis |
| **Python API** | Programmatic access for custom integrations |
| **REST API** | HTTP-based access for web applications |
| **Parser Manager** | Orchestrates language-specific parsers |
| **Metric Calculator** | Computes all supported metrics |
| **Rule Engine** | Evaluates code against defined rules |
| **Cache Manager** | Stores results for incremental analysis |
| **Config Manager** | Loads and validates configurations |
| **Report Engine** | Generates output in various formats |

---

## Supported Languages

CodeMetrics supports the following programming languages out of the box:

| Language | Version Support | Parser | Extensions |
|----------|-----------------|--------|------------|
| **Python** | 2.7, 3.6 - 3.12 | `ast` module | `.py`, `.pyw`, `.pyi` |
| **JavaScript** | ES5 - ES2024 | Babel AST | `.js`, `.jsx`, `.mjs`, `.cjs` |
| **TypeScript** | 4.0 - 5.5 | TypeScript Compiler | `.ts`, `.tsx` |
| **Java** | 8 - 21 | javac + ANTLR | `.java` |
| **Go** | 1.14 - 1.22 | go/parser | `.go` |
| **C** | C89 - C23 | Clang | `.c`, `.h` |
| **C++** | C++11 - C++23 | Clang | `.cpp`, `.cc`, `.cxx`, `.hpp`, `.hxx` |
| **C#** | .NET 6+ | Roslyn | `.cs` |
| **Ruby** | 2.7 - 3.3 | Parser gem | `.rb` |
| **PHP** | 7.4 - 8.3 | PHP-Parser | `.php` |
| **Rust** | 1.70+ | rustc_ast | `.rs` |
| **Swift** | 5.0 - 5.9 | SwiftParser | `.swift` |
| **Kotlin** | 1.6 - 1.9 | kotlin-compiler | `.kt`, `.kts` |
| **Scala** | 2.13 - 3.3 | scalameta | `.scala` |
| **Shell/Bash** | Bash 4+ | bash-parser | `.sh`, `.bash` |

### Language-Specific Features Matrix

| Language | LOC | Complexity | Maintainability | Duplication | Dependencies |
|----------|-----|------------|-----------------|-------------|--------------|
| Python | ✅ | ✅ | ✅ | ✅ | ✅ |
| JavaScript | ✅ | ✅ | ✅ | ✅ | ✅ |
| TypeScript | ✅ | ✅ | ✅ | ✅ | ✅ |
| Java | ✅ | ✅ | ✅ | ✅ | ✅ |
| Go | ✅ | ✅ | ✅ | ✅ | ✅ |
| C | ✅ | ✅ | ✅ | ✅ | ❌ |
| C++ | ✅ | ✅ | ✅ | ✅ | ❌ |
| C# | ✅ | ✅ | ✅ | ✅ | ✅ |
| Ruby | ✅ | ✅ | ✅ | ✅ | ✅ |
| PHP | ✅ | ✅ | ✅ | ✅ | ✅ |
| Rust | ✅ | ✅ | ✅ | ✅ | ✅ |
| Swift | ✅ | ✅ | ✅ | ✅ | ✅ |
| Kotlin | ✅ | ✅ | ✅ | ✅ | ✅ |
| Scala | ✅ | ✅ | ✅ | ✅ | ✅ |
| Shell | ✅ | ✅ | ✅ | ❌ | ❌ |

---

## Installation

### Prerequisites

- **Python**: 3.9 or higher
- **pip**: Latest version recommended
- **Operating System**: macOS, Linux, Windows (WSL recommended)

### Standard Installation

```bash
# Install from PyPI (when published)
pip install codemetrics

# Or install the latest development version
pip install git+https://github.com/moggan1337/CodeMetrics.git

# With all optional dependencies
pip install codemetrics[all]
```

### Development Installation

```bash
# Clone the repository
git clone https://github.com/moggan1337/CodeMetrics.git
cd CodeMetrics

# Create a virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install in development mode with all dependencies
pip install -e ".[dev,all]"

# Run tests to verify installation
pytest tests/
```

### Docker Installation

```bash
# Pull the official image
docker pull codemetrics/codemetrics:latest

# Run analysis
docker run --rm -v $(pwd):/workspace codemetrics analyze /workspace

# Or use Docker Compose
cat > docker-compose.yml << 'EOF'
version: '3.8'
services:
  codemetrics:
    image: codemetrics/codemetrics:latest
    volumes:
      - .:/workspace
    command: analyze /workspace --format html --output report.html
EOF

docker-compose up
```

### Verifying Installation

```bash
# Check version
codemetrics --version

# Display help
codemetrics --help

# Run a test analysis
codemetrics analyze . --quick
```

---

## Quick Start

### 5-Minute Tutorial

```bash
# 1. Navigate to your project
cd ~/projects/my-app

# 2. Run a quick analysis
codemetrics analyze . --quick

# 3. Generate an HTML report
codemetrics analyze . --format html --output report.html

# 4. View the report
open report.html

# 5. Check for issues
codemetrics analyze . --fail-on-warnings
```

### Expected Output

```
╔══════════════════════════════════════════════════════════════════════════════╗
║                           CodeMetrics Analysis Report                        ║
╠══════════════════════════════════════════════════════════════════════════════╣
║ Project: my-app                               Date: 2024-04-20 14:30:00      ║
╠══════════════════════════════════════════════════════════════════════════════╣
║ METRICS SUMMARY                                                              ║
║ ─────────────────────────────────────────────────────────────────────────── ║
║  Total Files          │ 142                                                  ║
║  Lines of Code        │ 12,847                                               ║
║  Comment Lines        │ 3,291  (20.4%)                                        ║
║  Blank Lines          │ 1,928  (15.0%)                                        ║
║  Cyclomatic Complexity│ 3.42 avg │ 48 max                                     ║
║  Cognitive Complexity│ 2.18 avg │ 32 max                                     ║
║  Maintainability Index│ 78.5 (Good)                                           ║
║  Technical Debt       │ 4.2 days                                             ║
╠══════════════════════════════════════════════════════════════════════════════╣
║  ⚠️  3 files exceed complexity threshold (CC > 15)                           ║
║  ⚠️  2 duplicate code blocks detected                                        ║
║  ℹ️   Overall grade: B (80/100)                                               ║
╚══════════════════════════════════════════════════════════════════════════════╝
```

---

## Usage

### Command Line Interface

#### Basic Commands

```bash
# Analyze current directory
codemetrics analyze .

# Analyze specific directory
codemetrics analyze ./src

# Analyze multiple directories
codemetrics analyze ./src ./tests

# Analyze with all metrics
codemetrics analyze . --full

# Quick analysis (fewer metrics, faster)
codemetrics analyze . --quick
```

#### Output Options

```bash
# JSON output
codemetrics analyze . --format json --output metrics.json

# HTML report
codemetrics analyze . --format html --output report.html

# XML output (JUnit compatible)
codemetrics analyze . --format xml --output results.xml

# Markdown report
codemetrics analyze . --format markdown --output report.md

# SARIF format (for GitHub code scanning)
codemetrics analyze . --format sarif --output results.sarif

# Console output with colors
codemetrics analyze . --format console --no-ansi

# Multiple output formats
codemetrics analyze . --format json,html --output metrics.json --output-dir ./reports
```

#### Filtering and Focus

```bash
# Analyze only Python files
codemetrics analyze . --language python

# Exclude test files
codemetrics analyze . --exclude "**/*test*.py" --exclude "**/tests/*"

# Focus on specific modules
codemetrics analyze . --include "src/core/*"

# Set minimum file size
codemetrics analyze . --min-lines 10

# Maximum depth
codemetrics analyze . --max-depth 5
```

#### Threshold and Quality Gates

```bash
# Set complexity threshold
codemetrics analyze . --max-complexity 15

# Set maintainability threshold
codemetrics analyze . --min-maintainability 70

# Fail on warnings
codemetrics analyze . --fail-on-warnings

# Fail on errors only
codemetrics analyze . --fail-on-errors

# Set exit code based on grade
codemetrics analyze . --min-grade C
```

#### Incremental Analysis

```bash
# Use cached results for unchanged files
codemetrics analyze . --incremental

# Force full analysis ignoring cache
codemetrics analyze . --no-cache

# Clear cache before analysis
codemetrics analyze . --clear-cache

# Specify cache directory
codemetrics analyze . --cache-dir ./.codemetrics-cache
```

#### Comparison and Baselines

```bash
# Compare with baseline
codemetrics analyze . --compare-with baseline.json

# Generate new baseline
codemetrics analyze . --save-baseline baseline.json

# Show only changed metrics
codemetrics analyze . --show-diff

# Set tolerance for changes
codemetrics analyze . --tolerance 5%
```

### Python API

#### Basic Usage

```python
from codemetrics import Analyzer, Configuration

# Create analyzer with default settings
analyzer = Analyzer()
results = analyzer.analyze('./src')

# Access metrics
print(f"LOC: {results.loc.total}")
print(f"Complexity: {results.complexity.average}")
print(f"Maintainability: {results.maintainability.score}")

# Generate report
report = results.generate_report(format='html')
with open('report.html', 'w') as f:
    f.write(report)
```

#### Advanced Configuration

```python
from codemetrics import Analyzer, Configuration, MetricType
from pathlib import Path

# Create custom configuration
config = Configuration()
config.max_complexity = 10
config.min_maintainability = 75
config.exclude_patterns = ['**/test_*.py', '**/*_test.py']
config.include_patterns = ['src/**/*.py']
config.languages = ['python']
config.thresholds = {
    'cyclomatic_complexity': {'warning': 10, 'error': 20},
    'cognitive_complexity': {'warning': 8, 'error': 15},
    'maintainability_index': {'warning': 70, 'error': 50},
    'loc': {'warning': 500, 'error': 1000}
}

# Create analyzer with custom config
analyzer = Analyzer(config=config)
results = analyzer.analyze(
    path='./src',
    incremental=True,
    verbose=True
)

# Process results
for file_result in results.files:
    print(f"{file_result.path}: CC={file_result.complexity.cyclomatic}")
    for issue in file_result.issues:
        print(f"  - {issue.severity}: {issue.message}")
```

#### Detailed Metrics Access

```python
from codemetrics import Analyzer, MetricType

analyzer = Analyzer()
results = analyzer.analyze('./src')

# Per-file metrics
for file in results.files:
    print(f"\n=== {file.path} ===")
    print(f"  LOC: {file.loc.code}")
    print(f"  Functions: {len(file.functions)}")
    print(f"  Classes: {len(file.classes)}")
    
    # Function-level metrics
    for func in file.functions:
        print(f"    {func.name}: CC={func.cyclomatic_complexity}, "
              f"Cog={func.cognitive_complexity}")

# Summary statistics
print("\n=== Summary ===")
print(f"Total Files: {results.summary.file_count}")
print(f"Total LOC: {results.summary.loc}")
print(f"Average Complexity: {results.summary.avg_complexity}")
print(f"Total Technical Debt: {results.summary.technical_debt}")
print(f"Quality Grade: {results.summary.grade}")
```

#### Custom Report Generation

```python
from codemetrics import Analyzer, ReportGenerator
from jinja2 import Template

# Create custom report generator
template = """
# Code Analysis Report

**Project:** {{ project_name }}
**Date:** {{ analysis_date }}
**Grade:** {{ grade }}

## Summary

| Metric | Value |
|--------|-------|
| Files | {{ file_count }} |
| LOC | {{ loc }} |
| Avg Complexity | {{ avg_complexity }} |
| Maintainability | {{ maintainability }} |

## High Complexity Functions

{% for func in high_complexity_functions %}
- {{ func.name }} ({{ func.file }}): CC={{ func.cyclomatic }}
{% endfor %}
"""

generator = ReportGenerator(template=template)
report = generator.generate(results)

with open('custom_report.md', 'w') as f:
    f.write(report)
```

#### Incremental Analysis with Change Detection

```python
from codemetrics import Analyzer
from git import Repo

# Get list of changed files
repo = Repo('.')
changed_files = [item.a_path for item in repo.index.diff(None)]
changed_files += [item.a_path for item in repo.index.diff('HEAD')]

# Run incremental analysis
analyzer = Analyzer()
results = analyzer.analyze(
    './src',
    incremental=True,
    changed_files=changed_files
)

# Process only changed files
for file_result in results.changed_files:
    print(f"Changed: {file_result.path}")
    print(f"  New issues: {len(file_result.new_issues)}")
```

### CI/CD Integration

#### GitHub Actions

```yaml
# .github/workflows/code-analysis.yml
name: Code Quality Analysis

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

jobs:
  analyze:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        
      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.11'
          
      - name: Install CodeMetrics
        run: pip install codemetrics
        
      - name: Run Analysis
        run: |
          codemetrics analyze . \
            --format sarif \
            --output codemetrics.sarif \
            --fail-on-warnings
            
      - name: Upload SARIF results
        uses: github/codeql-action/upload-sarif@v3
        with:
          sarif_file: codemetrics.sarif
          
      - name: Generate HTML Report
        if: always()
        run: |
          codemetrics analyze . \
            --format html \
            --output codemetrics-report.html
            
      - name: Upload Report
        uses: actions/upload-artifact@v4
        if: always()
        with:
          name: code-metrics-report
          path: codemetrics-report.html
```

#### GitLab CI

```yaml
# .gitlab-ci.yml
variables:
  PIP_CACHE_DIR: "$CI_PROJECT_DIR/.cache/pip"

cache:
  paths:
    - .cache/pip/

code_analysis:
  image: python:3.11-slim
  before_script:
    - pip install codemetrics
  script:
    - codemetrics analyze . --format json --output metrics.json
    - codemetrics analyze . --format html --output report.html
  artifacts:
    reports:
      junit: metrics.json
    paths:
      - report.html
    expire_in: 1 week
  rules:
    - if: $CI_PIPELINE_SOURCE == "merge_request_event"
    - if: $CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH
```

#### Jenkins

```groovy
// Jenkinsfile
pipeline {
    agent any
    
    environment {
        CODEMETRICS_THRESHOLD = '15'
    }
    
    stages {
        stage('Code Analysis') {
            steps {
                sh '''
                    python -m venv venv
                    . venv/bin/activate
                    pip install codemetrics
                    codemetrics analyze . \
                        --format json \
                        --output metrics.json \
                        --max-complexity ${CODEMETRICS_THRESHOLD}
                '''
            }
        }
        
        stage('Publish Results') {
            steps {
                recordIssues(
                    enabledForFailure: true,
                    tools: [pyLint()],
                    qualityGates: [[threshold: 15, type: 'COMPLEXITY', unstable: true]]
                )
                
                publishHTML([
                    allowMissing: false,
                    alwaysLinkToLastBuild: true,
                    keepAll: true,
                    reportDir: '.',
                    reportFiles: 'report.html',
                    reportName: 'CodeMetrics Report'
                ])
            }
        }
    }
    
    post {
        always {
            cleanWs()
        }
    }
}
```

#### Travis CI

```yaml
# .travis.yml
language: python
python:
  - "3.11"

install:
  - pip install codemetrics

script:
  - codemetrics analyze . --format json --output metrics.json

after_success:
  - codemetrics analyze . --format html --output report.html
  - pip install codeclimate-test-reporter
  - codeclimate-test-reporter < coverage/lcov.info

notifications:
  email:
    on_success: change
    on_failure: always
```

#### Azure DevOps

```yaml
# azure-pipelines.yml
trigger:
  - main
  - develop

pool:
  vmImage: 'ubuntu-latest'

steps:
  - task: UsePythonVersion@0
    displayName: 'Use Python 3.11'
    inputs:
      versionSpec: '3.11'
      
  - script: |
      pip install codemetrics
      codemetrics analyze . --format json --output metrics.json
      codemetrics analyze . --format html --output report.html
    displayName: 'Run CodeMetrics Analysis'

  - task: PublishBuildArtifacts@1
    displayName: 'Publish HTML Report'
    inputs:
      pathtoPublish: 'report.html'
      artifactName: 'CodeMetrics Report'

  - task: PublishCodeCoverageResults@2
    displayName: 'Publish Code Coverage'
    inputs:
      codeCoverageTool: 'Cobertura'
      summaryFileLocation: 'metrics.json'
```

---

## Configuration

### Configuration File

Create a `codemetrics.yml` or `codemetrics.yaml` file in your project root:

```yaml
# codemetrics.yml - CodeMetrics Configuration

# Project Information
project:
  name: "My Project"
  version: "1.0.0"
  description: "Project description for reports"

# Analysis Settings
analysis:
  # Directories to analyze
  paths:
    - ./src
    - ./lib
    
  # File patterns to include
  include:
    - "**/*.py"
    - "**/*.js"
    
  # File patterns to exclude
  exclude:
    - "**/test*.py"
    - "**/*_test.py"
    - "**/__pycache__/**"
    - "**/node_modules/**"
    - "**/.venv/**"
    - "**/dist/**"
    - "**/build/**"
    - "**/*.min.js"
    
  # Minimum file size (lines) to analyze
  min_file_lines: 3
  
  # Maximum file depth to traverse
  max_depth: 10
  
  # Languages to analyze (auto-detect if empty)
  languages: []
  
# Metric Thresholds
thresholds:
  # Cyclomatic Complexity
  cyclomatic_complexity:
    warning: 10
    error: 20
    critical: 30
    
  # Cognitive Complexity  
  cognitive_complexity:
    warning: 8
    error: 15
    critical: 25
    
  # Lines of Code per file
  loc:
    warning: 500
    error: 1000
    
  # Lines of Code per function
  loc_per_function:
    warning: 50
    error: 100
    
  # Maintainability Index (0-100, higher is better)
  maintainability_index:
    warning: 65
    error: 50
    
  # Technical Debt (in minutes)
  technical_debt:
    warning: 480  # 8 hours
    error: 1440   # 1 day
    
  # Duplication percentage
  duplication:
    warning: 5    # 5%
    error: 10
    
  # Comment ratio (comments / total lines)
  comment_ratio:
    warning: 0.1  # 10%
    error: 0.05   # 5%

# Quality Gates
quality_gates:
  # Fail build if any threshold exceeded
  fail_on_warning: false
  fail_on_error: true
  fail_on_critical: true
  
  # Minimum grade to pass (A, B, C, D, F)
  min_grade: "C"
  
  # Exit with error code
  exit_code_on_fail: true

# Output Settings
output:
  # Default format (console, json, html, xml, markdown, sarif)
  format: "console"
  
  # Output file path
  output_file: null
  
  # Output directory for multiple formats
  output_dir: "./reports"
  
  # Console output options
  console:
    color: true
    emoji: true
    verbosity: "normal"  # quiet, normal, verbose, debug
    
  # JSON output options
  json:
    pretty: true
    indent: 2
    include_raw_data: false
    
  # HTML report options
  html:
    theme: "default"  # default, dark, minimal
    include_charts: true
    include_source: false

# Caching
cache:
  # Enable incremental analysis
  enabled: true
  
  # Cache directory
  directory: ".codemetrics-cache"
  
  # Cache expiration (days)
  expiration: 7
  
  # Clear cache before analysis
  clear_on_run: false

# Baseline Comparison
baseline:
  # Enable baseline comparison
  enabled: false
  
  # Baseline file path
  file: ".codemetrics-baseline.json"
  
  # Tolerance for changes (percentage)
  tolerance: 5
  
  # Show improvements as positive
  show_improvements: true

# Rules Engine
rules:
  # Enable/disable specific rules
  enabled:
    - complexity
    - maintainability
    - duplication
    - dependencies
    - naming
    - documentation
    
  # Custom rules
  custom:
    - name: "no-goto"
      pattern: "\\bgoto\\b"
      severity: "warning"
      languages: ["python"]
      
    - name: "magic-numbers"
      pattern: "\\b\\d{3,}\\b"
      severity: "info"
      exclude: ["version", "port", "timeout"]

# Plugins
plugins:
  - name: "security-scanner"
    enabled: true
    options:
      severity_threshold: "high"
```

### Environment Variables

```bash
# Core Settings
export CODEMETRICS_CONFIG=".codemetrics.yml"
export CODEMETRICS_OUTPUT_DIR="./reports"
export CODEMETRICS_CACHE_DIR=".codemetrics-cache"

# Thresholds
export CODEMETRICS_MAX_COMPLEXITY="15"
export CODEMETRICS_MIN_MAINTAINABILITY="70"
export CODEMETRICS_MAX_LOC="1000"

# Output
export CODEMETRICS_FORMAT="json"
export CODEMETRICS_OUTPUT="metrics.json"
export CODEMETRICS_NO_COLOR="false"

# Analysis
export CODEMETRICS_INCREMENTAL="true"
export CODEMETRICS_FAIL_ON_WARNING="false"
export CODEMETRICS_LANGUAGES="python,javascript"

# API Server
export CODEMETRICS_API_HOST="0.0.0.0"
export CODEMETRICS_API_PORT="8080"
export CODEMETRICS_API_KEY="your-secret-key"

# Debugging
export CODEMETRICS_DEBUG="false"
export CODEMETRICS_TRACE="false"
export CODEMETRICS_LOG_LEVEL="INFO"
```

### Command Line Options

```
Usage: codemetrics [OPTIONS] COMMAND [ARGS]...

CodeMetrics - Enterprise Code Quality and Complexity Analysis

╭─ Options ───────────────────────────────────────────────────────────────────╮
│ --version          Show version and exit                                    │
│ --help             Show this message and exit                               │
│ --config PATH      Configuration file path                                  │
│ --verbose          Enable verbose output                                    │
│ --quiet            Suppress all output except errors                         │
│ --debug            Enable debug mode                                        │
╰─────────────────────────────────────────────────────────────────────────────╯

╭─ Commands ──────────────────────────────────────────────────────────────────╮
│ analyze    Analyze code and generate metrics                                │
│ baseline   Manage analysis baselines                                        │
│ compare    Compare two analysis results                                     │
│ report     Generate custom reports                                          │
│ serve      Start the API server                                             │
│ config     Configuration management                                          │
│ init       Initialize CodeMetrics in a project                              │
│ validate   Validate configuration file                                       │
╰─────────────────────────────────────────────────────────────────────────────╯

analyze:
  codemetrics analyze PATH [PATH...] [OPTIONS]
  
  Analyze directories or files for code metrics.
  
  ╭─ Analysis Options ────────────────────────────────────────────────────────╮
  │ --quick               Quick analysis mode (fewer metrics)                │
  │ --full                Full analysis (all metrics)                         │
  │ --language, -l         Filter by language (can be repeated)                │
  │ --include PATTERN      Include pattern (can be repeated)                   │
  │ --exclude PATTERN      Exclude pattern (can be repeated)                  │
  │ --min-lines N          Minimum file size to analyze                       │
  │ --max-depth N          Maximum directory depth                             │
  ╰─────────────────────────────────────────────────────────────────────────────╯
  
  ╭─ Output Options ──────────────────────────────────────────────────────────╮
  │ --format, -f           Output format (console, json, html, xml, md, sarif)│
  │ --output, -o           Output file path                                    │
  │ --output-dir           Output directory for multiple files                 │
  │ --no-ansi              Disable ANSI colors                                │
  │ --show-issues          Show detailed issue list                            │
  ╰─────────────────────────────────────────────────────────────────────────────╯
  
  ╭─ Threshold Options ───────────────────────────────────────────────────────╮
  │ --max-complexity N     Maximum cyclomatic complexity                       │
  │ --min-maintainability  Minimum maintainability index                        │
  │ --max-loc N            Maximum lines per file                              │
  │ --min-grade GRADE      Minimum acceptable grade (A-F)                      │
  ╰─────────────────────────────────────────────────────────────────────────────╯
  
  ╭─ Quality Gate Options ─────────────────────────────────────────────────────╮
  │ --fail-on-warnings     Exit with error if warnings found                  │
  │ --fail-on-errors        Exit with error if errors found                    │
  │ --strict                Enable strict mode (fail on any threshold breach) │
  ╰─────────────────────────────────────────────────────────────────────────────╯
  
  ╭─ Cache Options ─────────────────────────────────────────────────────────────╮
  │ --[no-]incremental     Use incremental analysis                            │
  │ --clear-cache          Clear cache before analysis                         │
  │ --cache-dir DIR        Cache directory                                     │
  ╰─────────────────────────────────────────────────────────────────────────────╯
  
  ╭─ Comparison Options ───────────────────────────────────────────────────────╮
  │ --compare-with FILE    Compare with baseline file                          │
  │ --save-baseline FILE   Save results as baseline                            │
  │ --show-diff            Show only changed metrics                           │
  │ --tolerance N%         Tolerance for change detection                      │
  ╰─────────────────────────────────────────────────────────────────────────────╯

baseline:
  codemetrics baseline [ACTION] [OPTIONS]
  
  Manage analysis baselines.
  
  Actions:
    create    Create a new baseline from current analysis
    update    Update existing baseline
    delete    Delete a baseline
    list      List all baselines
    diff      Show changes from baseline

report:
  codemetrics report [OPTIONS]
  
  Generate custom reports from saved analysis results.
  
  ╭─ Options ──────────────────────────────────────────────────────────────────╮
  │ --input FILE           Input analysis results (JSON)                      │
  │ --template FILE        Custom report template                              │
  │ --format FORMAT        Output format                                      │
  │ --output FILE          Output file                                        │
  ╰─────────────────────────────────────────────────────────────────────────────╯

serve:
  codemetrics serve [OPTIONS]
  
  Start the CodeMetrics API server.
  
  ╭─ Options ──────────────────────────────────────────────────────────────────╮
  │ --host ADDRESS         Server host (default: 0.0.0.0)                      │
  │ --port PORT            Server port (default: 8080)                         │
  │ --api-key KEY          API authentication key                              │
  │ --workers N            Number of worker processes                          │
  ╰─────────────────────────────────────────────────────────────────────────────╯

config:
  codemetrics config [ACTION] [OPTIONS]
  
  Configuration management.
  
  Actions:
    init      Create new configuration file
    validate  Validate configuration file
    show      Show current effective configuration
    edit      Open configuration in editor
```

---

## Metrics Explained

### Lines of Code (LOC)

Lines of Code is the most fundamental metric, counting various types of lines in source files.

#### Types of Lines Counted

| Type | Description | Purpose |
|------|-------------|---------|
| **Physical Lines** | Every line in a file | Total file size |
| **Code Lines** | Lines containing executable code | Actual implementation |
| **Comment Lines** | Lines with comments | Documentation coverage |
| **Blank Lines** | Empty lines | Formatting/organization |
| **Logical LOC** | Statements (language-specific) | True code measurement |

#### Code Line Calculation by Language

```python
# Python: One logical LOC per statement
def foo():
    x = 1           # 1 LOC
    y = 2           # 1 LOC
    return x + y    # 1 LOC
# Total: 3 logical LOC

# JavaScript: One logical LOC per semicolon-terminated statement
const x = 1;        // 1 LOC
const y = 2;        // 1 LOC
// Total: 2 logical LOC

# C: Includes preprocessor directives
#define MAX 100    // 1 LOC
int main() {        // 1 LOC
    return 0;       // 1 LOC
}                   // Total: 3 logical LOC
```

#### LOC Thresholds

| LOC/File | Rating | Action |
|----------|--------|--------|
| < 200 | Excellent | No action needed |
| 200-500 | Good | Monitor |
| 500-1000 | Warning | Consider refactoring |
| > 1000 | Critical | Refactor required |

### Cyclomatic Complexity

Cyclomatic Complexity (CC) measures the number of linearly independent paths through a program.

#### Calculation Formula

```
CC = E - N + 2P
Where:
  E = Number of edges in the graph
  N = Number of nodes in the graph
  P = Number of connected components (usually 1)
```

#### Simplified Calculation

```
CC = Number of decision points + 1
```

#### Decision Points That Increase Complexity

| Construct | Complexity Added |
|-----------|------------------|
| `if` | +1 |
| `elif` | +1 |
| `else` | +0 |
| `for` | +1 |
| `while` | +1 |
| `case` (each branch) | +1 |
| `catch` (each) | +1 |
| `&&` / `\|\|` | +1 |
| Ternary `?:` | +1 |
| Function call | +0 |

#### Example

```python
# Complexity = 4 (if=1, for=1, &&=1, return=0)
def process(user, items):
    if user.is_active and user.has_permission:  # +2 (if + &&)
        for item in items:                      # +1
            if item.is_valid:                   # +1
                item.process()
        return True                             # +0
    return False                                # +0
```

#### Complexity Ratings

| CC Range | Rating | Risk Level |
|----------|--------|------------|
| 1-10 | Low | Low risk, simple code |
| 11-20 | Moderate | Medium risk, moderate code |
| 21-50 | High | High risk, complex code |
| 51-100 | Very High | Very high risk |
| > 100 | Extremely High | Untestable, should be refactored |

### Cognitive Complexity

Cognitive Complexity measures how difficult code is to understand, accounting for human reading patterns.

#### Scoring Rules

```
1. Code Structure Penalties
   - Nesting penalty: +1 per nesting level
   - Structural penalty: +1 for each breaking flow structure

2. Hybrid Structures
   - Mix of structures: Additional +1 for each type
   - Recursion: +2 per level

3. Cognitive Patterns
   - Indirect recursion: Additional +1
   - Tail recursion: +0
```

#### Key Differences from Cyclomatic Complexity

| Aspect | Cyclomatic | Cognitive |
|--------|------------|-----------|
| Counts loops | Yes | Yes |
| Counts recursion | Yes | Yes |
| Penalizes nesting | No | Yes |
| Penalizes switch cases | Yes | Yes |
| Penalizes if chains | No | Yes |
| Measures readability | No | Yes |

#### Example Comparison

```python
# Cyclomatic: 4, Cognitive: 6
if condition1:           # Nesting 0, Structure 1
    if condition2:        # Nesting 1, Structure 1
        if condition3:    # Nesting 2, Structure 1
            if condition4: # Nesting 3, Structure 1
                do_something()
                
# Cyclomatic: 4, Cognitive: 2 (flat structure)
if condition1 and condition2 and condition3 and condition4:
    do_something()
```

### Maintainability Index

The Maintainability Index (MI) is a composite metric predicting how maintainable code is.

#### Formula

```
MI = 171 - 5.2 * ln(avgLOC) - 0.23 * avgComplexity - 16.2 * ln(avgVolume) + 50 * sin(sqrt(2.4 * percentComments))
```

#### Simplified Version

```
MI = MAX(0, (171 - 5.2 * ln(HALSTEAD_VOLUME) - 0.23 * CC - 16.2 * ln(LOC) + 50 * sin(sqrt(2.46 * COMMENT_RATIO))) * 100 / 171)
```

#### Rating Scale

| MI Range | Color | Rating | Interpretation |
|----------|-------|--------|----------------|
| 100-80 | Green | Excellent | Highly maintainable |
| 79-70 | Yellow | Good | Moderately maintainable |
| 69-60 | Orange | Fair | Somewhat difficult |
| 59-40 | Red | Poor | Difficult to maintain |
| 39-0 | Dark Red | Very Poor | Very difficult |

#### Factors Affecting Maintainability

1. **Volume**: Larger files are harder to maintain
2. **Complexity**: More complex code is harder to understand
3. **Comment Ratio**: Well-commented code is easier to maintain
4. **Structure**: Modular, well-organized code scores higher

### Code Duplication

Code duplication detection identifies similar code blocks that should be refactored.

#### Detection Methods

| Method | Description | Sensitivity |
|--------|-------------|-------------|
| **Exact Match** | Identical code lines | High |
| **Normalized Match** | Identical after normalization | Medium-High |
| **Abstract Syntax Tree** | Identical AST structures | Medium |
| **Semantic Match** | Functionally equivalent | Low |

#### Similarity Threshold

```yaml
duplication:
  # Minimum lines for a duplicate block
  min_block_lines: 6
  
  # Similarity threshold (0-100%)
  similarity_threshold: 80
  
  # Ignore patterns (e.g., variable names)
  ignore_patterns:
    - "^var_\\d+$"
    - "^temp\\d*$"
```

#### Duplication Impact

| Duplication % | Impact | Action |
|---------------|--------|--------|
| 0-3% | Minimal | Acceptable |
| 3-5% | Low | Monitor |
| 5-10% | Medium | Plan refactoring |
| 10-20% | High | Prioritize cleanup |
| > 20% | Critical | Urgent refactoring needed |

### Technical Debt

Technical Debt estimates the time required to bring code to ideal quality.

#### Debt Categories

| Category | Description | Measurement |
|----------|-------------|-------------|
| **Complexity Debt** | Time to simplify complex code | CC * factor |
| **Duplication Debt** | Time to eliminate duplicates | Lines * factor |
| **Documentation Debt** | Time to add documentation | Missing docs * factor |
| **Naming Debt** | Time to fix poor names | Instances * factor |
| **Structure Debt** | Time to reorganize code | Structure issues * factor |

#### Calculation Formula

```
Debt (minutes) = Σ (issue_count × time_per_issue) / complexity_multiplier

Where time_per_issue defaults:
  - High complexity: 120 min
  - Medium complexity: 60 min
  - Low complexity: 30 min
  - Naming issues: 15 min
  - Documentation: 10 min
```

#### Debt Ratings

| Debt | Rating | Action |
|------|--------|--------|
| < 1 day | Low | Normal development |
| 1-3 days | Moderate | Schedule cleanup |
| 3-5 days | High | Prioritize in sprint |
| 5-10 days | Very High | Requires dedicated sprint |
| > 10 days | Critical | Immediate attention needed |

### Halstead Metrics

Halstead metrics measure software complexity based on operators and operands.

#### Primary Metrics

| Metric | Formula | Description |
|--------|---------|-------------|
| **n1** | Count | Unique operators |
| **n2** | Count | Unique operands |
| **N1** | Count | Total operators |
| **N2** | Count | Total operands |

#### Derived Metrics

| Metric | Formula | Description |
|--------|---------|-------------|
| **Program Length** | N = N1 + N2 | Total tokens |
| **Vocabulary** | n = n1 + n2 | Unique tokens |
| **Volume** | V = N × log₂(n) | Information content |
| **Difficulty** | D = (n1/2) × (N2/n2) | Error proneness |
| **Effort** | E = D × V | Mental effort |
| **Time** | T = E/18 | Estimated time (seconds) |
| **Bugs** | B = V/3000 | Expected bugs |

#### Example Calculation

```python
# operators: def, =, +, return (4)
# operands: a, b, x, 1 (4)
# n1=4, n2=4, N1=4, N2=4

def add(a, b):
    x = a + b
    return x

# Program Length: N = 4 + 4 = 8
# Vocabulary: n = 4 + 4 = 8
# Volume: V = 8 × log₂(8) = 8 × 3 = 24 bits
# Difficulty: D = (4/2) × (4/4) = 2
# Effort: E = 2 × 24 = 48
```

---

## API Reference

### Analyzer Class

Main class for code analysis operations.

#### Constructor

```python
from codemetrics import Analyzer

analyzer = Analyzer(
    config: Configuration = None,
    cache_dir: str = ".codemetrics-cache",
    verbose: bool = False
)
```

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `config` | Configuration | None | Analysis configuration |
| `cache_dir` | str | ".codemetrics-cache" | Cache directory path |
| `verbose` | bool | False | Enable verbose output |

#### Methods

##### `analyze()`

Perform code analysis on specified paths.

```python
results = analyzer.analyze(
    path: str | List[str],
    incremental: bool = False,
    changed_files: List[str] = None,
    verbose: bool = False
) -> AnalysisResults
```

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `path` | str/List[str] | Required | Path(s) to analyze |
| `incremental` | bool | False | Use incremental analysis |
| `changed_files` | List[str] | None | Files changed since last analysis |
| `verbose` | bool | False | Print progress information |

**Returns:** `AnalysisResults` object containing all metrics

**Example:**

```python
results = analyzer.analyze('./src')
print(f"Files analyzed: {results.summary.file_count}")
```

##### `analyze_file()`

Analyze a single file.

```python
result = analyzer.analyze_file(
    file_path: str
) -> FileMetrics
```

##### `analyze_string()`

Analyze code from a string without file I/O.

```python
result = analyzer.analyze_string(
    code: str,
    language: str = "python",
    file_name: str = "<string>"
) -> FileMetrics
```

##### `get_supported_languages()`

Get list of supported languages.

```python
languages = analyzer.get_supported_languages() -> List[str]
```

##### `validate_config()`

Validate current configuration.

```python
is_valid, errors = analyzer.validate_config() -> Tuple[bool, List[str]]
```

#### Properties

| Property | Type | Description |
|----------|------|-------------|
| `config` | Configuration | Current configuration |
| `cache` | Cache | Cache manager instance |
| `results` | AnalysisResults | Last analysis results |

### MetricsCollector Class

Collects and aggregates metrics from analyzed code.

```python
from codemetrics import MetricsCollector

collector = MetricsCollector()
collector.add_file_metrics(file_metrics)
collector.add_function_metrics(function_metrics)
summary = collector.get_summary()
```

#### Methods

| Method | Description |
|--------|-------------|
| `add_file_metrics()` | Add file-level metrics |
| `add_function_metrics()` | Add function-level metrics |
| `add_class_metrics()` | Add class-level metrics |
| `get_summary()` | Get aggregated summary |
| `get_by_file()` | Get metrics grouped by file |
| `get_by_language()` | Get metrics grouped by language |
| `reset()` | Clear all collected metrics |

### ReportGenerator Class

Generates reports in various formats.

```python
from codemetrics import ReportGenerator

generator = ReportGenerator(
    template: str = None,
    theme: str = "default"
)
report = generator.generate(
    results: AnalysisResults,
    format: str = "html"
)
```

#### Output Formats

| Format | Method | Description |
|--------|--------|-------------|
| `html` | `generate_html()` | Interactive HTML report |
| `json` | `generate_json()` | JSON data export |
| `xml` | `generate_xml()` | XML (JUnit compatible) |
| `markdown` | `generate_markdown()` | Markdown report |
| `sarif` | `generate_sarif()` | SARIF for GitHub |
| `csv` | `generate_csv()` | CSV spreadsheet |
| `console` | `generate_console()` | Colored console output |

#### Template Variables

Available variables for custom templates:

```jinja2
{{ project_name }}
{{ analysis_date }}
{{ analysis_duration }}
{{ grade }}
{{ file_count }}
{{ loc.total }}
{{ loc.code }}
{{ loc.comments }}
{{ loc.blank }}
{{ avg_complexity }}
{{ max_complexity }}
{{ avg_maintainability }}
{{ technical_debt }}
{{ issues }}
{{ high_complexity_functions }}
{{ duplicate_blocks }}
```

### Configuration Class

Manages analysis configuration.

```python
from codemetrics import Configuration

config = Configuration()
config.load("codemetrics.yml")
config.set("thresholds.max_complexity", 15)
config.save("custom-config.yml")
```

#### Methods

| Method | Description |
|--------|-------------|
| `load(path)` | Load configuration from file |
| `save(path)` | Save configuration to file |
| `set(key, value)` | Set configuration value |
| `get(key, default)` | Get configuration value |
| `to_dict()` | Convert to dictionary |
| `merge(other)` | Merge with another config |
| `validate()` | Validate configuration |

#### Default Configuration

```python
Configuration.DEFAULTS = {
    "analysis.paths": ["."],
    "analysis.exclude": ["**/node_modules/**", "**/__pycache__/**"],
    "analysis.min_file_lines": 3,
    "analysis.max_depth": 10,
    "thresholds.cyclomatic_complexity": {"warning": 10, "error": 20},
    "thresholds.maintainability_index": {"warning": 70, "error": 50},
    "output.format": "console",
    "cache.enabled": True,
    "cache.directory": ".codemetrics-cache"
}
```

### AnalysisResults Class

Contains results from code analysis.

```python
results = analyzer.analyze("./src")

# Access results
results.summary           # Overall summary
results.files            # Per-file metrics
results.issues           # All issues found
results.functions        # Function-level metrics
results.classes          # Class-level metrics
results.dependencies     # Dependency information
```

#### Summary Object

```python
{
    "project_name": "my-project",
    "analysis_date": "2024-04-20T14:30:00",
    "duration_seconds": 12.5,
    "file_count": 142,
    "loc": {
        "total": 12847,
        "code": 8628,
        "comments": 3291,
        "blank": 1928
    },
    "complexity": {
        "cyclomatic": {"avg": 3.42, "max": 48, "total": 485},
        "cognitive": {"avg": 2.18, "max": 32, "total": 310}
    },
    "maintainability": {
        "score": 78.5,
        "grade": "B"
    },
    "technical_debt_minutes": 3024,
    "duplication": {
        "percent": 4.2,
        "lines": 541
    },
    "issue_count": {"critical": 0, "error": 3, "warning": 12, "info": 45}
}
```

---

## Output Formats

### JSON Output

```json
{
  "version": "2.0.0",
  "project": {
    "name": "my-project",
    "path": "/path/to/project"
  },
  "summary": {
    "files": 142,
    "loc": 12847,
    "complexity": 3.42,
    "maintainability": 78.5,
    "grade": "B"
  },
  "files": [
    {
      "path": "src/main.py",
      "language": "python",
      "loc": 456,
      "complexity": 8.5,
      "maintainability": 82.3,
      "issues": []
    }
  ],
  "issues": [
    {
      "file": "src/main.py",
      "line": 42,
      "severity": "warning",
      "type": "high_complexity",
      "message": "Function 'process_data' has cyclomatic complexity of 18"
    }
  ]
}
```

### HTML Report

Generates an interactive HTML report with:
- Dashboard with key metrics
- Charts and visualizations
- File tree navigation
- Issue details
- Filter and search capabilities
- Export functionality

### SARIF Output

```json
{
  "version": "2.1",
  "$schema": "https://raw.githubusercontent.com/oasis-tcs/sarif-spec/master/Schemata/sarif-schema-2.1.0.json",
  "runs": [{
    "tool": {
      "driver": {
        "name": "CodeMetrics",
        "version": "2.0.0"
      }
    },
    "results": [
      {
        "level": "warning",
        "message": {
          "text": "Cyclomatic complexity 18 exceeds threshold of 15"
        },
        "locations": [{
          "physicalLocation": {
            "artifactLocation": {
              "uri": "src/main.py"
            },
            "region": {
              "startLine": 42
            }
          }
        }]
      }
    ]
  }]
}
```

---

## Advanced Usage

### Incremental Analysis

Only analyze files that have changed since the last run:

```bash
# First run (full analysis)
codemetrics analyze . --output baseline.json

# Subsequent runs (incremental)
codemetrics analyze . --incremental

# With Git integration
codemetrics analyze . --incremental --git-changes
```

```python
from codemetrics import Analyzer

analyzer = Analyzer()

# First full analysis
results = analyzer.analyze('./src')
results.save_state('state.json')

# Load previous state for incremental analysis
analyzer.load_state('state.json')
incremental_results = analyzer.analyze('./src', incremental=True)
```

### Baseline Comparison

Compare current metrics against a baseline:

```bash
# Create baseline
codemetrics analyze . --save-baseline baseline-2024-01.json

# Later, compare against baseline
codemetrics analyze . --compare-with baseline-2024-01.json --show-diff
```

```python
from codemetrics import Analyzer, BaselineComparator

analyzer = Analyzer()
comparator = BaselineComparator()

baseline = analyzer.load_baseline('baseline.json')
current = analyzer.analyze('./src')

comparison = comparator.compare(baseline, current)

print(f"Complexity change: {comparison.complexity_change:+.1f}%")
print(f"New issues: {comparison.new_issues}")
print(f"Resolved issues: {comparison.resolved_issues}")
```

### Custom Rules

Define project-specific rules:

```python
from codemetrics import Rule, RuleEngine

class NoGotoRule(Rule):
    name = "no-goto"
    description = "Disallow goto statements"
    severity = "warning"
    
    def check(self, context):
        for node in context.find_nodes('goto'):
            self.report(
                file=context.file,
                line=node.line,
                message=f"goto statement found at line {node.line}"
            )

engine = RuleEngine()
engine.register_rule(NoGotoRule())
results = engine.run(analyzer.analyze('./src'))
```

### Plugins

Create and use plugins:

```python
# my_plugin.py
from codemetrics.plugins import Plugin

class MyPlugin(Plugin):
    name = "my-plugin"
    version = "1.0.0"
    
    def on_analyze_complete(self, results):
        # Custom post-processing
        self.send_to_webhook(results)
        
    def get_metrics(self):
        return {"custom_metric": self.calculate()}

# Register plugin
# codemetrics.yml:
# plugins:
#   - path: my_plugin.MyPlugin
#     enabled: true
```

---

## Troubleshooting

### Common Issues

#### Issue: "No files found to analyze"

**Cause:** Incorrect paths or overly restrictive filters

**Solution:**
```bash
# Verify path exists
ls -la ./src

# Check file patterns
codemetrics analyze ./src --verbose

# Disable filters temporarily
codemetrics analyze ./src --include "**/*"
```

#### Issue: "Permission denied" errors

**Cause:** Insufficient read permissions on files

**Solution:**
```bash
# Check permissions
ls -la ./src

# Fix permissions
chmod -R u+r ./src

# Run with appropriate user
sudo codemetrics analyze ./src
```

#### Issue: "Out of memory" on large projects

**Cause:** Insufficient RAM for large codebases

**Solution:**
```bash
# Increase memory limit
codemetrics analyze ./src --max-depth 3

# Process in chunks
codemetrics analyze ./src/module1 --output part1.json
codemetrics analyze ./src/module2 --output part2.json
codemetrics merge part1.json part2.json --output combined.json

# Use streaming mode
codemetrics analyze ./src --stream
```

#### Issue: "Unsupported language" error

**Cause:** Language not installed or parser not available

**Solution:**
```bash
# Check supported languages
codemetrics --list-languages

# Install optional parsers
pip install codemetrics[typescript]  # For TypeScript support
pip install codemetrics[java]         # For Java support

# Verify installation
python -c "from codemetrics.parsers import javascript; print('OK')"
```

#### Issue: "Cache corrupted" warnings

**Cause:** Previous analysis left incomplete cache

**Solution:**
```bash
# Clear cache
codemetrics analyze . --clear-cache

# Or manually delete cache
rm -rf .codemetrics-cache

# Verify cache is clear
ls -la .codemetrics-cache
```

#### Issue: Slow analysis performance

**Cause:** Too many files or complex analysis settings

**Solution:**
```bash
# Use quick mode
codemetrics analyze . --quick

# Exclude unnecessary directories
codemetrics analyze . --exclude "**/node_modules/**" --exclude "**/vendor/**"

# Increase analysis speed
codemetrics analyze . --parallel --workers 4

# Profile analysis
codemetrics analyze . --profile --output profile.txt
```

### FAQ

**Q: Can I analyze multiple repositories in one report?**
A: Yes, use the merge command:
```bash
codemetrics analyze ./repo1 --output repo1.json
codemetrics analyze ./repo2 --output repo2.json
codemetrics merge repo1.json repo2.json --output combined.json
```

**Q: How do I exclude generated files?**
A: Add patterns to your config:
```yaml
analysis:
  exclude:
    - "**/generated/**"
    - "**/*.gen.py"
    - "**/migrations/*.py"
```

**Q: Can I integrate with SonarQube?**
A: Yes, export in SonarQube-compatible format:
```bash
codemetrics analyze . --format sonarqube --output sonarqube.json
```

**Q: How accurate is the technical debt estimate?**
A: The estimates are based on industry averages and should be calibrated for your team. Adjust factors in configuration:
```yaml
thresholds:
  technical_debt:
    factors:
      high_complexity: 180  # minutes per instance
      duplication: 60        # minutes per 10 lines
```

**Q: Does CodeMetrics work with monorepos?**
A: Yes, use path mapping:
```yaml
analysis:
  monorepo:
    enabled: true
    packages:
      - path: packages/a
        name: package-a
      - path: packages/b
        name: package-b
```

### Debug Mode

Enable detailed debugging output:

```bash
# Basic debug
codemetrics analyze . --debug

# Trace all operations
codemetrics analyze . --trace

# Verbose with timestamps
codemetrics analyze . --verbose --log-timestamps

# Save debug log
codemetrics analyze . --debug --debug-log debug.log
```

Debug logging includes:
- File parsing details
- Metric calculation steps
- Rule evaluation traces
- Cache operations
- Performance profiling

---

## Contributing

Contributions are welcome! Please read our contributing guidelines before submitting PRs.

### Development Setup

```bash
git clone https://github.com/moggan1337/CodeMetrics.git
cd CodeMetrics
python -m venv venv
source venv/bin/activate
pip install -e ".[dev,all]"
```

### Running Tests

```bash
# Run all tests
pytest tests/

# Run with coverage
pytest tests/ --cov=codemetrics --cov-report=html

# Run specific test file
pytest tests/test_analyzer.py -v

# Run tests matching pattern
pytest -k "complexity" -v
```

### Code Style

```bash
# Format code
black src/ tests/

# Lint code
flake8 src/ tests/
pylint src/

# Type check
mypy src/
```

---

## Changelog

See [CHANGELOG.md](CHANGELOG.md) for full version history.

---

## License

MIT License - see [LICENSE](LICENSE) for details.

---

## Support

- **Documentation**: [docs/](docs/)
- **Issue Tracker**: [GitHub Issues](https://github.com/moggan1337/CodeMetrics/issues)
- **Discussion**: [GitHub Discussions](https://github.com/moggan1337/CodeMetrics/discussions)
- **Email**: support@codemetrics.dev

---

<div align="center">

**Built with ❤️ by developers, for developers**

[Back to Top](#codemetrics)

</div>
