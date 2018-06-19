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

To debug an UI :

```sh
# API
docker-compose up api
# Proxy
docker run -d -p 8888:8888 -e API_HOST=localhost:3333 poudreauxyeux/mattemaraquette
```

All the requests to the API should hit http://127.0.0.1:8888/graphql.

## Deployment

```Dockerfile
FROM poudreauxyeux/mattemaraquette
COPY dist .
ENV PORT=80
ENTRYPOINT ["/root/server"]
EXPOSE 80
```

## Kubernetes

Apply the latest k8s configuration (this will not pull the latest images)

```sh
kubectly apply -f k8s
```

To manually update a Docker image, delete the out-of-date deployment and apply
the k8s config again.
