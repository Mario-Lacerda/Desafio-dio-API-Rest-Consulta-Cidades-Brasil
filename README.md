# Desafio Dio API Rest Java Cidades Brasil 

Construindo uma API Rest de consulta de cidades do Brasil do zero até a produção

### Descrição
Desenvolver uma API Rest de consulta de cidades do Brasil com dados comparativos. Nessa sessão você irá desenvolver uma API rest de consulta. A ideia é navegar pelas boas práticas de Java e do Spring, popular o bando de dados Postgres, criar serviço para cálculo de distância entre cidades.

### Endpoints
- GET /api/v1/states

- GET /api/v1/states/{id}

- GET /api/v1/cities

- GET /api/v1/cities/{id}

- GET /api/v1/countries

- GET /api/v1/countries/{id}

- GET /api/v1/distances/by-points?from={id}&to={id}

- GET /api/v1/distances/per-cube?from={id}&to={id}

  

#### Detalhes obtidos no README original do projeto DataBase
### Postgres
* [Postgres Docker Hub](https://hub.docker.com/_/postgres)

```shell script
docker run --name cities-db -d -p 5432:5432 -e POSTGRES_USER=postgres_user_city -e POSTGRES_PASSWORD=super_password -e POSTGRES_DB=cities postgres
```

### Populate
* [data](https://github.com/chinnonsantos/sql-paises-estados-cidades/tree/master/PostgreSQL)

  cd ~/workspace/sql-paises-estados-cidades/PostgreSQL

  docker run -it --rm --net=host -v $PWD:/tmp postgres /bin/bash

  psql -h localhost -U postgres_user_city cities -f /tmp/pais.sql
  psql -h localhost -U postgres_user_city cities -f /tmp/estado.sql
  psql -h localhost -U postgres_user_city cities -f /tmp/cidade.sql

  psql -h localhost -U postgres_user_city cities

  CREATE EXTENSION cube; 
  CREATE EXTENSION earthdistance;



### Foi utilizado neste projeto:

- Java 11
- IntelliJ 
- Grandle
- Spring Data JPA
- Spring Web
- Spring Boot 
- Postgres SQL Driver
- [cidade.sql](https://github.com/chinnonsantos/sql-paises-estados-cidades/tree/master/PostgreSQL)

&nbsp;

Retornando todas as Cidades:
- localhost:8080/cidades

![All](https://github.com/gusBernardi/DIO_API_Rest_Cidades_Java/blob/main/images/getAll.png)

Retornando apenas uma cidade por Id:
- localhost:8080/cidades/1

![Id](https://github.com/gusBernardi/DIO_API_Rest_Cidades_Java/blob/main/images/getById.png)

Calculando a distância em metros usando a extensão "earthdistance" e "cube" do PostgreSQL:
- localhost:8080/distancia/metros?origem=1&destino=2

![Dist](https://github.com/gusBernardi/DIO_API_Rest_Cidades_Java/blob/main/images/Distancia.png)

* [Postgres Earth distance](https://www.postgresql.org/docs/current/earthdistance.html)
* [earthdistance--1.0--1.1.sql](https://github.com/postgres/postgres/blob/master/contrib/earthdistance/earthdistance--1.0--1.1.sql)
* [OPERATOR <@>](https://github.com/postgres/postgres/blob/master/contrib/earthdistance/earthdistance--1.1.sql)
* [postgrescheatsheet](https://postgrescheatsheet.com/#/tables)
* [datatype-geometric](https://www.postgresql.org/docs/current/datatype-geometric.html)

### Access
```shell script
docker exec -it cities-db /bin/bash

psql -U postgres_user_city cities
```

### Query Earth Distance
Point
```roomsql
select ((select lat_lon from cidade where id = 4929) <@> (select lat_lon from cidade where id=5254)) as distance;
```

Cube
```roomsql
select earth_distance(
    ll_to_earth(-21.95840072631836,-47.98820114135742), 
    ll_to_earth(-22.01740074157715,-47.88600158691406)
) as distance;
```

## Spring Boot
* [https://start.spring.io/](https://start.spring.io/)

