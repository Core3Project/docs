# Contact Form

Adds a /contact page with an email contact form.

| | |
|---|---|
| **Default** | Disabled |
| **Slug** | `contact-form` |

## What It Does

Registers a `/contact` route with a contact form. Submissions are sent to the site admin's email address using the configured mail method (PHP mail or SMTP). Includes honeypot spam protection.

## Settings

| Setting | Description |
|---|---|
| `contact_recipient` | Recipient Email. Contact form submissions will be sent to this email. Leave blank to use the site's From Email. |
| `contact_success_message` | Success Message. Message shown after successful submission. |

## Activation

Enable from **Admin → Modules**. After activation, configure the settings from the module's settings page.
