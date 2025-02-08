---
title: Basic Docker File
---

```dockerfile
FROM node:23-alpine

# addgroup mygroup && adduser -S -G mygroup myuser
RUN addgroup app && adduser -S -G app app

USER app

WORKDIR /app

COPY package*.json ./

USER root

# chown -R <user>:<group> <directory>
RUN chown -R app:app .

USER app

RUN npm install

COPY . .

EXPOSE 5173

CMD npm run dev
```
