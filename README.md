# Docker development for symfony project

## Images

- php:7.2.0-apache
- mysql:5.7
- phpmyadmin/phpmyadmin
- willdurand/elk


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
    
## Symfony 4 Project

### Doctrine ORM (Optional)
1. Require package:
    
    composer require doctrine maker
2. Create entity:

    php bin/console make:entity Product

3. Configuration (config/doctrine.yaml)
    ```
    parameters:
        
        env(DATABASE_URL): ''
        doctrine:
            dbal:
                # configure these for your database server
                dbname: 'your_database_name'
                host: db #docker name
                port: 3306
                user: 'your_user_name'
                password: 'your_user_pass'
                driver: 'pdo_mysql'
            orm:
                auto_generate_proxy_classes: '%kernel.debug%'
                naming_strategy: doctrine.orm.naming_strategy.underscore
                auto_mapping: true
                mappings:
                    App:
                        is_bundle: false
                        type: annotation
                        dir: '%kernel.project_dir%/src/Entity'
                        prefix: 'App\Entity'
                        alias: App
    ```
    
