# Middleware

1. Authenticate Middleware
    - This middleware is responsible for checking if a user is authenticated before accessing certain routes.
    - Path: app/Http/Middleware/Authenticate.php
    - Example:
    - 
    - public function handle($request, Closure $next, ...$guards)
    - {
    -     if (Auth::guard($guards)->guest()) {
    -         return redirect()->route('login');
    -     }
    -     return $next($request);
    - }

2. ThrottleRequests Middleware
    - Limits the number of requests a user can make to a route within a certain period of time, often used to protect against abuse or DDoS attacks.
    - Path: app/Http/Middleware/ThrottleRequests.php
    - Example:
    - public function handle($request, Closure $next, $maxAttempts = 60, $decayMinutes = 1)
    - {
    -     // Throttling logic here
    -     return $next($request);
    - }

3. VerifyCsrfToken Middleware
    - Protects the application from cross-site request forgery (CSRF) attacks by ensuring that a valid CSRF token is included with every request.
    - Path: app/Http/Middleware/VerifyCsrfToken.php
    - Example:
    - public function handle($request, Closure $next)
    - {
    -     if ($this->isReading($request) || $this->inExceptArray($request) || $this->tokensMatch($request)) {
    -         return $next($request);
    -     }
    -     throw new TokenMismatchException;
    - }

4. EncryptCookies Middleware
    - Automatically encrypts cookies sent to the user and decrypts them when received.
    - Path: app/Http/Middleware/EncryptCookies.php
    - Example:
    - public function handle($request, Closure $next)
    - {
    -     return $next($request);
    - }

5. RedirectIfAuthenticated Middleware
    - Redirects authenticated users away from routes intended only for guests (e.g., login, registration pages).
    - Path: app/Http/Middleware/RedirectIfAuthenticated.php
    - Example:
    - public function handle($request, Closure $next, $guard = null)
    - {
    -     if (Auth::guard($guard)->check()) {
    -         return redirect('/home');
    -     }
    -     return $next($request);
    - }

6. CheckForMaintenanceMode Middleware
    - Blocks access to the application when it's in maintenance mode.
    - Path: app/Http/Middleware/CheckForMaintenanceMode.php
    - Example:
    - public function handle($request, Closure $next)
    - {
    -     if (app()->isDownForMaintenance()) {
    -         throw new MaintenanceModeException;
    -     }
    -     return $next($request);
    - }

7. TrimStrings Middleware
    - Automatically trims all the incoming string inputs in the request.
    - Path: app/Http/Middleware/TrimStrings.php
    - Example:
    - public function handle($request, Closure $next)
    - {
    -     $this->cleanStrings($request);
    -     return $next($request);
    - }

8. ConvertEmptyStringsToNull Middleware
    - Converts empty string fields in requests to null, which can be useful when storing data in a database.
    - Path: app/Http/Middleware/ConvertEmptyStringsToNull.php
    - Example:
    - public function handle($request, Closure $next)
    - {
    -     $this->convertEmptyStringsToNull($request);
    -     return $next($request);
    - }

9. SetLocale Middleware
    - Used to set the application's locale (language) based on user preferences, browser settings, or a route parameter.
    - Example:
    - public function handle($request, Closure $next)
    - {
    -     App::setLocale($request->getPreferredLanguage());
    -     return $next($request);
    - }

10. RoleMiddleware (Custom)
    - Restricts access to certain routes based on the user's role (e.g., admin, editor, etc.).
    - Example:
    - public function handle($request, Closure $next, $role)
    - {
    -     if (!Auth::check() || !Auth::user()->hasRole($role)) {
    -         abort(403);
    -     }
    -     return $next($request);
    - }

11. ForceHttps Middleware
    - Redirects all non-HTTPS traffic to HTTPS, ensuring that your site is served over a secure connection.
    - Example:
    - public function handle($request, Closure $next)
    - {
    -     if (!$request->secure()) {
    -         return redirect()->secure($request->getRequestUri());
    -     }
    -     return $next($request);
    - }

12. CorsMiddleware (Custom or Package)
    - Handles Cross-Origin Resource Sharing (CORS) settings, allowing requests from different domains.
    - Example:
    - public function handle($request, Closure $next)
    - {
    -     return $next($request)->header('Access-Control-Allow-Origin', '*');
    - }

13. CacheResponse Middleware
    - Caches responses for specific routes to improve performance by reducing database queries and processing time.
    - Example:
    - public function handle($request, Closure $next)
    - {
    -     return Cache::remember($request->url(), 60, function () use ($request, $next) {
    -         return $next($request);
    -     });
    - }

14. SanitizeInput Middleware (Custom)
    - Cleans or sanitizes input to remove harmful content (e.g., HTML tags, scripts) for security purposes.
    - Example:
    - public function handle($request, Closure $next)
    - {
    -     $input = array_map('strip_tags', $request->all());
    -     $request->merge($input);
    -     return $next($request);
    - }

15. AuthenticateWithBasicAuth Middleware
    - Authenticates users using HTTP Basic Authentication.
    - Example:
    - public function handle($request, Closure $next)
    - {
    -     return Auth::basic() ?: $next($request);
    - }

16. SubstituteBindings Middleware
    - Resolves route model bindings and dependency injections automatically based on route parameters.
    - Example:
    - public function handle($request, Closure $next)
    - {
    -     Route::substituteBindings($request);
    -     return $next($request);
    - }

17. HandleInertiaRequests Middleware
    - Used in Inertia.js-based applications to handle the Inertia requests and responses.
    - Example:
    - public function handle($request, Closure $next)
    - {
    -     return Inertia::handle($request, $next($request));
    - }

18. AuthenticateSession Middleware
    - Adds session authentication for user login and session-based auth.
    - Example:
    - public function handle($request, Closure $next)
    - {
    -     if (Auth::viaRemember()) {
    -         Auth::loginUsingId(Auth::user()->id);
    -     }
    -     return $next($request);
    - }
19. LogRequests Middleware (Custom)
    - Logs all incoming requests for debugging or audit purposes.
    - Example:
    - public function handle($request, Closure $next)
    - {
    -     \Log::info('Request:', ['url' => $request->url()]);
    -     return $next($request);
    - }

20. AdminMiddleware (Custom)
    - Restricts access to routes intended for administrators.
    - Example:
    - public function handle($request, Closure $next)
    - {
    -     if (Auth::user()->isAdmin()) {
    -         return $next($request);
    -     }
    -     abort(403);
    - }

21. SecureHeadersMiddleware (Custom or Package)
    - Adds security headers to the response (e.g., Content-Security-Policy, X-Frame-Options).
    - Example:
    - public function handle($request, Closure $next)
    - {
    -     $response = $next($request);
    -     return $response->header('X-Frame-Options', 'DENY')
    -                     ->header('Content-Security-Policy', "default-src 'self'");
    - }

22. VerifyUserEmail Middleware (Custom)
    - Ensures the user has verified their email before allowing access to certain routes.
    - Example:
    - public function handle($request, Closure $next)
    - {
    -     if (Auth::check() && !Auth::user()->hasVerifiedEmail()) {
    -         return redirect()->route('verification.notice');
    -     }
    -     return $next($request);
    - }

23. CheckAge Middleware (Custom)
    - Restricts access to routes based on a user's age.
    - Example:
    - public function handle($request, Closure $next)
    - {
    -     if (Auth::check() && Auth::user()->age < 18) {
    -         abort(403, 'You are too young to access this resource.');
    -     }
    -     return $next($request);
    - }

24. LogOutInactiveUsers Middleware (Custom)
    - Logs out users after a certain period of inactivity.
    - Example:
    - public function handle($request, Closure $next)
    - {
    -     if (Auth::check() && Auth::user()->isInactive()) {
    -         Auth::logout();
    -         return redirect()->route('login');
    -     }
    -     return $next($request);
    - }

25. RedirectIfVerified Middleware
    - Redirects users who have already verified their email from verification pages to the home/dashboard page.
    - Example:
    - public function handle($request, Closure $next)
    - {
    -     if (Auth::check() && Auth::user()->hasVerifiedEmail()) {
    -         return redirect()->route('home');
    -     }
    -     return $next($request);
    - }