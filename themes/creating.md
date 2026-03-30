# Creating a Theme

A step-by-step guide to building a Core 3 theme from scratch.

## 1. Create the Directory

```
content/themes/my-theme/
├── theme.json
├── assets/
│   └── style.css
└── templates/
    └── partials/
        └── header.php
```

## 2. Write theme.json

```json
{
    "name": "My Theme",
    "version": "1.0.0",
    "description": "A custom theme for my site.",
    "author": "Your Name"
}
```

## 3. Override the Header

The header is the most common template to override. Here's a minimal example:

```php
<?php
$_siteName = Setting::get('site_name', 'Core 3 CMS');
$_navPages = DB::rows("SELECT title,slug FROM " . DB::t('pages') . " WHERE status='published' AND show_in_nav=1 ORDER BY sort_order,title");
?>
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title><?= isset($pageTitle) ? e($pageTitle) . ' — ' : '' ?><?= e($_siteName) ?></title>
<link rel="icon" type="image/svg+xml" href="<?= url('assets/images/favicon.svg') ?>">
<link rel="stylesheet" href="<?= Theme::asset('style.css') ?>?v=<?= e(Setting::get('cache_version', '0')) ?>">
<?= Modules::html('head') ?>
</head>
<body>
<header>
    <a href="<?= url() ?>"><?= e($_siteName) ?></a>
    <nav>
        <?php foreach ($_navPages as $np): ?>
        <a href="<?= url('page/' . $np['slug']) ?>"><?= e($np['title']) ?></a>
        <?php endforeach; ?>
    </nav>
</header>
```

## 4. Write Your CSS

```css
/* content/themes/my-theme/assets/style.css */
:root {
    --bg: #ffffff;
    --text: #1e1e1e;
    --red: #b72626;
}

body {
    font-family: -apple-system, sans-serif;
    color: var(--text);
    background: var(--bg);
}
```

## 5. Activate

Go to **Admin → Appearance → Themes** and click **Activate** next to your theme.

## Tips

- **Start from the default theme.** Copy `content/themes/default/` and modify it. This ensures you have all templates.
- **Use CSS variables** for colours and spacing — makes it easy to create variants.
- **Test the fallback.** Delete a template from your theme and verify it falls back to the default's version correctly.
- **Cache busting.** The `?v=` parameter on stylesheets is tied to the `cache_version` setting, bumped when an admin clicks "Clear Cache".
- **Respect module hooks.** Always include `<?= Modules::html('head') ?>` in the head and `<?= Modules::html('footer') ?>` before `</body>` so modules can inject their content.
