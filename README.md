# YaTёrochka-psql
<p align="center">
  <img src="https://raw.githubusercontent.com/Kseen715/imgs/main/favicon.ico" />
</p>

## Description
This is PostgreSQL part of [YaTёrochka project](https://github.com/Kseen715/yaterochka). It's a web application written as a course work for the 3rd year of study at the university. 

The project is a web application for a fictional company that sells random goods. The application allows you to view the catalog of goods, view the history of orders, and also allows you to log in to your Admin account.

## Usage
Docker-compose:
```
version: '3'
services:
  yaterochka-psql:
    container_name: yaterochka-psql
    image: kseen/yaterochka-psql:latest
    command:
      - "sh"
      - "./run.sh"
    environment:
      POSTGRES_DB: <database>
      POSTGRES_USER: <username>
      POSTGRES_PASSWORD: <password>
      PGDATA: "/var/lib/postgresql/data/pgdata"
    volumes:
      - /mnt/d/ydb/yat-db-init:/docker-entrypoint-initdb.d    # PostgreSQL entrypoint path
      - /mnt/d/ydb/yat-db:/var/lib/postgresql/data            # PostgreSQL data path
    ports:
      - "5433:5432"
    healthcheck:
      test: [ "CMD-SHELL", "pg_isready -U postgres -d postgres" ]
      interval: 10s
      timeout: 5s
      retries: 5
      start_period: 10s
    restart: unless-stopped
    deploy:
      resources:
        limits:
          cpus: '1'
          memory: 4G
```
