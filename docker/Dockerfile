FROM node:10

# Create app directory
WORKDIR /usr/src/app

# strapi is a CLI; the above are customised extensions to the strapi CLI; namely, custom types
RUN npm install -g strapi

# A wildcard is used to ensure both package.json AND package-lock.json are copied
# where available (npm@5+)
#COPY package*.json ./

# Install this app from github project
RUN git clone https://github.com/wozitech/strapi.git /usr/src/app

# Work from the "clone" app directory
WORKDIR /usr/src/app/strapi

# Install the application dependencies
RUN npm install
# If you are building your code for production
# RUN npm ci --only=production

# now build the strapi admin UI
RUN npm run build

# strapi starts up on port 1337
EXPOSE 1337

# environment variables for database configuration
#  assumes the complementary mongo container is called "cms-db"
#  override DATABASE_HOST on the docker run with "-e" option
#  or provide a local "env_file" and use docker run with -e"
ENV DATABASE_HOST cms-db
ENV DATABASE_NAME cms
env DATABASE_PORT 27017
ENV DATABASE_SRV false
ENV DATABASE_SSL false
ENV DATABASE_USERNAME ''
ENV DATABASE_PASSWORD ''

# pick on the production DB configuration that uses ENV VAR overrides
ENV NODE_ENV production

# now start strapi
CMD ["npm", "run", "start"]
#CMD ["ping", "cms-db"]
