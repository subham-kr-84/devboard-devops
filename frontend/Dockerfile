# Stage 1- Builder stage
FROM node:24-alpine AS builder

WORKDIR /app

COPY . .

RUN npm install --legacy-peer-deps && npm run build

# Stage 2- Runner stage
FROM node:24-alpine AS runner

WORKDIR /app

COPY package.json .
COPY vite.config.js .

# RUN npm install -g vite
# use project declared vite version

COPY --from=builder /app/dist ./dist
COPY --from=builder /app/node_modules ./node_modules

CMD ["npm", "run", "preview", "--", "--host", "0.0.0.0", "--port", "4173"]

