# S3 with minio

### How to upload file using s3 and minio?

## Steps:

1. Start Docker and connect minio
 or 
1. run this cmd:
    - docker run -p 9000:9000 -p 9001:9001 --name minio -e "MINIO_ROOT_USER=minioadmin" -e "MINIO_ROOT_PASSWORD=minioadmin" minio/minio server /data --console-address ":9001"

2. Configure Laravel Filesystem for MinIO
    - go to .env and setup this
    
    - AWS_ACCESS_KEY_ID=minioadmin
    - AWS_SECRET_ACCESS_KEY=minioadmin
    - AWS_DEFAULT_REGION=us-east-1
    - AWS_BUCKET=my-bucket
    - AWS_URL=http://localhost:9000
    - AWS_ENDPOINT=http://localhost:9000/<bucket-name> # This should include the bucket name in the URL

3. set the filesystem.php
    - 'disks' => [
        - 's3' => [
        -     'driver' => 's3',
        -     'key' => env('AWS_ACCESS_KEY_ID'),
        -     'secret' => env('AWS_SECRET_ACCESS_KEY'),
        -     'region' => env('AWS_DEFAULT_REGION'),
        -     'bucket' => env('AWS_BUCKET'),
        -     'url' => env('AWS_URL'),
        -     'endpoint' => env('AWS_ENDPOINT'), // Important for MinIO
        -     'use_path_style_endpoint' => true, // Enable path-style for MinIO
        - ],
        ],

4. in controller set this 
    - Storage::disk('s3')->put('example.txt', 'Hello, MinIO!');

5. install package:
    - composer require league/flysystem-aws-s3-v3 "^3.0"

extra:

- php artisan config:cache


