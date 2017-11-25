# brimir-docker
Ready to use docker box for [Brimir open source ticket manager](https://github.com/ivaldi/brimir).

# Architecture
This docker box contains only Brimir Rails application. Nginx, database or any other
service not included because 'put everything into one box' architecture isn't what
docker is made for.

Minimal requirements for a working app you need a working [mysql docker](https://hub.docker.com/_/mysql/)
box and link it to Brimir box. This isn't a complicated task and I made a
[docker-compose](https://docs.docker.com/compose/) configuration for you to build it.

In production use I also recommend an [nginx](https://hub.docker.com/_/nginx/).
Meybe I will do docker-compose config later for it.

# How to use this image
```
$ docker run --name my-brimir -e MYSQL_HOST=localhost -e MYSQL_DATABASE=brimir -e MYSQL_USER=brimir -e MYSQL_ROOT_PASSWORD=my-secret-pw -d kepes/brimir-docker
```

## Login info

* Username: agent@getbrimir.com
* Password: tmppwd

## Environment variables

Name                | Default             | Value
------------------- | ------------------- | -------------
POSTGRES_HOST       | postgreql           | Postgresql server hostname
POSTGRES_DATABASE   | -                   | Postgresql database name
POSTGRES_USER       | -                   | Postgresql database username
POSTGRES_PASSWORD   | -                   | Postgresql Password
UNICORN_WORKERS     | 2                   | Number of Unicorn workers
UNICORN_TIMEOUT     | 30                  | Timeout of unicorn
UNICORN_PORT        | 3000                | Unicorn port number
RAILS_ENV           | production          | Rails environment
SECRET_KEY_BASE     | change_it_please    | Secret key base for Rails
SMTP_ADDRESS        | -                   | SMTP server address
SMTP_PORT           | -                   | SMTP port
SMTP_DOMAIN         | -                   | Domain name for SMTP HELLO
SMTP_USERNAME       | -                   | SMTP username
SMTP_PASSWORD       | -                   | SMTP password
SMTP_AUTHENTICATION | palin               | SMTP auth type

## Use it with `docker-compose`

[docker-compose.yml](https://github.com/kepes/brimir-docker/blob/master/docker-compose.yml)
```
$ git clone https://github.com/kepes/brimir-docker.git
$ docker-compose up
```

## Kubernetes

I made a [Kubernetes](http://kubernetes.io/) config (config/kubernetes_rc_brimir.yaml).
You can use it for configure a full functional Brimir service. Be careful and change all
necessary paramaters for your Kuberentes deployment!
