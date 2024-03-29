
[ https://laravel.com/docs/10.x#your-first-laravel-project ]

                        ___________

                        DEPENDENCES
                        ___________

#       ----------------------------
-       download && install composer:
#       ----------------------------

>       php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
>       php -r "if (hash_file('sha384', 'composer-setup.php') ==='55ce33d7678c5a611085589f1f3ddf8b3c52d662cd01d4ba75c0ee0459970c2200a51f492d557530c71c15d8dba01eae') { echo 'Installer verified'; } else { echo'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
>       php composer-setup.php
>       php -r "unlink('composer-setup.php');"

#       ---------------------------------------------------------------------------------------------------
-       put the composer.phar into a directory to simply call composer from any directory (Global install):
#       ---------------------------------------------------------------------------------------------------

>       sudo mv composer.phar /usr/local/bin/composer

#       ------------
-       Run composer
#       ------------

>       php composer.phar

#       --------------------
-       install Node and NPM
#       --------------------

        https://nodejs.org/en

                        _______

                        LARAVEL
                        _______

#       -----------------------------------------
-       create a new Laravel project via Composer
#       -----------------------------------------

>       composer create-project laravel/laravel <APP_NAME>

#       ------------------------------------------------------------------------------------------
-       Or create a new Laravel projects by globally installing the Laravel installer via Composer
#       ------------------------------------------------------------------------------------------

>       composer global require laravel/installer
>       laravel new <APP_NAME>

#       --------------------------------------------------------------------------------------
-       start Laravel's local development server using the Laravel's Artisan CLI serve command
#       --------------------------------------------------------------------------------------

>       cd <APP_NAME>
>       php artisan serve

>       http://localhost:8000. 

                        _____________________

                        DATABASE & MIGRATIONS
                        _____________________

#       --------------------------------------------------------------------------------------
-       Run application's database migrations, which will create application's database tables
#       --------------------------------------------------------------------------------------
>       php artisan migrate

