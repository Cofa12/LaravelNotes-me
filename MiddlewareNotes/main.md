# All middleware are resolved via the service container,so you may type-hint any dependencies you need within a middleware's constructor.

Middleware: In Laravel, middleware are classes that execute before a request reaches a controller or route. They can be used for various purposes, such as authentication, authorization, logging, request modification, etc.
Dependency Injection: This is a software design pattern that promotes loose coupling by providing dependencies (objects or services) to a class through its constructor or setter methods. In Laravel, the service container acts as the central registry for managing dependencies.
How It Works:

Middleware Definition: You define your middleware class extending the Illuminate\Http\Middleware\BaseMiddleware class.
Dependency Injection: Within the middleware's constructor, you can use type hinting to specify the dependencies your middleware needs. Laravel will automatically resolve these dependencies using the service container.
Resolving Dependencies: When your middleware is registered and a request triggers it, Laravel utilizes the service container to retrieve the required dependencies based on the type hints in the constructor.


# What is the illuminate 
simply is a huge components library(PHP framework) that contains powerful services to the laravel like
-Routing
-Database interactions (Eloquent ORM)
-Authentication and authorization
-Templating (Blade)
-Form handling
-Validation
-Caching
-Queueing
-Event handling
-Much more


and it uses the namespacing to access the class or services in it like when you need to use request you use
At the command prompt, type `use illuminate\Http\Middleware`.



# When you to exclude a middleware from a group of middlewares in route file you can use method *** ->withoutMiddleware()***
Code : 
`
    Route::middleware([EnsureTokenIsValid::class])->group(function () {
    Route::get('/', function () {
    });
        Route::get('/profile', function () {
            // ...
        })->withoutMiddleware([EnsureTokenIsValid::class]);
});
`

*** OR *** 

`
    use App\Http\Middleware\EnsureTokenIsValid;
    Route::withoutMiddleware([EnsureTokenIsValid::class])->group(function () {
    Route::get('/profile', function () {
    });
    });
`

    The withoutMiddleware method can only remove route middleware and does not apply to global middleware.


# to assign a middleware as a global one there are two methods 
-  Modern Way Using *Kenranl.php file* 
    - Create Your Middleware Class
    - Register the middleware globally in kernal.php $middleware
-  Legacy Way *boatstrap\app.php* 
    - Create Your Middleware Class 
    - define it in the boatstrap\app.php
