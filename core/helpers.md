# Helper Functions

Global utility functions available everywhere in Core 3.

## HTML & Output

| Function | Returns | Description |
|---|---|---|
| `e($string)` | string | HTML-escape (htmlspecialchars with UTF-8) |
| `url($path)` | string | Full URL relative to site root |
| `excerpt($html, $length)` | string | Strip tags and truncate (default: 200 chars) |
| `formatDate($datetime)` | string | Format using the site's date setting |
| `formatDate($datetime, 'Y-m-d')` | string | Format with custom format |
| `timeAgo($datetime)` | string | Relative time ("just now", "3h ago", "2d ago") |

## Strings

| Function | Returns | Description |
|---|---|---|
| `slugify($text)` | string | Convert to URL-safe slug (lowercase, hyphens) |

## Pagination

```php
$pag = paginate($total, $perPage, $currentPage);
// Returns:
// [
//     'total'    => 47,
//     'per_page' => 10,
//     'page'     => 2,
//     'pages'    => 5,
//     'offset'   => 10,
// ]

echo renderPagination($pag, url('pages'));
// Renders: <nav class="pagination">...</nav>
```

## Flash Messages

```php
// Set a flash message
flash('success', 'Post saved.');
flash('error', 'Something went wrong.');

// Retrieve and clear (returns array or null)
$flash = getFlash();
if ($flash) {
    echo $flash['type'];  // 'success' or 'error'
    echo $flash['msg'];
}
```

## File Uploads

```php
$result = uploadImage($_FILES['photo']);
// Success: ['ok' => true, 'file' => 'content/uploads/a1b2c3d4.jpg']
// Failure: ['error' => 'Invalid file type.']

// With custom directory
$result = uploadImage($_FILES['photo'], 'content/uploads/avatars');
```

**Allowed types:** JPEG, PNG, GIF, WebP, SVG  
**Max size:** 5 MB
