# Quickstart

1. Run the following in your theme directory:
    ```bash
    composer require htmlburger/wpemerge
    ```
1. Create a new file for your routes, for example `routes/web.php`.
1. Add the following to your new `web.php` file:
    ```php
    <?php
    /**
     * Web Routes.
     */
    use WPEmerge\Facades\Route;

    Route::get()->url( '/' )->handle( function() {
        return WPEmerge\output( 'Hello World!' );
    } );
    ```
1. Add the following to the **start** of your `functions.php`:
    ```php
    use WPEmerge\Facades\WPEmerge;
 
    require_once( 'vendor/autoload.php' );
 
    add_action( 'init', function() {
        session_start(); // required only if you use Flash and OldInput
    } );

    add_action( 'after_setup_theme', function() {
        WPEmerge::bootstrap( [
            'routes' => [
                'web' => __DIR__ . '/routes/web.php',
            ],
        ] );
    } );
    ```
1. If you open your website's homepage in your browser you will now be greeted with `Hello World!`.

## Optional: Setting up autoloading for your own classes

1. Add the following to your `composer.json`:
    ```js
    "autoload": {
        "psr-4": {
            "App\\": "app/"
        }
    }
    ```
    - `App` represents the base namespace for your classes
    - `app/` represents the base path for your classes relative to your theme (i.e. `twentyseventeen/app`)

    With this change any class in the `App\` namespace will be autoloaded from the `app/` directory relative to your `composer.json`.
1. Run `composer dump-autoload` so your changes take effect

Here are a few example classes (and their filepaths) that will be autoloaded:

| Class                    | File                       |
|--------------------------|----------------------------|
| `App\MyClass`            | `app/MyClass.php`          |
| `App\Foo\Bar\Baz`        | `app/Foo/Bar/Baz.php`      |
| `App\Controllers\Home`   | `app/Controllers/Home.php` |


You can find more information about PSR-4 autoloading at http://www.php-fig.org/psr/psr-4/
