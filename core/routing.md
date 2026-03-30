# Routing

The `Router` class parses request URLs and dispatches to controller actions.

## Built-in Routes

| Pattern | Controller | Action |
|---|---|---|
| `/` | BlogController | index |
| `/pages/{num}` | BlogController | index (paginated) |
| `/post/{slug}` | BlogController | single |
| `/category/{slug}` | BlogController | category |
| `/category/{slug}/{num}` | BlogController | category (paginated) |
| `/page/{slug}` | PageController | show |
| `/register` | AuthController | register |
| `/feed` | FeedController | rss |
| `/sitemap.xml` | FeedController | sitemap |

## Route Patterns

- `{slug}` matches alphanumeric characters, hyphens, and underscores
- `{num}` matches digits only

## Adding Routes via Modules

```php
Modules::on('routes', function (&$routes) {
    $routes['/contact'] = [
        'controller' => 'ContactController',
        'action'     => 'show',
    ];
    $routes['/api/posts/{num}'] = [
        'controller' => 'ApiController',
        'action'     => 'getPost',
    ];
});
```

## URL Generation

```php
Router::url('post/hello-world');
// Returns: https://yoursite.com/post/hello-world

url('admin/');  // helper shortcut
// Returns: https://yoursite.com/admin/
```

## Admin Routing

Admin requests (`/admin/*`) are handled by a separate router in `admin/index.php`. Each admin page is a PHP file in `admin/pages/`. The path `/admin/posts` loads `admin/pages/posts.php`.
