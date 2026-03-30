# Creating a Module

A walkthrough for building a Core 3 module from scratch.

## Example: Reading Time

This module calculates and displays the estimated reading time on blog posts.

### 1. Create the Directory

```
content/modules/reading-time/
├── module.json
└── boot.php
```

### 2. Write module.json

```json
{
    "name": "Reading Time",
    "version": "1.0.0",
    "description": "Shows estimated reading time on blog posts.",
    "author": "Your Name",
    "default_enabled": "0",
    "settings": [
        {
            "key": "reading_wpm",
            "label": "Words Per Minute",
            "type": "text",
            "default": "200",
            "hint": "Average reading speed. Default: 200 words per minute."
        }
    ]
}
```

### 3. Write boot.php

```php
<?php

Modules::on('post_content_after', function (&$post) {
    $wpm = (int) Setting::get('reading_wpm', '200');
    if ($wpm < 1) $wpm = 200;

    $wordCount = str_word_count(strip_tags($post['content']));
    $minutes = max(1, (int) ceil($wordCount / $wpm));

    return '<p style="color:#888;font-size:14px;margin-top:16px">'
        . $minutes . ' min read'
        . '</p>';
});
```

### 4. Install & Activate

Drop the `reading-time` folder into `content/modules/`, then enable it from **Admin → Modules**.

## Tips

- **Keep boot.php lightweight.** It runs on every page load. Put heavy logic inside hook callbacks.
- **Use unique setting keys.** Prefix with your module name to avoid collisions.
- **Test with modules disabled.** Your module shouldn't break the site if deactivated.
- **Respect existing hooks.** Check `Modules::has('hook')` if you need to know whether other modules are listening.
