FROM node:26-alpine

WORKDIR /usr/src/inventory-service/

COPY package*.json .
RUN npm ci --omit=dev && npm cache clean --force

COPY --chown=node:node src/ .
USER node

EXPOSE 8083
CMD ["node", "index.js"]
