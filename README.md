## Run mono web applications with apacke mod_mono

This repository contains Dockerfile for publishing Docker's automated build to the public [Docker Hub Registry](https://registry.hub.docker.com/).

> Apache is exposed from the container on port 80 and the mono-fastcgi-server4 loads the application from /var/www.

### Base docker image

    debian/jessie

### Usage

First you need to pull the image:

    docker pull seif/docker-mono-apache

Then build your project, create a Dockerfile, copy the application to /var/www and start runit:

    FROM seif/docker-mono-apache
    ADD buildOutput/website /var/www/
    CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

Build your container

    docker build -t my_website .

Run it, forwarding the host's port 8080 to the container's port 80

    docker run --rm -i -t -p 8080:80 my_website

You should now be able to access the site on [your local machine port 8080](http://localhost:8080/)
