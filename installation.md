# Installation

## Step 1: Upload

Download the latest release from [GitHub Releases](https://github.com/Core3Project/Core3CMS/releases/latest) and upload the files to your web server via FTP, SFTP, or your host's file manager.

You can install Core 3 in the site root or a subdirectory. The installer detects the path automatically.

## Step 2: Run the Installer

Navigate to `https://yoursite.com/install/` in your browser. The installer walks you through four steps:

### Check
The installer verifies your server meets the requirements — PHP version, required extensions, and writable directories. Fix any failed checks before continuing.

### Database
Enter your MySQL database credentials. If the database doesn't exist yet, Core 3 will create it for you (if your MySQL user has `CREATE` privileges).

| Field | Description |
|---|---|
| Database Host | Usually `localhost` |
| Database Name | The database to use |
| Database Username | MySQL username |
| Database Password | MySQL password |
| Table Prefix | Default: `c3_` — useful if sharing a database |

### Setup
Configure your site and create the admin account.

| Field | Description |
|---|---|
| Site Title | Shown in the header and browser tab |
| Site URL | Full URL including `https://` — no trailing slash |
| Username | Your admin login |
| Email | Used for password resets |
| Password | Minimum 6 characters |

### Done
The installer creates:
- All database tables
- Your admin user account
- Default settings, categories, and a welcome post
- The `core/config.php` configuration file
- The `.htaccess` file with correct rewrite rules

## Step 3: Clean Up

**Delete the `/install` directory** from your server. Leaving it accessible is a security risk. Core 3 will redirect to the admin panel if it detects the installer after config exists, but removing it is best practice.

## Step 4: Log In

Visit `https://yoursite.com/admin/login` and sign in with the credentials you created during setup.

## Troubleshooting

### Redirect loop on install
If visiting `/install/` causes a redirect loop, your server may have a pre-existing `.htaccess` file interfering. Delete any existing `.htaccess` and try again — the installer generates a fresh one.

### Session issues (login not working)
Some shared hosts have misconfigured PHP session paths. Core 3 includes a fallback that auto-detects this and uses the system temp directory. If login still fails after entering correct credentials, check that the `session` PHP extension is enabled in your host's PHP settings.

### 500 error after install
Check your host's PHP error log. Common causes:
- Missing `pdo_mysql` extension — enable it in PHP settings
- Wrong PHP version — Core 3 requires 7.4+
- File permissions — `core/` and `content/uploads/` need to be writable
