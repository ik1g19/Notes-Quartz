Typical Spring project structure:
- **Controller**: receives HTTP requests, returns responses
- **Service**: business logic
- **Repository**: DB access
- **Entity**: persistence model
- **DTO**: API request/response models
- **Exception handling**: centralised errors with `@ControllerAdvice`

Spring modules used:
- Spring Web
- Spring Data JPA
- PostgreSQL driver
- Bean Validation
- Lombok optionally
- Spring Security later if adding auth

`pom.xml` holds the Spring dependencies, Spring initializr configures this for you

# Postgres Setup

The backend needs a db to run, I installed the official postgres container using

```bash
docker pull postgres
```

Started a container using

```bash
docker run -itd -e POSTGRES_USER=myuser -e POSTGRES_PASSWORD=mypassword -p 5432:5432 --name mypostgres postgres
```

Then connected using the psql terminal using

```bash
PGPASSWORD=mypassword psql -h localhost -p 5432 -U myuser
```

Then use `\l` to list the databases

To connect using the `psql` client I used

```bash
docker exec -it mypostgres psql -U myuser 
```

In psql I made a database with

```sql
CREATE DATABASE url_shortener;
```

## Spring Postgres Setup

