### 1. Create, your container

    docker-compose up -d


### 2. Api Container

    docker-compose exec api composer req api cors annotations form doctrine jwt-auth security

### 4. Into the container, generate RSA pair key

    mkdir -p config/jwt # For Symfony3+, no need of the -p option
    openssl genrsa -out config/jwt/private.pem -aes256 4096
    openssl rsa -pubout -in config/jwt/private.pem -out config/jwt/public.pem 
