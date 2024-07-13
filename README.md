# demo

## Init

```bash
npm init -y
npm i express
npm i -D nodemon supertest jest
```

## Dev

```bash
npm i
npm start
```

## Docker

```bash
docker build -t sh3b0/demo .
echo $PASSWORD | docker login -u sh3b0 --password-stdin
docker push sh3b0/demo --all-tags
```

## Run with MongoDB

```bash
docker compose build --no-cache && docker compose up -d
```

## Autotests

NodeJS tests run automatically (GitHub Action) on each push to the main branch that modifies files in the `app_nodejs` directory.
