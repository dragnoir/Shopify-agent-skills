# Shopify Agent Skills 🛍️

> **AI Agent Skills for Shopify Development** - A comprehensive collection of specialized skills that extend AI agent capabilities for building Shopify stores, themes, apps, and integrations.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-Compatible-green.svg)](https://agentskills.io)
[![Shopify Partner](https://img.shields.io/badge/Shopify-Partner-96bf48.svg)](https://shopify.dev)

## 🎯 What is this?

This repository contains [Agent Skills](https://agentskills.io/what-are-skills) for Shopify development. Agent Skills are a lightweight, open format for extending AI agent capabilities with specialized knowledge and workflows.

**How it works:**

1. **Discovery**: At startup, agents load only the name and description of each skill
2. **Activation**: When a task matches a skill's description, the agent reads the full instructions
3. **Execution**: The agent follows the instructions, using bundled scripts and references as needed

## 📁 Skill Categories

| Category                                                       | Description                                                              | Status   |
| -------------------------------------------------------------- | ------------------------------------------------------------------------ | -------- |
| [**theme-development**](./skills/theme-development/)           | Complete guide to creating, architecting, and customizing Shopify themes | ✅ Ready |
| [**liquid-templating**](./skills/liquid-templating/)           | Liquid template language - objects, filters, tags, and patterns          | ✅ Ready |
| [**app-development**](./skills/app-development/)               | Building Shopify apps with extensions and embedded experiences           | ✅ Ready |
| [**headless-hydrogen**](./skills/headless-hydrogen/)           | Hydrogen framework and headless commerce with Oxygen                     | ✅ Ready |
| [**checkout-customization**](./skills/checkout-customization/) | Checkout UI extensions and payment customizations                        | ✅ Ready |
| [**shopify-functions**](./skills/shopify-functions/)           | Backend logic with Shopify Functions (discounts, shipping, etc.)         | ✅ Ready |
| [**api-graphql**](./skills/api-graphql/)                       | Shopify GraphQL APIs, Admin API, and Storefront API                      | ✅ Ready |
| [**cli-tools**](./skills/cli-tools/)                           | Shopify CLI commands and developer tooling                               | ✅ Ready |

## 🚀 Quick Start

### For AI Agent Users

1. Clone or add this repository to your AI agent's skill discovery path:

   ```bash
   git clone https://github.com/your-org/shopify-agent-skills.git
   ```

2. Point your agent to the skills directory:

   ```
   skills/
   ├── theme-development/SKILL.md
   ├── liquid-templating/SKILL.md
   ├── app-development/SKILL.md
   └── ...
   ```

3. The agent will automatically discover and use relevant skills when needed.

### For Developers

Each skill folder contains:

- `SKILL.md` - The main instruction file (required)
- `references/` - Additional documentation and references
- `examples/` - Code examples and templates
- `scripts/` - Helper scripts (where applicable)

## 📖 Skill Format

Skills follow the [Agent Skills Specification](https://agentskills.io/specification):

```markdown
---
name: skill-name
description: Brief description of what this skill does and when to use it.
license: MIT
metadata:
  author: your-org
  version: "1.0"
---

# Skill Title

## When to use this skill

...

## Instructions

...
```

## 🛠️ Requirements

To use these skills effectively, you'll need:

- **Shopify Partner Account** - [Create one here](https://partners.shopify.com/signup)
- **Shopify CLI** - `npm install -g @shopify/cli`
- **Node.js 18+** - For modern Shopify development
- **VS Code** (recommended) - With [Shopify Liquid extension](https://marketplace.visualstudio.com/items?itemName=Shopify.theme-check-vscode)

## 🤝 Contributing

We welcome contributions! Please follow these guidelines:

1. Fork the repository
2. Create a new skill folder under `skills/`
3. Add a `SKILL.md` following the specification
4. Include relevant references and examples
5. Submit a pull request

### Skill Writing Best Practices

- Keep instructions under 5000 tokens
- Use progressive disclosure - link to reference files for details
- Include specific keywords for better agent matching
- Provide concrete examples and code snippets
- Document edge cases and common issues

## 📚 Resources

- [Agent Skills Specification](https://agentskills.io/specification)
- [Shopify Dev Documentation](https://shopify.dev)
- [Shopify Liquid Reference](https://shopify.dev/docs/api/liquid)
- [Shopify CLI Theme Commands](https://shopify.dev/docs/api/shopify-cli/theme)
- [Dawn Theme (Reference Theme)](https://github.com/Shopify/dawn)
- [Skeleton Theme (Starter Theme)](https://github.com/Shopify/skeleton-theme)

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## ⭐ Support

If you find these skills helpful, please consider:

- Starring this repository ⭐
- Sharing with other Shopify developers
- Contributing improvements and new skills

---

**Made with ❤️ for the Shopify developer community**
