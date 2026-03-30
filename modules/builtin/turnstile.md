# Cloudflare Turnstile

Anti-bot verification for registration and comment forms using Cloudflare Turnstile.

| | |
|---|---|
| **Default** | Disabled |
| **Slug** | `turnstile` |

## What It Does

Adds a Cloudflare Turnstile CAPTCHA widget to the comment form. Validates the token server-side before allowing the comment to be saved. Requires a Turnstile site key and secret key from the Cloudflare dashboard.

## Settings

| Setting | Description |
|---|---|
| `turnstile_site_key` | Site Key. Get this from your Cloudflare dashboard → Turnstile → Add Site |
| `turnstile_secret_key` | Secret Key. Keep this private. Used for server-side verification. |

## Activation

Enable from **Admin → Modules**. After activation, configure the settings from the module's settings page.
