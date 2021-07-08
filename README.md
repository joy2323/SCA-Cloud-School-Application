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


3. After creating the Dockerfile, I created the Docker image. From my terminal, I navigate to the root folder of my project and ran:-

        docker build -t sca-cloud-school-application .

# Where the -t is used to specify the tag/name of the Docker image, and  the dot (.) means the current folder will be used as the context for the image to be built.

4. After building the Docker image (sca-cloud-school-application) I ran it using:-

            docker run -p 8000:8000 -d sca-cloud-school-application


5. The application can be accessed from the browser at  http://localhost:8000/


Docker Hub Link

https://hub.docker.com/repository/docker/oluebubechukwu/sca-cloud-school-application