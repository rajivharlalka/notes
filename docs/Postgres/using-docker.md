## Setup postgres locally using docker

```shell
docker run --name postgresql-container -p 5432:5432 -e POSTGRES_PASSWORD=test-db -d postgres
```

## Docker-compose

```shell
version: '3'

services:
  postgres:
    container_name: postgres
    image: postgres:latest
    volumes:
      - dbdata:/var/lib/postgresql/data
    ports:
      - 5432:5432
    environment:
      POSTGRES_USER: "root"
      POSTGRES_PASSWORD: "password"
    restart: always

volumes:
  dbdata:
```

