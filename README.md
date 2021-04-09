# Docker images for Laravel development
[![Travis](https://img.shields.io/travis/tonyyb/docker-laravel-nginx.svg?maxAge=1800&style=flat-square)](https://travis-ci.org/tonyyb/docker-laravel-nginx)

## Requirements

These images requires **Docker** and **Docker Compose**.

## Installation

1. Copy `docker-compose.yml` file to your laravel project root path, and edit it according to your needs ;

2. Copy content of `.env.example` file and put it into your laravel `.env` file with desired values ;

3. From your project directory, start up your application by running:

```sh
docker-compose up
```

## Docker Images

These docker images are configured in `docker-compose.yml` file. 
You can comment or uncomment some services according to your project.

* [`tonyyb/laravel-php:7.2`](https://hub.docker.com/r/tonyyb/laravel-php/)
* [`tonyyb/laravel-php:7.3`](https://hub.docker.com/r/tonyyb/laravel-php/)
* [`tonyyb/laravel-php:7.4`](https://hub.docker.com/r/tonyyb/laravel-php/)
* [`tonyyb/laravel-php:8.0`](https://hub.docker.com/r/tonyyb/laravel-php/)
* [`tonyyb/laravel-nginx:latest`](https://hub.docker.com/r/tonyyb/laravel-nginx/)
* [`mysql:5.7`](https://hub.docker.com/_/mysql/) ;

## Contributing

Contributions are welcome!
Leave an issue on Github, or create a Pull Request.

## Licence

This work is under [MIT](LICENCE) licence.
