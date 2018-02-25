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

## Encore

### Install 
``` 
yarn add @symfony/webpack-encore --dev 
```
``` 
yarn add node-sass
```
```
yarn add sass-loader
```
``` 
yarn add webpack-notifier
```

### Configuring Encore/Webpack

Create a new file called webpack.config.js at the root of your project.

_webpack.config.js_

```
    // webpack.config.js
    var Encore = require('@symfony/webpack-encore');

    Encore
        // the project directory where all compiled assets will be stored
        .setOutputPath('public/build/')

        // the public path used by the web server to access the previous directory
        .setPublicPath('/build')

        // will create public/build/app.js and public/build/app.css
        //.addEntry('app', './assets/js/app.js')

        .addStyleEntry('style', './assets/scss/style.scss')

        // allow sass/scss files to be processed
        .enableSassLoader()

        // allow legacy applications to use $/jQuery as a global variable
        .autoProvidejQuery()

        .enableSourceMaps(!Encore.isProduction())

        // empty the outputPath dir before each build
        .cleanupOutputBeforeBuild()

        // show OS notifications when builds finish/fail
        .enableBuildNotifications()

        // create hashed filenames (e.g. app.abc123.css)
        // .enableVersioning()
    ;

    // export the final configuration
    module.exports = Encore.getWebpackConfig();
```

### Example

_assets/scss/style.css_

```
//assets/scss/style.scss
@font-face {
    font-family: myFirstFont;
    src: url("fonts/BACKTO1982.ttf") format('truetype');//assets/fonts/BACKTO1982.ttf
}

p {
    font-family: myFirstFont;
    color: red;
}

```
_templates/base.html.twig_

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>{% block title %}Welcome !{% endblock %}</title>
        {% block stylesheets %}
            <link rel="stylesheet" href="{{ asset('build/style.css') }}">
        {% endblock %}
    </head>
    <body>
        {% block body %}
        <p>1982 Style font !!!</p>
        {% endblock %}
        {% block javascripts %}{% endblock %}
    </body>
</html>
```

### Run

Compile assets once

```
    yarn run encore dev
```

Recompile assets automatically when files change

```
    yarn run encore dev --watch
```
 
Compile assets but also minify & optimize them

```
    yarn run encore production
```