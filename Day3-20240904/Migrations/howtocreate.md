# How to create migration file?

1. php artisan make:migration migration_name
    - for creating the migration
    - mention the name of migration whatever you want 
    - Instead of migration_name
    - ex. 
        - php artisan make:migration employee

2. after step 1 my migration will be created

3. go to the database folder
    - database/migrations
    - here you will find your newly created migration

4. Inside this file already class has been created
    - class will be like:
        `
             <?php

            use Illuminate\Database\Migrations\Migration;
            use Illuminate\Database\Schema\Blueprint;
            use Illuminate\Support\Facades\Schema;

            return new class extends Migration
            {
                /**
                 * Run the migrations.
                 */
                public function up(): void
                {
                    //
                }

                /**
                 * Reverse the migrations.
                 */
                public function down(): void
                {
                    //
                }
            };

        `

5. this class has up and down methods 

6. define the schema inside up method

7. Schema creation
    - ex. 
        - public function up(): void
        - {
        -     Schema::create('employees',function(Blueprint $table){
        -         $table->id();
        -         $table->string('empName');
        -         $table->string('department');
        -         $table->integer('salary');
        -         $table->timestamps();
        -     });
        - }

8. in down method do this:
    -  public function down(): void
        {
            Schema::dropIfExists('<name of your Schema>');
        }