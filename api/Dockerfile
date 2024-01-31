# Specify Node Version and Image
# Name Image development (can be anything)
FROM node:18.16.0  AS development

# Specify Working directory inside container
WORKDIR /tsepo/src/app

# Copy package-lock.json & package.json from host to inside container working directory
COPY package*.json ./

# Install deps inside container
RUN npm install
RUN npm install -g @angular/cli@12.0.0

# Bundle App Source
COPY .  .

RUN npm run build

EXPOSE 3000

################
## PRODUCTION ##
################
# Build another image named production
FROM node:18 AS production

ARG NODE_ENV=production
ENV NODE_ENV=${NODE_ENV}

# Set work dir
WORKDIR /tsepo/src/app

COPY --from=development /tsepo/src/app/ .

EXPOSE 8080

# run app
CMD [ "node", "dist/main"]