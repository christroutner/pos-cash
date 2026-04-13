# Bitcoin Cash Point of Sale

BCH Point of Sale (https://pos.cash) is a non-custodial web-based point of sale client.
It requires no backend services to run other than simple web/http(s) hosting.

User configurations are stored client-side via localstorage.

The web application uses bitcoin.com, blockchain.info, and bitcoinverde.org for
payment alerts.

## Docker (Nginx)

Production Docker files live under `production/docker/`. The image is built by cloning
[this repository](https://github.com/christroutner/pos-cash) from GitHub during the
build (not from your working tree), then serving the static `www/` content with
Nginx.

### Prerequisites

- [Docker Engine](https://docs.docker.com/engine/install/) with the Compose plugin
  (`docker compose`), or Docker Desktop.

### Install and run

From the repo root:

```bash
cd production/docker
docker compose up --build -d
```

Open the app at [http://localhost:8083](http://localhost:8083) (host port is set in
`production/docker/docker-compose.yml`; change the left side of `ports` if 8083 is
already in use).

### Stop and remove

```bash
cd production/docker
docker compose down
```

### Build options

`REPO_URL` and `REPO_REF` in `docker-compose.yml` control which Git remote and branch
(or tag) are cloned. Edit those values and rebuild, for example:

```bash
docker compose build --no-cache
docker compose up -d
```

To build the image without Compose:

```bash
cd production/docker
docker build -t pos-cash .
```

Run it:

```bash
docker run --rm -p 8083:80 pos-cash
```
