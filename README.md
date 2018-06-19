# Matte ma raquette

[![Join the chat at https://gitter.im/poudre-aux-yeux/matte-ma-raquette](https://badges.gitter.im/poudre-aux-yeux/matte-ma-raquette.svg)](https://gitter.im/poudre-aux-yeux/matte-ma-raquette?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

## Ecosystem

**Back-end:**

[rAPIquette](https://github.com/poudre-aux-yeux/rapiquette): GraphQL API

**Front-ends:**

[MonArbitreRaquette](https://github.com/poudre-aux-yeux/mon-arbitre-raquette):
Web application for the referee

[MatteMaRaquette](https://github.com/poudre-aux-yeux/ATP_LIVE):
Web application to watch the live scores and results

[GereMaRaquette](https://github.com/poudre-aux-yeux/mon-admin-raquette):
Back-office Web application to administrate accounts, players, matches, stadiums...

## Development

Develop with Docker Compose.

To develop an UI :

```sh
# API
docker-compose up api
```

In your UI, hit `http://127.0.0.1/graphql`.

To just run an UI :

```sh
docker-compose up
```

And hit the UI you want to browse.

## Kubernetes

Apply the latest k8s configuration (this will not pull the latest images)

```sh
kubectly apply -f k8s
```

To manually update a Docker image, delete the out-of-date deployment and apply
the k8s config again.

# Setup the CI

## Docker

Setup your Dockerfile and make sure it works.

Try building it:

```sh
docker build -t [docker hub repo]:latest .
```

for exemple: `docker build -t poudreauxyeux/rapiquette:latest`.

and pushing it:

```sh
docker push [docker hub repo]:latest
```

## Travis CI

Create a `.travis.yml` file at the root of your project :

```yml
sudo: required

services:
  - docker

env:
  - IMAGE_COMMIT=[docker hub repo]:$TRAVIS_COMMIT
  - IMAGE_LATEST=[docker hub repo]:latest

before_install:
  - docker login -u "$DOCKER_USERNAME" -p "$DOCKER_PASSWORD"

script:
  - docker build -t $IMAGE_COMMIT -t $IMAGE_LATEST .

after_success:
  - docker push $IMAGE_COMMIT
  - docker push $IMAGE_LATEST
```

Navigate to https://travis-ci.org/, and activate Travis CI for your repository.
In the project settings on Travis CI, setup the two environment variables:
`DOCKER_USERNAME` and `DOCKER_PASSWORD`.
