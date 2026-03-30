# Settings

The `Setting` class manages key-value pairs stored in the database.

## Reading Settings

```php
$siteName = Setting::get('site_name');
$postsPerPage = Setting::get('posts_per_page', '10');  // with default
```

Settings are cached in memory after the first read — subsequent calls don't hit the database.

## Writing Settings

```php
Setting::set('site_name', 'My Blog');
```

Creates the setting if it doesn't exist, or updates it if it does.

## Deleting Settings

```php
Setting::delete('my_old_setting');
```

## Flushing Cache

```php
Setting::flush();  // clears in-memory cache
```

Call this after bulk operations to ensure fresh data on the next `get()`.

## Core Settings

| Key | Default | Description |
|---|---|---|
| `site_name` | "Core 3 CMS" | Site title |
| `site_tagline` | "" | Subtitle shown in header |
| `site_description` | "" | Used in RSS feed |
| `posts_per_page` | "10" | Blog listing pagination |
| `theme` | "default" | Active theme slug |
| `timezone` | "UTC" | PHP timezone |
| `date_format` | "M d, Y" | Date display format |
| `comments_enabled` | "1" | Global comment toggle |
| `comments_moderation` | "1" | Require comment approval |
| `registration_enabled` | "0" | Allow public registration |
| `front_page` | "posts" | Homepage: "posts" or "page" |
| `front_page_id` | "" | Page ID for static homepage |
| `blog_page_id` | "" | Page ID for blog listing |
| `cache_version` | "0" | Bumped on cache clear |
| `db_version` | "3.1.0" | Database schema version |
