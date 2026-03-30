# Template Inheritance

Core 3's theme engine supports template inheritance. A theme only needs to include the files it wants to override — anything missing falls back to the `default` theme automatically.

## How It Works

When Core 3 needs to render a template, the `Theme::resolve()` method looks for it in this order:

1. The active theme's `templates/` directory
2. The `default` theme's `templates/` directory

If neither has the file, an error message is shown.

## Example: Dark Theme

The bundled `dark` theme demonstrates this pattern. It only contains:

```
dark/
├── theme.json
├── assets/
│   └── style.css          # Dark colour overrides
└── templates/
    └── partials/
        └── header.php     # Uses logo-light.svg instead of logo.svg
```

Everything else — `blog/index.php`, `blog/single.php`, `page.php`, `404.php`, `footer.php`, `sidebar.php` — is inherited from the `default` theme. The dark theme only changes the CSS variables and the header logo.

## What to Override

| Template | Override when... |
|---|---|
| `partials/header.php` | You need a different nav structure, logo, or `<head>` content |
| `partials/footer.php` | You want custom footer content or scripts |
| `assets/style.css` | Always — this is your theme's visual identity |
| `blog/index.php` | You want a different post listing layout (grid, cards, etc.) |
| `blog/single.php` | You want a different single post layout |
| `front-page.php` | You have a custom homepage design |
| `404.php` | You want a branded error page |

## Template Data

Templates receive data via `extract()`, making variables available as local PHP variables. Common variables:

| Variable | Available in | Type |
|---|---|---|
| `$posts` | blog/index, blog/category | array of post rows |
| `$post` | blog/single | single post row |
| `$page` | page, front-page | single page row |
| `$pag` | blog/index, blog/category | pagination metadata |
| `$category` | blog/category | category row |
| `$comments` | blog/single | array of comment rows |
| `$pageTitle` | all templates | string for `<title>` |
