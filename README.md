### Install

```bash
git clone https://github.com/andreydiveev/webapp-docker
cd webapp-docker
mkdir -p src/public
```

### WebRoot

```
└📁webapp-docker
 └📁src
  └📁public
   ├ ...
   └📄index.php
```

### Starting
```bash
docker-compose up -d
docker-compose exec php composer install
docker-compose exec php cp .env.example .env
docker-compose exec php artisan key:generate
```

### PHP version:

To change PHP version set build path for php service `build: ./.docker/php/5.6` and rebuild vie command `docker-compose up -d --build`.
To check current PHP version run `docker-compose exec php php -v`.

### Composer:

Run `docker-compose exec php composer install`.

Open http://localhost/.
