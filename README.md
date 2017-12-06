# Docker development for symfony project

## Images

- php:7.2.0-apache
- mysql:5.7
- phpmyadmin/phpmyadmin


## Prerequisites / Requirements

- Docker (Tested with version 1.13.1)
- docker-compose (Tested with version 1.11.1)

## Usage
1. Build:

    docker-compose build
2. Up (-d : background):

    docker-compose up -d

3. Create Symfony 4 project into "webserver" container:

    docker-compose exec webserver composer create-project symfony/skeleton skeleton

4. Move skeleton to DirectoryRoot:

    docker-compose exec webserver rsync -ua --delete-after skeleton/ .

5. Enjoy:

    http://localhost:9000/