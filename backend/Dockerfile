# Backend Dockerfile - multi-stage
# Build stage
FROM node:20-alpine AS builder
WORKDIR /app

# install dependencies (including devDeps for build step)
COPY package.json package-lock.json* ./
# Install all dependencies so tsc and @types packages are available to build
RUN npm ci || npm install

# copy source
COPY tsconfig.json ./
COPY src ./src

# build TypeScript using local project tsc
RUN npm run build

# Production stage
FROM node:20-alpine AS runner
WORKDIR /app
ENV NODE_ENV=production

# copy production deps
COPY --from=builder /app/package.json ./
COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/dist ./dist

EXPOSE 3001
CMD ["node", "dist/server.js"]
