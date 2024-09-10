# Redis

### Connect the redis with laravel

1. set this in .env

    - REDIS_CLIENT=predis
    - REDIS_HOST=127.0.0.1
    - REDIS_PASSWORD=null
    - REDIS_PORT=6379
    - 
    - FILESYSTEM_DRIVER=s3

2. add predis as depandency
    - composer require predis

3. then define the routes in web.php
    - 
    - Route::get('/redis',function(){
    -     Redis::set('todo_test', 'Hello, Redis!');
    -     return Redis::get('todo_test');
    - });
    - 

4. if still not working so go to the database.php of config and update the redis

5. check the proper connection with docker