# Hooks Reference

Hooks are named extension points where modules can inject content or modify data. There are two types:

- **Output hooks** — callbacks return HTML strings that are concatenated
- **Data hooks** — callbacks receive data by reference and can modify it

## Registering Hooks

```php
// Register a callback (priority: lower runs first, default: 10)
Modules::on('hook_name', function (&$data) {
    // modify $data or return HTML
}, 10);

// Remove a callback
Modules::off('hook_name', $callback);

// Check if any callbacks exist
Modules::has('hook_name');  // bool
```

## Output Hooks

Output hooks are fired with `Modules::html('name')`. Each callback returns an HTML string. All strings are concatenated.

### `head`
Fires inside `<head>` before the closing tag.

```php
Modules::on('head', function () {
    return '<meta property="og:type" content="article">';
});
```

### `footer`
Fires before `</body>`.

```php
Modules::on('footer', function () {
    return '<script src="/analytics.js"></script>';
});
```

### `post_content_after`
Fires after a post's content on the single post page. Receives `$post`.

```php
Modules::on('post_content_after', function (&$post) {
    return '<div class="share-buttons">Share: ...</div>';
});
```

### `comments_replace`
Replaces the entire native comment section if any callback returns non-empty HTML. Receives `$post`.

```php
Modules::on('comments_replace', function (&$post) {
    $id = $post['slug'];
    return "<div id=\"disqus_thread\"></div><script>/* Disqus embed */</script>";
});
```

### `before_comment_form`
Fires above the native comment form.

### `comment_form_fields`
Fires inside the comment form, before the submit button. Use for CAPTCHA fields.

### `admin_dashboard_before`
Fires at the top of the admin dashboard, above the stats grid.

### `admin_dashboard_after`
Fires in the right sidebar of the admin dashboard, below the system info panel.

## Data Hooks

Data hooks are fired with `Modules::hook('name', $data)`. Callbacks receive `$data` by reference.

### `routes`
Fires during router initialisation. Add custom URL patterns.

```php
Modules::on('routes', function (&$routes) {
    $routes['/contact'] = [
        'controller' => 'ContactController',
        'action'     => 'show',
    ];
});
```

Route patterns support `{slug}` (alphanumeric + hyphens) and `{num}` (digits) placeholders.

### `comment_validate`
Fires when a comment is submitted, before saving. Set `$error` to reject.

```php
Modules::on('comment_validate', function (&$error) {
    $token = $_POST['cf-turnstile-response'] ?? '';
    if (!verify_turnstile($token)) {
        $error = 'Verification failed. Please try again.';
    }
});
```

## Hook Priority

The second argument to `Modules::on()` is priority (default: 10). Lower numbers run first.

```php
Modules::on('footer', $myCallback, 5);   // runs before default
Modules::on('footer', $otherCallback, 20); // runs after default
```
