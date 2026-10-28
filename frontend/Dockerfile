FROM node:26-alpine AS builder

WORKDIR /frontend

COPY package.json package-lock.json ./
RUN npm ci 

COPY . .
RUN npm run build

FROM nginx:1.31.8-alpine

COPY --from=builder /frontend/nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /frontend/dist /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]