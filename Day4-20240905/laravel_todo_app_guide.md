
# Laravel To-Do Application Setup Guide

This guide will walk you through the steps to create a simple To-Do application using Laravel and MySQL.

## Prerequisites
Make sure you have the following installed:
- Composer
- PHP
- MySQL

---

## Step 1: Install Laravel
To install a fresh Laravel project, run the following command:
```bash
composer create-project --prefer-dist laravel/laravel todo-app
```

---

## Step 2: Set Up MySQL Connection
1. Open the `.env` file in the root of your project and configure the database settings:
```bash
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=todo_database
DB_USERNAME=root
DB_PASSWORD=root
```

2. Create the database:
```sql
CREATE DATABASE todo_database;
```

---

## Step 3: Create Model, Migration, and Controller
Run the following command to create a `Todo` model, migration, and controller:
```bash
php artisan make:model Todo -mcr
```

---

## Step 4: Define the Database Schema
Edit the migration file (`database/migrations/xxxx_xx_xx_create_todos_table.php`):
```php
public function up()
{
    Schema::create('todos', function (Blueprint $table) {
        $table->id();
        $table->string('title');
        $table->boolean('completed')->default(false);
        $table->timestamps();
    });
}
```
Run the migration to create the table:
```bash
php artisan migrate
```

---

## Step 5: Define the Todo Model
In the `app/Models/Todo.php` file, define the fillable fields:
```php
class Todo extends Model
{
    protected $fillable = ['title', 'completed'];
}
```

---

## Step 6: Set Up Routes
In `routes/web.php`, define the routes for the to-do operations:
```php
use App\Http\Controllers\TodoController;

Route::get('/', [TodoController::class, 'index'])->name('todos.index');
Route::post('/todos', [TodoController::class, 'store'])->name('todos.store');
Route::put('/todos/{todo}', [TodoController::class, 'update'])->name('todos.update');
Route::delete('/todos/{todo}', [TodoController::class, 'destroy'])->name('todos.destroy');
```

---

## Step 7: Create Controller Methods
In `app/Http/Controllers/TodoController.php`, define the CRUD methods:
```php
use App\Models\Todo;
use Illuminate\Http\Request;

class TodoController extends Controller
{
    public function index()
    {
        $todos = Todo::all();
        return view('todos.index', compact('todos'));
    }

    public function store(Request $request)
    {
        $request->validate(['title' => 'required|max:255']);
        Todo::create(['title' => $request->title]);
        return redirect()->route('todos.index');
    }

    public function update(Request $request, Todo $todo)
    {
        $todo->update(['completed' => $request->has('completed')]);
        return redirect()->route('todos.index');
    }

    public function destroy(Todo $todo)
    {
        $todo->delete();
        return redirect()->route('todos.index');
    }
}
```

---

## Step 8: Create Views
1. Create the view directory: `resources/views/todos/`.
2. Create an `index.blade.php` file in `resources/views/todos/`:
```html
<!DOCTYPE html>
<html>
<head>
    <title>Todo List</title>
</head>
<body>
    <h1>Todo List</h1>

    <form action="{{ route('todos.store') }}" method="POST">
        @csrf
        <input type="text" name="title" placeholder="New Todo">
        <button type="submit">Add Todo</button>
    </form>

    <ul>
        @foreach($todos as $todo)
            <li>
                <form action="{{ route('todos.update', $todo->id) }}" method="POST">
                    @csrf
                    @method('PUT')
                    <input type="checkbox" name="completed" {{ $todo->completed ? 'checked' : '' }} onchange="this.form.submit()">
                    {{ $todo->title }}
                </form>
                
                <form action="{{ route('todos.destroy', $todo->id) }}" method="POST" style="display:inline;">
                    @csrf
                    @method('DELETE')
                    <button type="submit">Delete</button>
                </form>
            </li>
        @endforeach
    </ul>
</body>
</html>
```

---

## Step 9: Run the Application
Run the Laravel development server:
```bash
php artisan serve
```

Visit `http://127.0.0.1:8000/` to see your To-Do application.

---

## Optional: Add Bootstrap for Styling
To add some basic styling, include Bootstrap in your `index.blade.php`:
```html
<head>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
```

---

That's it! You've successfully built a simple To-Do application with Laravel.
