
# Creating Models and REST API in PHP Laravel

## 1. Creating Models in Laravel

To create models in Laravel, you can use the `artisan` command:

### Step 1: Create a Model
To create a new model, run the following command:
```bash
php artisan make:model ModelName
```

This will generate a basic model file located in the `app/Models` directory (in recent Laravel versions).

### Step 2: Create Model with Migration
To generate a model along with a migration file for database schema creation:
```bash
php artisan make:model ModelName -m
```
This will create:
- `app/Models/ModelName.php`
- `database/migrations/xxxx_xx_xx_create_model_name_table.php`

### Step 3: Define Relationships (Optional)
If your model needs relationships (e.g., one-to-many, many-to-many), define them within the model:
```php
public function relationshipName()
{
    return $this->hasMany(RelatedModel::class);
}
```

### Step 4: Use UUID or ULID (Optional)
To use UUID or ULID in your models, override the key generation in your model class.

For UUID:
```php
use Illuminate\Support\Str;

class ModelName extends Model
{
    public static function boot()
    {
        parent::boot();
        static::creating(function ($model) {
            $model->id = (string) Str::uuid();
        });
    }
}
```

For ULID:
```php
use Illuminate\Support\Str;

class ModelName extends Model
{
    public static function boot()
    {
        parent::boot();
        static::creating(function ($model) {
            $model->id = (string) Str::ulid();
        });
    }
}
```

---

## 2. Creating REST API in Laravel

### Step 1: Set Up Routes
Define the API routes in `routes/api.php`:
```php
Route::get('/modelname', [ModelNameController::class, 'index']);
Route::get('/modelname/{id}', [ModelNameController::class, 'show']);
Route::post('/modelname', [ModelNameController::class, 'store']);
Route::put('/modelname/{id}', [ModelNameController::class, 'update']);
Route::delete('/modelname/{id}', [ModelNameController::class, 'destroy']);
```

### Step 2: Create Controller
Generate a controller using the artisan command:
```bash
php artisan make:controller ModelNameController
```

### Step 3: Define CRUD Operations in Controller
Implement the CRUD operations inside the controller methods:
```php
public function index() {
    return ModelName::all();
}

public function show($id) {
    return ModelName::findOrFail($id);
}

public function store(Request $request) {
    $model = ModelName::create($request->all());
    return response()->json($model, 201);
}

public function update(Request $request, $id) {
    $model = ModelName::findOrFail($id);
    $model->update($request->all());
    return response()->json($model, 200);
}

public function destroy($id) {
    ModelName::destroy($id);
    return response()->json(null, 204);
}
```

### Step 4: Enable Mass Assignment (Optional)
Make sure to define the `$fillable` property in your model to allow mass assignment:
```php
protected $fillable = ['column1', 'column2', 'column3'];
```

### Step 5: Test Your API
You can use tools like [Postman](https://www.postman.com/) or `curl` to test your API.

Example using `curl`:
```bash
curl -X POST http://your-app-url/api/modelname -d "key1=value1&key2=value2"
```

---

### Optional: Authentication with JWT
If you want to secure your API, you can implement JWT authentication.

### Step 1: Install the JWT Package
```bash
composer require tymon/jwt-auth
```

### Step 2: Publish the Configuration
```bash
php artisan vendor:publish --provider="Tymon\JWTAuth\Providers\LaravelServiceProvider"
```

### Step 3: Generate JWT Secret
```bash
php artisan jwt:secret
```

### Step 4: Use Middleware for Protecting Routes
Add the JWT middleware to your routes to secure them:
```php
Route::middleware('auth:api')->group(function () {
    Route::get('/user', [UserController::class, 'getUser']);
});
```
