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
