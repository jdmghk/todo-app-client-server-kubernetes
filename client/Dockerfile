FROM node:18-alpine as todo-app-build

WORKDIR /client

COPY package.json yarn.lock README.md ./

RUN yarn

COPY ./public ./public

COPY ./src ./src

# ✅ Fix for "error:0308010C:digital envelope routines::unsupported"
ENV NODE_OPTIONS=--openssl-legacy-provider
ENV REACT_APP_baseAPIURL=<backend-app-service-ip>:<port>

RUN yarn build

FROM nginx:latest

LABEL maintainer=Aamir-Pinger

COPY --from=todo-app-build /client/build/ /usr/share/nginx/html

EXPOSE 80
