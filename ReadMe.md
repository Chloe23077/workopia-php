# Workopia

Workopia is a job listing website from my PHP From Scratch course. It includes a custom Laravel-like router, controller
classes, views, a database layer and a project structure using namespaces and PSR-4 autoload. It highlights how to
structure a PHP project without using any frameworks or libraries.

# Usage

## Requirements
- PHP 7.4 or higher
- MySQL 5.7 or higher

## Installation
1. Clone the repo into your document root (www.htdocs, etc)
2. Create a database called workopia
3. Import the workopia.sql file into your database
4. Rename config/_db.php to config/db.php and update with your credentials
5. Run composer install to set up the autoloading
6. Set your document root to the public directory

## Setting the Document Root
You will need to set your document root to the public directory. Here are some instructions for setting the document root
for some popular local development tools:

### PHP built-in server
If you are using the PHP built-in server, you can run the following command from the project root:

php -S localhost:800 -t public

### Laragon
If you are using Laragon, you can set right-click the icon in the system tray and go to Apache > sites-enable >
auto.workopia.test.conf. Your file may be named differently

## Project Structure and Notes

#### Custom Laravel-like router

Creating a route in `routes.php` looks like this:

`$router->get('/lisings', 'ListingController@index');`

This would load the `index` method in the `App/controllers/ListingController.php` file.

#### Authorization Middleware

You can pass in middleware for authorization. This is an array of roles. If you want the route to be accessible only
to logged-in users, you would add the `auth` role:

`$router->get('/listings/create', 'ListingController@create', ['auth']);`

If you only want non-logged-in users to access the route, you would add the `guest` role:

`$router->get('/register', 'AuthController@register', ['guest']);`

#### Public Directory

This project has a public directory that contains all the assets like CSS, JS and images. This is where the `index.php`
file is located, which is the entry point for the application.

You will need to set your document root to the `public` directory.

#### Framework Directory

All of the core files for this project are in the `Framework` directory. This includes the following files:

- **Database.php** - Database connection and query method (PDO)
- **Router.php** - Router logic
- **Session.php** - Session logic
- **Validation.php** - Simple validations for strings, email and matching passwords
- **Authorization.php** - Handles resource authorization
- **middleware/Authorize.php** - Handles authorization middleware for routes

#### PSR-4 Autoloading

This project uses PSR-4 autoloading. All the classes are loaded in the `composer.json` file:

```json
"autoload": {
    "psr-4": {
      "Framework\\": "Framework/",
      "App\\": "App/"
    }
  }
```

#### Namespaces

This project uses namespaces for all the classes. Here are the namespaces used:

- **Framework** - All the core framework classes
- **Framework\Router** - All the router classes
- **Framework\Session** - All the session classes
- **Framework\Validation** - All the validation classes
- **Framework\Authorization** - All the authorization classes
- **Framework\Middleware\Authorize** - Authorization middleware
- **App\Controllers** - All the controllers

#### App Directory

The `App` directory contains all the main application files like controllers, views, etc. Here is the directory structure:

- **controllers/** - Contains all the controllers, including listings, users, home and error
- **views/** - Contains all the views
- **views/partials/** - Contains all the partial views

#### Other Files

- **/index.php** - Entry point for the application
- **public/.htaccess** - Handles the URL rewriting
- **/helpers.php** - Contains helper functions
- **/routes.php** - Contains all the routes
- **/config/db.php** - Contains the database configuration
- **composer.json** - Contains the composer dependencies
- **workopia.sql** - Contains the database dump

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.