# Updater

The `Updater` class checks the GitHub Releases API for newer versions of Core 3.

## How It Works

The updater runs automatically on the admin dashboard. It queries the GitHub API every 12 hours and caches the result in the settings table.

When a newer version is detected:
- A blue info banner appears on the dashboard with a link to the release
- The "At a Glance" panel shows a green checkmark when up to date

## API

```php
// Check for updates (returns release info or null if up to date)
$update = Updater::check();
if ($update) {
    echo $update['tag'];    // e.g. "v3.2.0"
    echo $update['url'];    // GitHub release URL
    echo $update['date'];   // publish date
}

// Simple boolean check
Updater::isUpToDate();  // bool
```

## Configuration

The updater checks the `Core3Project/Core3CMS` repository. The check interval is 12 hours, cached via the `update_check_result` and `update_check_time` settings.
