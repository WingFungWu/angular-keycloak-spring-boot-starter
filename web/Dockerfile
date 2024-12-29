FROM node:20-alpine3.20 AS builder

WORKDIR /app

COPY ./package.json .
COPY ./package-lock.json .
RUN npm ci

COPY ./angular.json .
COPY ./tsconfig.json .
COPY ./tsconfig.app.json .
COPY ./src ./src
RUN npm run build

# runtime
FROM node:20-alpine3.20

WORKDIR /app

RUN npm i -g http-server

COPY --from=builder /app/dist ./dist

ENTRYPOINT [ "http-server" ]
CMD [ "/app/dist", "-p", "4200", "-d", "false" ]
