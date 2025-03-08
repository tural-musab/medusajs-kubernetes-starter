FROM node:22-slim

RUN corepack enable yarn

WORKDIR /app

COPY .medusa/server ./
COPY .yarnrc.yml ./

RUN yarn install --immutable

EXPOSE 9000

CMD ["yarn", "start"]
