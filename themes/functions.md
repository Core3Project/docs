# Template Functions

Functions available inside theme templates.

## Theme Functions

| Function | Returns | Description |
|---|---|---|
| `Theme::partial('name')` | void | Render a partial template (header, footer, sidebar) |
| `Theme::partial('name', ['key' => 'val'])` | void | Render a partial with extra data |
| `Theme::asset('file.css')` | string | URL to a file in the theme's `assets/` directory |
| `Theme::set('key', $value)` | void | Store a value in the template data scope |
| `Theme::url()` | string | URL to the active theme directory |
| `Theme::path()` | string | Filesystem path to the active theme directory |

## HTML & Output

| Function | Returns | Description |
|---|---|---|
| `e($string)` | string | HTML-escape a string (htmlspecialchars) |
| `url($path)` | string | Generate a full URL relative to the site root |
| `excerpt($html, $len)` | string | Strip HTML tags and truncate to `$len` characters |
| `formatDate($datetime)` | string | Format using the site's configured date format |
| `formatDate($datetime, 'Y-m-d')` | string | Format with a custom format string |
| `timeAgo($datetime)` | string | Relative time (e.g. "3h ago", "2d ago") |
| `Markdown::render($content, $format)` | string | Render content as HTML with XSS sanitisation |
| `renderPagination($pag, $baseUrl)` | string | Render a pagination nav bar |

## Widgets

| Function | Returns | Description |
|---|---|---|
| `Widget::zone('sidebar')` | string | Render all active widgets in a zone |
| `Widget::zone('footer')` | string | Render footer widgets |

## Modules & Hooks

| Function | Returns | Description |
|---|---|---|
| `Modules::html('hook_name')` | string | Concatenated output from all hook callbacks |
| `Modules::html('hook_name', $data)` | string | Output hook with data argument |
| `Modules::has('hook_name')` | bool | Whether any callbacks are registered |

## Auth (for conditional content)

| Function | Returns | Description |
|---|---|---|
| `Auth::check()` | bool | Whether a user is logged in |
| `Auth::isAdmin()` | bool | Whether the current user is an admin |
| `Auth::user()` | array/null | The current user's database row |

## Settings

| Function | Returns | Description |
|---|---|---|
| `Setting::get('key')` | string | Get a setting value |
| `Setting::get('key', 'default')` | string | Get a setting with a fallback |

## Database (advanced)

| Function | Returns | Description |
|---|---|---|
| `DB::row($sql, $params)` | array/null | Fetch one row |
| `DB::rows($sql, $params)` | array | Fetch all matching rows |
| `DB::count($table, $where, $params)` | int | Count matching rows |
| `DB::t('name')` | string | Prefixed table name (e.g. `c3_posts`) |

## Usage Example

```php
<?php Theme::partial('header'); ?>

<div class="container">
    <?php foreach ($posts as $post): ?>
    <article>
        <h2><a href="<?= url('post/' . $post['slug']) ?>"><?= e($post['title']) ?></a></h2>
        <span><?= formatDate($post['published_at']) ?></span>
        <p><?= excerpt($post['content'], 200) ?></p>
    </article>
    <?php endforeach; ?>

    <?= renderPagination($pag, url('pages')) ?>
</div>

<?php Theme::partial('footer'); ?>
```
