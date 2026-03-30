# Maintenance Mode

Show a 'Coming Soon' or maintenance page to visitors. Logged-in admins can still browse the site.

| | |
|---|---|
| **Default** | Disabled |
| **Slug** | `maintenance-mode` |

## What It Does

Displays a "coming soon" or maintenance page to all visitors except logged-in admins. The maintenance message is configurable. Useful during development or when performing major updates.

## Settings

| Setting | Description |
|---|---|
| `maintenance_title` | Page Title. The heading visitors will see. |
| `maintenance_message` | Message. The message shown below the title. |
| `maintenance_allow_admin` | Allow logged-in admins to view the site. Admins can bypass maintenance mode when logged in. |

## Activation

Enable from **Admin → Modules**. After activation, configure the settings from the module's settings page.
