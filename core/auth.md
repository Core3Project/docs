# Authentication

The `Auth` class handles login, logout, sessions, CSRF tokens, password resets, and role-based access control.

## Login & Logout

```php
// Attempt login (returns bool)
Auth::login($usernameOrEmail, $password);

// Destroy session
Auth::logout();
```

## Session State

```php
Auth::check();    // bool — is a user logged in?
Auth::id();       // int|null — current user ID
Auth::role();     // string — current user role
Auth::user();     // array|null — full user row from database
```

## Roles

| Role | Permissions |
|---|---|
| `admin` | Full access to everything |
| `editor` | Create, edit, delete posts and pages |
| `author` | Create and edit own posts |
| `subscriber` | View only (frontend registration) |

```php
Auth::isAdmin();    // role === 'admin'
Auth::canEdit();    // admin or editor
Auth::canWrite();   // admin, editor, or author
```

## Guarding Pages

```php
// Require login (redirects to /admin/login if not authenticated)
Auth::guard();

// Require specific roles
Auth::guard('admin');
Auth::guard('admin', 'editor');
```

## CSRF Protection

```php
// Get or generate a CSRF token
$token = Auth::csrf();

// Render a hidden form field
echo Auth::csrfField();
// Output: <input type="hidden" name="_csrf" value="...">

// Validate a submitted token
Auth::checkCsrf($_POST['_csrf']);  // bool
```

## Password Reset

```php
// Generate a reset token (valid for 1 hour)
$result = Auth::createResetToken($email);
// Returns: ['user' => [...], 'token' => '...'] or null

// Consume the token and set new password
Auth::resetPassword($token, $newPassword);  // bool
```

## Registration

```php
$result = Auth::register($username, $email, $password, $displayName, $role);
// Returns: true on success, or error string
```
