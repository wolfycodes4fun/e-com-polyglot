FROM node:26-alpine AS builder

WORKDIR /dev/src/

COPY package*.json .
RUN npm ci 

COPY . .
RUN npm run build