# Module Settings

Modules can declare settings that are managed through the admin panel automatically.

## Declaring Settings

Add a `settings` array to your `module.json`:

```json
{
    "name": "My Module",
    "settings": [
        {
            "key": "api_key",
            "label": "API Key",
            "type": "text",
            "required": true,
            "placeholder": "sk_live_...",
            "hint": "Get this from your provider's dashboard."
        },
        {
            "key": "display_mode",
            "label": "Display Mode",
            "type": "select",
            "options": ["inline", "popup", "sidebar"],
            "default": "inline"
        },
        {
            "key": "enabled_on_pages",
            "label": "Enable on pages",
            "type": "checkbox",
            "default": "0"
        }
    ]
}
```

## Field Types

| Type | Renders as | Value stored |
|---|---|---|
| `text` | Single-line input | String |
| `password` | Masked input | String |
| `textarea` | Multi-line text area | String |
| `select` | Dropdown | Selected option string |
| `checkbox` | Checkbox | `"1"` or `"0"` |

## Field Properties

| Property | Required | Description |
|---|---|---|
| `key` | Yes | Setting key (stored in database) |
| `label` | Yes | Label shown in the admin form |
| `type` | Yes | One of: text, password, textarea, select, checkbox |
| `required` | No | If `true`, module redirects to settings on activation |
| `default` | No | Default value |
| `placeholder` | No | Placeholder text for text/password inputs |
| `hint` | No | Help text shown below the field |
| `options` | No | Array of options for `select` type |

## Reading Settings

In your `boot.php`:

```php
$apiKey = Setting::get('api_key', '');
$mode = Setting::get('display_mode', 'inline');
$onPages = Setting::get('enabled_on_pages', '0') === '1';
```

## Auto-redirect on Activation

When a module with `required: true` settings is activated and those settings are empty, the admin is automatically redirected to the module's settings page. The user must fill in the required fields before the module functions.

## Settings Storage

All settings are stored in the `c3_settings` table as key-value pairs. Module settings share the same table as core settings — use unique, descriptive keys to avoid collisions (e.g. `mymodule_api_key` rather than just `api_key`).
