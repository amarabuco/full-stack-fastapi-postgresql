# Stage 0, "build-stage", based on Node.js, to build and compile the frontend
# FROM tiangolo/node-frontend:10 as build-Stage
FROM node:16 as build-stage-1

WORKDIR /app

#COPY package*.json /app/

COPY ./ /app/

RUN npm install

ARG FRONTEND_ENV=production

ENV VUE_APP_ENV=${FRONTEND_ENV}

# Comment out the next line to disable tests
RUN npm run test:unit

RUN npm run build


# Stage 1, based on Nginx, to have only the compiled app, ready for production with Nginx
FROM nginx:1.15

# COPY --from=build-stage-1 /app/dist/ /usr/share/nginx/html

# COPY --from=build-stage-1 /nginx.conf /etc/nginx/conf.d/default.conf
# COPY ./nginx-backend-not-found.conf /etc/nginx/extra-conf.d/backend-not-found.conf

COPY --from=build-stage-1 /app/dist/ /usr/share/nginx/html
COPY ./nginx.conf /etc/nginx/conf.d/default.conf
COPY ./nginx-backend-not-found.conf /etc/nginx/extra-conf.d/backend-not-found.conf