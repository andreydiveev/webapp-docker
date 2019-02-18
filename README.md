### Install

```bash
git clone https://github.com/andreydiveev/laravel-docker
cd laravel-docker
docker-composer up -d
docker-compose exec php composer install
docker-compose exec php cp .env.example .env
docker-compose exec php php artisan key:generate
```

Open http://localhost/.
