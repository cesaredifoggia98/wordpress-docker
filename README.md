# Wordpress Docker Ecosystem

Docker Compose
==============
![Docker Compose](Moby-logo.png?raw=true "Docker Compose Logo")

Compose is a tool for defining and running multi-container Docker applications.
With Compose, you use a Compose file to configure your application's services.
Then, using a single command, you create and start all the services
from your configuration. To learn more about all the features of Compose
see [the list of features](https://github.com/docker/docker.github.io/blob/master/compose/index.md#features).

Compose is great for development, testing, and staging environments, as well as
CI workflows. You can learn more about each case in
[Common Use Cases](https://github.com/docker/docker.github.io/blob/master/compose/index.md#common-use-cases).

Using Compose is basically a three-step process.

1. Define your app's environment with a `Dockerfile` so it can be
reproduced anywhere.
2. Define the services that make up your app in `docker-compose.yml` so
they can be run together in an isolated environment.
3. Lastly, run `docker-compose up` and Compose will start and run your entire app.

A `docker-compose.yml`

    version: '3.3'

    services:
    db:
        image: mysql:5.7
        volumes:
        - db_data:/var/lib/mysql
        restart: always
        environment:
        MYSQL_ROOT_PASSWORD: *******
        MYSQL_DATABASE: *******
        MYSQL_USER: ******
        MYSQL_PASSWORD: *******

    wordpress:
        depends_on:
        - db
        image: wordpress:latest
        ports:
        - "8000:80"
        restart: unless-stopped
        volumes:
        - ./wp-content:/var/www/html/wp-content
        environment:
        WORDPRESS_DB_HOST: db:3306
        WORDPRESS_DB_USER: wordpress
        WORDPRESS_DB_PASSWORD: wordpress
        WORDPRESS_DB_NAME: wordpress
    volumes:
        db_data: {}

For more information about the Compose file, see the
[Compose file reference](https://github.com/docker/docker.github.io/blob/master/compose/compose-file/compose-versioning.md).

Compose has commands for managing the whole lifecycle of your application:

 * Start, stop and rebuild services
 * View the status of running services
 * Stream the log output of running services
 * Run a one-off command on a service

Installation and documentation
------------------------------

- Full documentation is available on [Docker's website](https://docs.docker.com/compose/).
- Code repository for Compose is on [GitHub](https://github.com/docker/compose).
- If you find any problems please fill out an [issue](https://github.com/docker/compose/issues/new/choose). Thank you!

Contributing
------------

[![Build Status](https://ci-next.docker.com/public/buildStatus/icon?job=compose/master)](https://ci-next.docker.com/public/job/compose/job/master/)

Want to help build Compose? Check out our [contributing documentation](https://github.com/docker/compose/blob/master/CONTRIBUTING.md).

Releasing
---------

Releases are built by maintainers, following an outline of the [release process](https://github.com/docker/compose/blob/master/project/RELEASE-PROCESS.md).

Wordpress in docker container
---------
In this container there is an wordpress image and to start the container the only action is to run this command 

    composer-dump up

File structure
---------
    -wp-content : In this folder there was all theme file , plugins  all wordpress content.

    -docker-compose.yml