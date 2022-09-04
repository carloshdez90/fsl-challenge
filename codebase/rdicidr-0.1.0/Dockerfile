### STAGE 1: BUILD ###
FROM node:14 AS builder

WORKDIR /app

COPY . /app/

RUN       npm install && \
          npm run lint && \
          npm install prettier && \
          npm run prettier && \
          CI=true npm run test && \
          npm run build

### STAGE 2: RUN APP ###
FROM nginx:1.23.1
COPY --from=builder /app/build/ /usr/share/nginx/html/
COPY default.conf /etc/nginx/conf.d 
EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]