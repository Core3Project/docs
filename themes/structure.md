# Theme Structure

A theme is a directory inside `content/themes/` containing templates, assets, and a metadata file.

## Directory Layout

```
your-theme/
├── theme.json              # Required: metadata
├── assets/
│   └── style.css           # Theme stylesheet
└── templates/
    ├── partials/
    │   ├── header.php       # Site header, nav, <head>
    │   ├── footer.php       # Site footer, closing tags
    │   └── sidebar.php      # Widget sidebar
    ├── blog/
    │   ├── index.php        # Post listing / blog homepage
    │   ├── single.php       # Single post view
    │   └── category.php     # Category archive
    ├── page.php             # Static page
    ├── front-page.php       # Static homepage (when configured)
    ├── contact.php          # Contact form page
    ├── register.php         # User registration
    ├── message.php          # Generic message page
    └── 404.php              # Not found
```

## theme.json

```json
{
    "name": "My Theme",
    "version": "1.0.0",
    "description": "A brief description of the theme.",
    "author": "Your Name"
}
```

All fields are required. The `name` is shown in the admin Appearance panel.

## Bundled Themes

Core 3 ships with three themes:

| Theme | Description |
|---|---|
| **default** | Clean light theme — the complete reference implementation |
| **dark** | Dark colour scheme — inherits templates from default, only overrides CSS and the header partial |

## Installing Themes

Themes can be installed two ways:

1. **FTP/File upload** — drop the theme folder into `content/themes/`
2. **Admin upload** — go to Appearance → Themes and upload a `.zip` containing a `theme.json`

Activate a theme from **Admin → Appearance → Themes**.
