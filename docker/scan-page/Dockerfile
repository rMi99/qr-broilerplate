FROM node:18

# WORKDIR /app

WORKDIR /var/www/html

COPY ./src/scan-page .

# COPY ./src/scan-page/package.json ./src/scan-page/package-lock.json ./
COPY ./src/scan-page/package.json .
COPY ./src/scan-page/package-lock.json .
RUN npm install

COPY ./src/scan-page/ .

EXPOSE 3000

CMD ["npm", "start"]
