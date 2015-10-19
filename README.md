Docker image for php apache for cake-php apps 
=====

Since CakePHP apps require MySQL PDO to be installed,
I found this to be a very time-consuming. I spent around 5 hours to get this
properly configured. CakePHP requires the following:

* Apache Module: Rewrite: http://httpd.apache.org/docs/current/mod/mod_rewrite.html
* Apache Module: Headers: http://httpd.apache.org/docs/2.2/mod/mod_headers.html
* PHP Module: MySQL PDO: http://php.net/manual/en/pdo.installation.php, http://stackoverflow.com/questions/13375061/installing-pdo-driver-on-mysql-linux-server

This image's parent is the latest PHP/Apache image. See more at https://hub.docker.com/_/php/.

Here's a Dockerfile that will work for your CakePHP Application.

```
FROM marcellodesales/php-apache-cakephp-mysql

ADD . /var/www/html

# In case you need write permissions in a given directory, do it here
RUN mkdir /var/www/html/api/tmp && chmod 777 /var/www/html/api/tmp

CMD ["apache2-foreground"]
```

After that, just perform a regular build:

```sh
docker build -t myPhpApp .
```
