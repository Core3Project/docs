# Module Structure

Modules extend Core 3 without modifying core files. A module is a folder inside `content/modules/` with two files.

## Directory Layout

```
your-module/
├── module.json    # Required: metadata and settings declaration
└── boot.php       # Required: code that runs when the module is active
```

## module.json

```json
{
    "name": "My Module",
    "version": "1.0.0",
    "description": "A brief description of what the module does.",
    "author": "Your Name",
    "default_enabled": "0",
    "settings": []
}
```

| Field | Type | Description |
|---|---|---|
| `name` | string | Display name in the admin panel |
| `version` | string | Semantic version |
| `description` | string | Shown on the Modules page |
| `author` | string | Author name |
| `default_enabled` | string | `"1"` to enable by default, `"0"` to disable |
| `settings` | array | Setting field declarations (see [Module Settings](modules/settings.md)) |

## boot.php

This file is `require`d when the module is active. It typically registers hook callbacks:

```php
<?php

Modules::on('footer', function () {
    return '<script src="my-script.js"></script>';
});
```

The boot file runs on every page load (both frontend and admin), so keep it lightweight. Avoid heavy database queries or API calls in the boot file — defer them to hook callbacks.

## Module Lifecycle

1. Core 3 boots and calls `Modules::init()`
2. Each module directory is scanned for `module.json`
3. The `default_enabled` value is checked against the database setting `module_{slug}`
4. If active, `boot.php` is loaded via `require_once`
5. Hook callbacks registered in boot.php are now available

## Installing Modules

Two methods:

1. **FTP/File upload** — drop the module folder into `content/modules/`
2. **Admin upload** — go to Admin → Modules and upload a `.zip` containing a `module.json`

After installing, enable the module from **Admin → Modules**.

## Checking Module State

```php
// Is a module active?
Modules::active('my-module');  // bool

// Get all loaded modules
Modules::loaded();  // ['slug' => metadata, ...]

// Get all installed modules (active or not)
Modules::all();
```
