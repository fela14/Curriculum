FROM node:lts-alpine
WORKDIR /usr/src/app
COPY curriculum-front/package*.json ./
RUN npm install
COPY curriculum-front ./
RUN npm run build
WORKDIR /usr/src/app/dist
EXPOSE 8080
CMD ["npx", "serve", "-s", "."]
