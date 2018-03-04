# Docker development for symfony project

## Images

- node:9.6-alpine
- php:7.2.0-apache
- mysql:5.7
- phpmyadmin/phpmyadmin

## Prerequisites / Requirements

- Docker (Tested with version 1.13.1)
- docker-compose (Tested with version 1.11.1)

## Usage
1. Build:

        docker-compose build
        
2. Create react App into "react" container (first)

        docker-compose run react create-react-app .


3. Up (-d : background):

        docker-compose up -d

4. Create Symfony 4 project into "webserver" container:

        docker-compose exec webserver composer create-project symfony/skeleton .

5. Enjoy:

    http://localhost:9000/
    

## Docker tricks

Stop && remove containers
    
    docker-compose down

Verbose
    docker-compose --verbose up
     

