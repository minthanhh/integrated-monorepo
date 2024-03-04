FROM docker.io/node:lts-alpine as development
ENV NODE_ENV development
ENV PORT 3000
WORKDIR /usr/src/app
COPY package.json pnpm-lock.yaml ./
RUN npm install -g pnpm@latest
RUN pnpm install
COPY apps/auth-service ./apps/auth-service
COPY nx.json tsconfig.base.json pnpm-workspace.yaml jest.config.ts jest.preset.js ./
COPY .nx ./.nx
EXPOSE 3000
CMD [ "npx", "nx", "serve", "auth-service" ]

# Production image, copy all the files and run nest
FROM docker.io/node:lts-alpine as runner
RUN apk add --no-cache dumb-init
ENV NODE_ENV production
ENV PORT 3000
WORKDIR /usr/src/app
COPY --from=development /usr/src/app/package.json ./package.json
COPY --from=development /usr/src/app/pnpm-lock.yaml ./pnpm-lock.yaml
COPY dist/apps/auth-service .

RUN npm install -g pnpm@latest
RUN pnpm install --frozen-lockfile --prod

RUN chown -R node:node .
USER node
EXPOSE 3000
CMD ["dumb-init", "node", "main.js"]
