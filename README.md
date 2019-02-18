### Install

```bash
git clone https://github.com/andreydiveev/webapp-docker
cd webapp-docker
mkdir -p src/public
```

### WebRoot

```
\--- webapp-docker
     \--- src
          \--- public
               \--- index.php
```

### Starting
```bash
docker-composer up -d
docker-compose exec php composer install
docker-compose exec php cp .env.example .env
docker-compose exec php php artisan key:generate
```

Open http://localhost/.
