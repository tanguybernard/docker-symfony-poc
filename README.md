# Docker development for symfony project

## Images

- php:7.2.0-apache
- mysql:5.7
- phpmyadmin/phpmyadmin


## Prerequisites / Requirements

- Docker (Tested with version 1.13.1)
- docker-compose (Tested with version 1.11.1)

## Usage
Build:

    docker-compose build
Up (-d : background):

    docker-compose up -d

Create Symfony 4 project into "webserver" container:

    docker-compose exec webserver composer create-project symfony/skeleton skeleton

Move skeleton to DirectoryRoot:

    docker-compose exec webserver rsync -ua --delete-after skeleton/ .

Enjoy:

    http://localhost:9000/