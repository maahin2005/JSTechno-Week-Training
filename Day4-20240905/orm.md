# Eloquent ORM

1. Retrieving All Records/data
    - To retrieve all records from a table
    - `$users = User::all();`

2. Retrieving a Single Record/data
    - To retrieve a single record using `find()` or `first()`:

    - `$user = User::find(1);`  // Find by primary key
        - find() retrieves a model by its primary key.

    - `$user = User::where('email', 'example@example.com')->first();`  // Find by condition
        - first() retrieves the first record that matches the query.

3. Using `where` Clauses
    - Eloquent allows you to add conditions:
    -  `$users = User::where('status', 'active')->get();`  // Get all active users

4. Retrieving Specific Columns
    - we can limit the columns selected from the database:
    - `$users = User::select('name', 'email')->get();`
    - This retrieves only the name and email columns.

5. Chunking Results
    - dealing with large datasets, chunking helps by processing the data in smaller chunks:
    -  User::chunk(100, function ($users) {
            foreach ($users as $user) {
                // Process each user
            }
        });
    - This processes 100 users at a time, which prevents memory issues.

7. andWhere:
    - In Laravel, there's no explicit andWhere() method because where() acts as an implicit "AND". Each where() call adds conditions using the logical "AND" operator.

    - Example:
    - `$users = User::where('status', 'active')->where('age', '>', 18)->get();`
    - This query retrieves users where status is 'active' and age is greater than 18

8. orWhere
    - orWhere() adds an "OR" condition to your query.
    - 
    - Example:
    - `$users = User::where('status', 'active')->orWhere('age', '>', 18)->get();`
    - This query retrieves users who are either active or have an age greater than 18.

9. pivot
    - Pivot is used in many-to-many relationships to access the intermediate table (pivot table). When using a belongsToMany relationship, we often need to access columns from the pivot table.
    - 
    - Example: Suppose User and Role have a many-to-many relationship. You can access the pivot table like this:
    - 
    - $roles = User::find(1)->roles;
    - foreach ($roles as $role) {
    -     echo $role->pivot->created_at;  // Access pivot table's 'created_at' column
    - }

10. pluck
    - pluck() retrieves a single column's values from a collection or database result, returning them as an array.
    - 
    - Example:
    - `$names = User::pluck('name');`
    - This returns an array of all user names.
    - Using with key-value pairs:
        - `$names = User::pluck('name', 'id');`
        - This returns an associative array where the keys are user IDs and the values are the corresponding names.
        
11. select
    - select() allows you to specify which columns you want to retrieve from the database.
    - 
    - Example:
    - `$users = User::select('name', 'email')->get();`
    - This retrieves only the name and email columns from the users' table.

12. toArray
    - toArray() converts a collection or model instance into a plain PHP array.
    - 
    - Example:
    - `$user = User::find(1)->toArray();`
    - This converts the user model instance into an array.

13. first
    - first() retrieves the first record that matches the query conditions.
    - 
    - Example:
    - 
    - `$user = User::where('email', 'example@example.com')->first();`
    - This retrieves the first user with the specified email.

14. latest
    - latest() orders the results by the most recently created or updated records, based on the created_at column by default.
    - 
    - Example:
    - `$latestUser = User::latest()->first();`
    - This retrieves the most recently created user.

15. orderBy
    - orderBy() orders the results by a specified column, in either ascending or descending order.
    - 
    - Example:
    - `$users = User::orderBy('name', 'asc')->get();`
    - This orders users by name in ascending order.
    - Descending Order:
    - $users = User::orderBy('created_at', 'desc')->get();
    - This orders users by creation date in descending order.

16. groupBy
    - groupBy() groups the results by a specified column. It’s often used with aggregate functions like count(), sum(), etc.
    - 
    - Example:
    - $users = User::select('status', DB::raw('count(*) as total'))
    -              ->groupBy('status')
    -              ->get();
    - This groups users by status and counts the total number of users for each status.