# Migrations

The `Migration` class tracks the database schema version and applies changes automatically when Core 3 is updated.

## How It Works

On every page load, `Migration::run()` compares the stored `db_version` setting against `C3_VERSION`. If the code is newer, it runs any pending migration methods in order.

This is completely automatic — users don't need to run any commands.

## Adding a Migration

For contributors adding database changes:

### 1. Add the version to the list

```php
// In core/classes/Migration.php
private static $versions = [
    '3.0.0',
    '3.1.0',
    '3.2.0',  // your new version
];
```

### 2. Create the migration method

```php
private static function migrate_3_2_0()
{
    $t = DB::prefix();
    DB::query("ALTER TABLE {$t}posts ADD COLUMN reading_time INT DEFAULT 0 AFTER views");
}
```

### 3. Bump C3_VERSION

```php
// In core/bootstrap.php
define('C3_VERSION', '3.2.0');
```

## Migration Rules

- Migrations run **once** and the version is recorded
- They run in order — you can't skip versions
- A migration method is optional — if there are no schema changes for a version, just add the version string to `$versions` and the version number will be recorded
- Always use `DB::prefix()` for table names
- Keep migrations idempotent where possible (use `IF NOT EXISTS`, `IF EXISTS`)
