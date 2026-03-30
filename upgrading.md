# Upgrading

## How Updates Work

Core 3 includes a built-in update checker that queries the GitHub Releases API every 12 hours. When a new version is available, a notice appears on the admin dashboard.

The **At a Glance** panel on the dashboard shows your current version with a green checkmark when up to date.

## Manual Upgrade Process

1. **Back up your database** — use the Backup module or export via phpMyAdmin
2. **Back up your files** — especially `core/config.php` and `content/`
3. **Download the new release** from [GitHub Releases](https://github.com/Core3Project/Core3CMS/releases)
4. **Upload and overwrite** the files on your server — but **do not overwrite**:
   - `core/config.php` (your database credentials)
   - `content/uploads/` (your uploaded files)
   - `content/themes/` (your custom themes)
   - `content/modules/` (your custom modules)
   - `.htaccess` (your generated rewrite rules)
5. **Visit your site** — the Migration system will detect the version change and apply any database updates automatically

## Database Migrations

The `Migration` class compares the stored `db_version` setting against the running `C3_VERSION` on every page load. If they don't match, it runs any pending migration methods in order.

This is completely automatic — you don't need to run any commands or SQL scripts. Just upload the new files and the database updates itself.

## Version History

| Version | Changes |
|---|---|
| 3.1.0 | Migration system, auto-updater, static front page, blog page routing, favicon, session fixes |
| 3.0.0 | Initial release — posts, pages, themes, modules, admin panel |
