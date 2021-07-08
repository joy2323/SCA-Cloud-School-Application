1. I created a laravel project "SCA-Cloud-School-Application"
2. Created a new Dockerfile file in the application directory and added the following commands

                FROM php:7.3.11-fpm
    ### This tells Docker to download and use the php:7.3.11-fpm image.


                RUN apt-get update -y && apt-get install -y libmcrypt-dev openssl
    ### Run apt-get to install the dependencies and extensions required by Laravel.


                RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
    ### For installing Composer

    
                RUN docker-php-ext-install pdo pdo_mysql sockets
    ### For install the dependencies that is required in the project.


                WORKDIR /app
                COPY . /app
    ### This tells Docker to set the working directory in the container to /app and copy the files (Laravel project) in my current folder (in my system host) to the /app folder in the container.

                RUN composer install
    ### If you didn't install the dependencies using the previous methods you can install them using the 'RUN composer install'.



                CMD php artisan serve --host=0.0.0.0 --port=8000
    ### This will serve the laravel project from port 8000

                EXPOSE 8000
    ###  For exposing the port 8000 from the container