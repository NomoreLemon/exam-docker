FROM node:20 as builder

WORKDIR /app

COPY ["package.json", "pnpm-lock.yaml", "/app/"]

RUN npm install -g pnpm && pnpm install && pnpm install prisma

COPY . .

RUN pnpm prisma generate

RUN pnpm build

FROM node:20

COPY --from=builder /app/package*.json ./
COPY --from=builder /app/dist ./dist

ENTRYPOINT ["./client"]

WORKDIR /app

ENV NODE_ENV=production

ENTRYPOINT ["node", "dist/index.js"]
