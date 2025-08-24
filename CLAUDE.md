# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a **Copier template** for creating multilingual online courses using Jupyter Book. The template enables educators to create interactive, internationalized documentation with support for multiple languages (default: English and Korean).

## Architecture

### Template Structure
- **Copier Configuration**: `copier.yaml` defines template variables and questions for project generation
- **Template Files**: Located in `.copier-template/` subdirectory (configured but currently empty in this instance)
- **Book Content**: Multi-language Jupyter Book structure in `book/` directory
  - `en/` - English content
  - `ko/` - Korean content
  - `_scripts/` - Build and publishing scripts
  - `_addons/` - Custom HTML/JS components for language switching and comments

### Key Components
1. **Package**: `src/hypercourse/` - Python package with CLI support
2. **Documentation**: Jupyter Book-based course materials with internationalization
3. **CI/CD**: Automated builds and releases via GitHub Actions
4. **Testing**: pytest-based test suite in `tests/`

## Common Commands

### Development
```bash
# Install dependencies
uv sync  # Install all dependencies including dev
uv pip install -e .  # Install package in editable mode

# Run the CLI
uv run hypercourse  # or just hypercourse if installed

# Format code
poe format  # Runs black and isort

# Lint code  
poe lint  # Runs black --check, flake8, and isort --check

# Type checking
poe lint-mypy

# Run tests
poe tests
poe tests-cov  # With coverage report
```

### Book Building
```bash
# Install Jupyter Book
poe install-jupyter-book  # or install-jupyter-book-pipx

# Build the book (both languages)
poe book-build

# Build with all outputs
poe book-build-all

# Publish to GitHub Pages
poe book-publish
```

### Template Operations
```bash
# Initialize a new project from this template
make init-project  # Warning: only run once on new projects

# Reinitialize/update template (preserves .copierignore files)
make reinit-project

# Test template generation
make test-init-project  # Creates in tmp/ directory
```

### Utilities
```bash
# Clean build artifacts
poe clean

# Build package
poe build  # Uses uv build

# Show available tasks
poe --help

# Lock dependencies
uv lock

# Update dependencies
uv lock --upgrade
```

## Template Usage

When using this as a Copier template:
1. The template prompts for project configuration (name, author, license, etc.)
2. It optionally applies a secondary code template if specified
3. Generated projects include:
   - Multi-language Jupyter Book structure
   - Python package skeleton (if `use_source_code_skeleton=true`)
   - CI/CD workflows for building and publishing
   - Pre-configured development tools (black, isort, flake8, mypy, pytest)

## Important Notes

- This is a template repository - avoid modifying template-specific files directly
- The `book/` directory contains the actual course content structure
- Language configuration is in `book/{lang}/_config.yml`
- Table of contents in `book/{lang}/_toc.yml`
- Build scripts handle preprocessing, building both language versions, and postprocessing
- UV manages Python dependencies and packaging, POE (poethepoet) provides task automation
- UV is significantly faster than Poetry for dependency resolution and installation