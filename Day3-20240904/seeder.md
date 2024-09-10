# seeder

- Why Use Seeders?

    - Testing: Seeders can create dummy data to test the functionality of your application.
    - Development: They help developers by providing a sample data set, making it easier to work on features that require data.
    - Initial Setup: Seeders can be used to set up default data for new installations of your application.


## How to Create and Use Seeders
1. Creating a Seeder

    - php artisan make:seeder UsersTableSeeder

    - This command generates a seeder file in the database/seeders directory. The file will be named UsersTableSeeder.php.

2. Defining Seeder Logic

    - Open the newly created seeder file (UsersTableSeeder.php) and add logic to insert data into the database. For example:
    - 
    - 
    - <?php
    - 
    - namespace Database\Seeders;
    - 
    - use Illuminate\Database\Seeder;
    - use Illuminate\Support\Facades\DB;
    - use Illuminate\Support\Facades\Hash;
    - 
    - class UsersTableSeeder extends Seeder
    - {
    -     public function run()
    -     {
    -         DB::table('users')->insert([
    -             'name' => 'John Doe',
    -             'email' => 'john@example.com',
    -             'password' => Hash::make('password'),
    -         ]);
    -     }
    - }
    - 
    - In this example, we are inserting a single record into the users table.

3. Running Seeders

    - php artisan db:seed

    - To run the seeders, you use the Artisan command:
    - 
    - This command runs all seeders defined in the DatabaseSeeder class. You can also specify a specific seeder class to run:
    - 
    - php artisan db:seed --class=UsersTableSeeder

