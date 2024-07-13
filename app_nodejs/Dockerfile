FROM node:22-alpine

WORKDIR /app

COPY package*.json .

RUN npm i

COPY . .

EXPOSE 3000

RUN addgroup -S app && adduser -S app -G app && chown -R app:app . 

USER app

CMD [ "npm", "run", "start" ]
