# Template Reference

Detailed reference for each template file and the data it receives.

## partials/header.php

The site header. Responsible for the `<!DOCTYPE>` declaration, `<head>` section (meta tags, CSS, favicon), site logo, and navigation.

**Key responsibilities:**
- Output `<!DOCTYPE html>` and open `<html>`, `<head>`, `<body>`
- Load the theme stylesheet via `Theme::asset('style.css')`
- Render favicon (custom or default)
- Build navigation from published pages with `show_in_nav = 1`
- Fire the `head` module hook
- Apply custom accent colour and CSS from the Appearance Customiser

## partials/footer.php

Closes the page. Outputs the footer text, "Powered by Core 3 CMS" link, widget zone, module hooks, and closing `</body></html>`.

**Key responsibilities:**
- Render the `footer` widget zone
- Fire the `footer` module hook
- Close HTML tags

## partials/sidebar.php

Renders the sidebar widget zone. Only used if your template includes it — the default theme uses it on blog pages.

```php
<?= Widget::zone('sidebar') ?>
```

## blog/index.php

The main post listing page. Shows paginated posts.

**Variables:**
- `$posts` — array of post rows with `author_name`, `cat_name`, `cat_slug`, `comment_count`
- `$pag` — pagination array from `paginate()`

**Example post fields:** `id`, `title`, `slug`, `content`, `excerpt`, `status`, `published_at`, `views`, `author_name`, `cat_name`, `cat_slug`

## blog/single.php

Single post view with comments.

**Variables:**
- `$post` — the post row with author and category data
- `$comments` — array of approved comments
- `$commentMsg` — flash message from comment submission (array with `type` and `msg`, or null)

## blog/category.php

Posts filtered by category.

**Variables:**
- `$category` — the category row (`name`, `slug`, `description`)
- `$posts` — filtered post array
- `$pag` — pagination

## page.php

Static page display.

**Variables:**
- `$page` — the page row (`title`, `slug`, `content`, `content_format`)

Content is rendered through `Markdown::render()` which handles both HTML and Markdown formats, with XSS sanitisation.

## front-page.php

Used when a static page is set as the homepage in Settings → Reading.

**Behaviour:**
- If the page content starts with `<!DOCTYPE` — output raw (standalone HTML document)
- Otherwise — wrap in the theme header and footer

**Variables:**
- `$page` — the page row

## 404.php

Not found page. No special variables — just `$pageTitle` set to "Not Found".

## contact.php

Contact form page (used by the Contact Form module).

## register.php

User registration form (when registration is enabled in Settings → Users).

**Variables:**
- `$regError` — error message string
- `$regSuccess` — success message string
