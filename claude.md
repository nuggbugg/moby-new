# Pitch - Shopify Theme v3.2.1

## Project Overview

A professional, feature-rich Shopify e-commerce theme with extensive customization options, 30+ language support, and modern web component architecture.

## Tech Stack

- **Liquid** - Shopify's templating language (primary)
- **Vanilla JavaScript** - Web Components architecture
- **CSS** - Custom properties for theming
- **TypeScript (JSDoc)** - Type annotations without build step

No build system - files deploy directly to Shopify.

## Project Structure

```
assets/          # JS components, CSS, images
blocks/          # Reusable block components (95 files, _ prefix)
config/          # settings_schema.json, settings_data.json
layout/          # theme.liquid (root), password.liquid
locales/         # i18n - en.default.json + 30 languages
sections/        # Customizable section modules
snippets/        # Reusable template partials
templates/       # Page templates (JSON format)
```

## Key Files

| File | Purpose |
|------|---------|
| `layout/theme.liquid` | Root HTML template |
| `config/settings_schema.json` | Admin UI customization definitions |
| `config/settings_data.json` | Current theme settings |
| `assets/global.d.ts` | TypeScript global definitions |
| `assets/jsconfig.json` | TS config (checkJs: true) |

## Architecture Patterns

### Component Hierarchy
1. **Sections** - Merchant-configurable modules (Shopify Admin)
2. **Blocks** - Composable units within sections (prefixed with `_`)
3. **Snippets** - Reusable template fragments

### Web Components
```javascript
// Base pattern in assets/
class MyComponent extends DeclarativeShadowElement {
  // Auto ref management, event listeners, mutation observers
}
customElements.define('my-component', MyComponent);
```

### Liquid Patterns
```liquid
{% liquid
  assign var = section.settings.option
  render 'snippet-name', param: value
%}
{% sections 'group-name' %}
```

## Conventions

### Naming
- Block files: `_block-name.liquid` (underscore prefix)
- Sections: `section-name.liquid`
- Snippets: `snippet-name.liquid`

### CSS Variables
- Colors: `--color-foreground`, `--color-background`, `--color-primary`
- Typography: `--font-body--family`, `--font-size--body-sm`
- 7 color schemes: `scheme-1` through `scheme-7`

### Section Schema
```json
{
  "type": "section-name",
  "name": "Display Name",
  "blocks": {},
  "settings": []
}
```

## Third-Party Integrations

- **Judge.me** - Product reviews
- **TripleWhale** - Analytics
- **Subscriptions App** - Recurring purchases

## Custom Fonts

- **Memoir** (serif) - Headings
- **N27** Light/Medium (sans-serif) - Body text

## Development Notes

### No Build Process
Files deploy as-is to Shopify servers. Shopify handles optimization, CDN, and minification.

### Type Checking
JSDoc annotations with TypeScript strict mode. Path alias `@theme/*` maps to project root.

### No Automated Tests
Manual testing only. Use Shopify Design Mode for visual testing.

## Common Tasks

### Add New Section
1. Create `sections/new-section.liquid`
2. Include schema JSON at bottom
3. Add to page templates in `templates/`

### Add New Block
1. Create `blocks/_block-name.liquid`
2. Reference in parent section's blocks schema

### Add New Snippet
1. Create `snippets/snippet-name.liquid`
2. Use: `{% render 'snippet-name' %}`

### Modify Theme Settings
Edit `config/settings_schema.json` for new admin options.

### Add JavaScript Component
1. Create `assets/component-name.js`
2. Use Web Component pattern with DeclarativeShadowElement
3. Include in relevant Liquid template

## Performance Features

- Lazy loading via `section-hydration.js`
- Declarative Shadow DOM
- requestIdleCallback for non-blocking JS
- Shopify image optimization filters

## MOBY Brand Guidelines

Use the `/moby-brand` skill when you need to check brand guidelines for colors, typography, spacing, or other design decisions.

### Design System
- **Border radius**: 4px (consistent across all buttons, cards, inputs)
- **Primary dark**: #1B1A0F
- **Accent lime**: #F9FDB5 (--moby-lime)
- **No pill-shaped buttons** - always use 4px radius
