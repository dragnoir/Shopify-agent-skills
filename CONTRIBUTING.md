# Contributing to Shopify Agent Skills

Thank you for your interest in contributing to this project! This guide will help you get started.

## 📋 Table of Contents

- [Code of Conduct](#code-of-conduct)
- [How Can I Contribute?](#how-can-i-contribute)
- [Creating New Skills](#creating-new-skills)
- [Improving Existing Skills](#improving-existing-skills)
- [Submitting Changes](#submitting-changes)
- [Style Guidelines](#style-guidelines)

## Code of Conduct

By participating in this project, you agree to maintain a respectful and inclusive environment. Be kind, constructive, and professional in all interactions.

## How Can I Contribute?

### 🐛 Reporting Issues

- Check if the issue already exists
- Use a clear, descriptive title
- Describe the expected vs actual behavior
- Include relevant code snippets or examples

### 📝 Suggesting Improvements

- Open an issue describing your suggestion
- Explain the use case and benefits
- Include examples if possible

### 💻 Contributing Code

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## Creating New Skills

### Directory Structure

```
skills/
└── your-skill-name/
    ├── SKILL.md            # Required: Main instruction file
    ├── references/         # Optional: Additional documentation
    │   └── REFERENCE.md
    ├── examples/           # Optional: Code examples
    │   └── example.liquid
    └── scripts/            # Optional: Helper scripts
        └── helper.sh
```

### SKILL.md Format

```markdown
---
name: skill-name
description: A clear description of what this skill does and when to use it.
license: MIT
compatibility: Any specific requirements
metadata:
  author: your-name
  version: "1.0"
  shopify-api-version: "2025-01"
---

# Skill Title

## When to use this skill

Describe the scenarios when an agent should use this skill.

## How to [accomplish task]

Step-by-step instructions...

## Best Practices

Key recommendations...

## Common Issues

Troubleshooting tips...

## Resources

Links to official documentation...
```

### Naming Conventions

- **Directory name**: lowercase with hyphens (e.g., `theme-development`)
- **Skill name**: Must match directory name
- **Keep names descriptive but concise**

### Content Guidelines

1. **Be Specific**: Include concrete examples and code snippets
2. **Stay Current**: Use the latest Shopify API version
3. **Progressive Disclosure**: Keep SKILL.md under 5000 tokens, link to references for details
4. **Include Keywords**: Help agents discover your skill

### Quality Checklist

- [ ] Follows the Agent Skills specification
- [ ] Name matches directory name
- [ ] Description clearly explains when to use the skill
- [ ] Instructions are actionable and clear
- [ ] Code examples are tested and working
- [ ] References to official docs are included
- [ ] No placeholders or TODO comments

## Improving Existing Skills

### What to Improve

- Update deprecated APIs or syntax
- Add missing examples
- Improve clarity of instructions
- Add troubleshooting tips
- Fix errors or inaccuracies
- Update links to documentation

### Review Process

All changes will be reviewed for:

- Accuracy of information
- Clarity of instructions
- Adherence to style guidelines
- Compatibility with Shopify best practices

## Submitting Changes

### Pull Request Process

1. **Fork & Clone**

   ```bash
   git clone https://github.com/YOUR-USERNAME/shopify-agent-skills.git
   cd shopify-agent-skills
   ```

2. **Create Branch**

   ```bash
   git checkout -b feature/your-feature-name
   ```

3. **Make Changes**
   - Follow style guidelines
   - Test your examples

4. **Commit**

   ```bash
   git add .
   git commit -m "feat: add new skill for X"
   ```

5. **Push & PR**
   ```bash
   git push origin feature/your-feature-name
   ```
   Then open a pull request on GitHub.

### Commit Message Format

Use conventional commits:

- `feat:` New skill or feature
- `fix:` Bug fix or correction
- `docs:` Documentation only
- `refactor:` Code restructuring
- `chore:` Maintenance tasks

Examples:

```
feat: add webhook management skill
fix: correct deprecated filter in liquid examples
docs: update API version references
```

## Style Guidelines

### Markdown

- Use ATX-style headers (`#`, `##`, `###`)
- Include blank lines between sections
- Use fenced code blocks with language tags
- Add alt text to images

### Code Examples

```liquid
<!-- Good: Specific, tested, current -->
{{ product.featured_image | image_url: width: 500 | image_tag }}

<!-- Avoid: Vague, placeholder -->
{{ do_something }}
```

### Writing Style

- Be concise and direct
- Use active voice
- Start instructions with verbs
- Include both "what" and "why"

### Frontmatter

```yaml
---
name: lowercase-with-hyphens
description: |
  First line: what this skill does.
  Second line: when to use it.
license: MIT
metadata:
  author: your-name
  version: "1.0"
---
```

## Questions?

- Open an issue for general questions
- Check existing issues and discussions first
- Be patient - maintainers are volunteers

---

Thank you for helping make Shopify development better for everyone! 🎉
