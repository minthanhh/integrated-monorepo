FROM docker.io/node:lts-alpine as development

RUN apk add --no-cache libc6-compat

ENV NODE_ENV development
ENV PORT 4000
WORKDIR /usr/src/app

COPY package.json pnpm-lock.yaml tsconfig.base.json jest.preset.js nx.json ./
COPY .nx ./.nx
COPY node_modules ./node_modules

COPY apps/web-main apps/web-main

EXPOSE $PORT

CMD ["npx", "nx", "serve", "web-main"]
