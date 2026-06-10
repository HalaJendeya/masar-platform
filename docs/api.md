# MASAR API Documentation

MASAR uses a Laravel REST API.

Authentication is handled using Laravel Sanctum.

---

## Authentication Routes

```php
Route::prefix('auth')->group(function () {
    Route::post('/register', 'register');
    Route::post('/login', 'login');
    Route::post('/logout', 'logout');
});
