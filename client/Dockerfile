FROM node:22.13.0-alpine3.21 AS builder
RUN mkdir -p /app
WORKDIR /app
COPY ./package*.json .
ENV http_proxy=http://proxy.esl.cisco.com:80/
ENV https_proxy=http://proxy.esl.cisco.com:80/
RUN npm i
COPY . .
RUN npm run build

################################
#### PRODUCTION ENVIRONMENT ####
################################


FROM nginx:alpine
WORKDIR /usr/share/nginx/html
COPY --from=builder /app/dist .
COPY ./nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 8088
CMD ["nginx", "-g", "daemon off;"]
