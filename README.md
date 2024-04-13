# Node.js API with PostgreSQL and TypeScript DEMO

## Starting project

### Install project dependencies

```bash
yarn install
```

### Create `.env` file

Rename the file `.env.example` to `.env`
This step is important to run before running the `prestart` command

### Run project prestart

```bash
yarn prestart
```

This will check for the `.env` file located at the project root level and load below environment variables

```ts
POSTGRES_DB: undefined;
POSTGRES_HOST: undefined;
POSTGRES_PASSWORD: undefined;
POSTGRES_USER: undefined;
```

## Database Setup

### Create Postgresql database with Docker command

```bash
docker run -d \
--name node-postgres-demo \
-e POSTGRES_PASSWORD=postgres \
-e POSTGRES_USER=postgres \
-e POSTGRES_DB=node-postgres-demo \
-p 5432:5432 \
postgres
```

### Create `Users Table` from terminal

#### Get in docker container terminal

```bash
docker exec -it {container_identifier} bash
```

The {container_identifier} for Docker is the Container ID for the Docker instance
You can get it using the below command

```bash
docker ps
```

#### Login to Postgres

```bash
psql -h localhost -p 5432 -U postgres
```

#### Go to `node-postgres-demo`

```bash
\c node-postgres-demo
```

#### Create users table

```bash
CREATE TABLE users (
 id SERIAL PRIMARY KEY,
 username VARCHAR(80),
 email VARCHAR(255),
 created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
 );
```

#### Create entry in `Users table`

```bash
curl -H 'Content-Type: application/json'
-d '{"username": "mateo", "email": "mateo@gmail.com"}'
-X POST
http://localhost:5000/api/v1/users
```

#### Get all users

```bash
curl -H 'Content-Type: application/json'
http://localhost:5000/api/v1/users
```
