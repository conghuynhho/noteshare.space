FROM node:16-alpine AS BUILD_IMAGE
# FROM --platform=linux/amd64 node:16-alpine AS BUILD_IMAGE

RUN apk update \
  && apk add openssl1.1-compat
#https://github.com/prisma/prisma/issues/16553

# install dependencies
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm ci

# Copy all local files into the image.
COPY . .

RUN npx prisma generate

RUN npm run build

# remove development dependencies
RUN npm prune --production

FROM node:16-alpine

WORKDIR /app
COPY --from=0 /app .

ENV PORT 8080
EXPOSE 8080

CMD ["node", "./build/src/server.js"]