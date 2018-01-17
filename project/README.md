# Symfony 4 Project

## Doctrine ORM (Optional)
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
                host: 'db' #docker name, for instance ('db', 'dockersymfonypoc_db_1')
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
