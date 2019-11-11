# Strapi application

A quick description of your strapi application

# Build
```
npm install -g strapi
npm install
npm run build
```

# Dependencies
Requires a mongodb database; for dev assumed to be on localhost host (port 27001), no SSL, no srv, no authentication. This can of course be a container bound to host on port 27001.

## ENV VARS
Required for an Atlas DB:
```
DATABASE_HOST=<hostname>.mongodb.net
DATABASE_NAME=wozitech-cms
DATABASE_SRV=true
DATABASE_SSL=true
DATABASE_USERNAME=<wozitech-cms-username>
DATABASE_PASSWORD=<wozitech-cms-password>
```

Don't forgot to create the database username/password, having read/write permission to the given database.

# To run
Only staging/production are able to use ENV VARs for database details.

* For dev: `npm run develop`
* For staging: `NODE_ENV=staging npm run start`
* For production: `NODE_ENV=production npm run start`

# Docker
Build a local docker image; refer to `Dockerfile` in `docker` folder:
```
docker build -t wozitech/wozitech-cms .
```

To run CMS docker image requires a running monogdb (assumed to be cms-db - no port projection to host):
```
docker run -d --name cms-db mongo:latest
docker run -e "DATABASE_HOST=cms-db" -p 8080:1337 --link cms-db --name cms -d wozitech/wozitech-cms
```

Or to run the CMS only, against a remote database, namely MongoDB Atlas:
```
docker run --env-file=./env_file -p 8080:1337 --link cms-db --name cms -d wozitech/wozitech-cms
```

# Docker Compose
Can run the cms and complementary mongodb instance using docker-compose; refer `docker-compose.yaml` in `docker` folder:
```
docker-compose up -d
docker-compose down
```
