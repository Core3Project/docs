# Database (DB)

The `DB` class provides a thin PDO wrapper with convenience methods. All queries use prepared statements.

## Connection

The connection is created lazily on first use. Credentials come from `core/config.php`.

```php
$pdo = DB::connect();  // returns the shared PDO instance
```

## Querying

### Fetch one row

```php
$post = DB::row("SELECT * FROM " . DB::t('posts') . " WHERE slug = ?", ['hello-world']);
// Returns: associative array or null
```

### Fetch all rows

```php
$posts = DB::rows("SELECT * FROM " . DB::t('posts') . " WHERE status = ?", ['published']);
// Returns: array of associative arrays
```

### Execute a statement

```php
$stmt = DB::query("UPDATE " . DB::t('posts') . " SET views = views + 1 WHERE id = ?", [42]);
// Returns: PDOStatement
```

## Writing

### Insert

```php
$id = DB::insert(DB::t('posts'), [
    'title'     => 'My Post',
    'slug'      => 'my-post',
    'content'   => '<p>Hello world</p>',
    'status'    => 'published',
    'author_id' => 1,
]);
// Returns: int (new auto-increment ID)
```

### Update

```php
DB::update(DB::t('posts'), ['title' => 'Updated Title'], 'id = ?', [42]);
```

### Delete

```php
DB::delete(DB::t('posts'), 'id = ?', [42]);
```

### Count

```php
$total = DB::count(DB::t('posts'), "status = 'published'");
$byAuthor = DB::count(DB::t('posts'), "author_id = ?", [1]);
```

## Table Prefix

```php
DB::prefix();      // returns 'c3_' (or whatever was configured)
DB::t('posts');    // returns 'c3_posts'
```

Always use `DB::t()` when referencing tables to ensure the correct prefix is applied.

## Database Schema

| Table | Description |
|---|---|
| `c3_users` | User accounts (username, email, password hash, role, status) |
| `c3_posts` | Blog posts (title, slug, content, status, author, category, views) |
| `c3_pages` | Static pages (title, slug, content, show_in_nav, sort_order) |
| `c3_categories` | Post categories (name, slug, description) |
| `c3_comments` | Post comments (author, email, content, status, IP) |
| `c3_settings` | Key-value settings (used by core and modules) |
| `c3_widgets` | Widget configuration (zone, type, title, config, sort_order) |
