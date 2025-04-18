# Local Docker environment: LEMP + MongoDB + Elasticsearch + Redis

A local dockerized environment running:

-   NGNIX ~ PHP 8.3
-   MySQL 8.0
-   MongoDB 8.0
-   Redis 7.0
-   Elasticsearch 8.16 (with Kibana)

(Setup instructions for Mac users)

## Require

Install [Docker](https://www.docker.com/products/docker-desktop)

## Setup

### Step 1 - clone environment

Clone the environment into a folder of your choice {MY_ENV}:

```bash
git clone https://github.com/pdphilip/docker-LEMP-REM.git MY_ENV
```

### Step 2 - set up hosts

For example:

-   laravel.loc
-   api.domain.loc

### Step 2.1 - edit sites-enabled `in env/php/sites-enabled/   `

-   laravel.loc.conf
-   api.domain.loc.conf

Edit domain_name variable on first line:

```bash
Define domain_name laravel.loc
```

```bash
Define domain_name api.domain.loc
```

### Step 2.2 - edit Mac host file

Via Terminal:

```bash
sudo nano /etc/hosts
```

Then add in:

```bash
0.0.0.0 localhost
0.0.0.0 laravel.loc
0.0.0.0 api.domain.loc
```

### Step 3 - docker-compose build

In environment root, run:

```bash
docker-compose build
```

## Running:

In repo root, run:

```bash
docker-compose up
```

Your local environment should be up and running on:

-   [http://localhost/](http://localhost/)
-   [http://laravel.loc/](http://laravel.loc/)
-   [http://api.domain.loc/](http://api.domain.loc/)

## Accessing from **outside** containers:

-   Mysql:
    -   host: **localhost**
    -   port: **3306**
    -   user: **root**
    -   pwd: **pass**
-   MongoDB:
    -   host: **localhost**
    -   port: **27017**
-   Elasticsearch:
    -   host: **localhost**
    -   port: **9200**
    -   url: **`http://localhost:9200`**
-   Kibana:
    -   url: **`http://localhost:5601`**
-   Redis:
    -   host: **127.0.0.1**
    -   port: **6380**

## Accessing from **inside** containers:

-   Mysql:
    -   host: **mysql**
    -   port: **3306**
    -   user: **root**
    -   pwd: **pass**
-   MongoDB:
    -   host: **mongo**
    -   port: **27017**
-   Elasticsearch:
    -   host: **elasticsearch**
    -   port: **9200**
    -   url: **`http://elasticsearch:9200`**
-   Redis:
    -   host: **redis**
    -   port: **6379**

If you would like to simulate 3 Elasticsearch nodes, then use `docker-compose-es3.yml`

## Notes:

-   Local site files root in ./sites/{domain}/html
-   Add ENV vars under the PHP container in docker-compose.yml
-   Data is persisted locally in: ./data/{engine}/

Simples

Local only please, nothing is secure
