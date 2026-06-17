# ============================================
# Stage 1: Build
# ============================================
FROM node:20-alpine AS builder

WORKDIR /app

# Копируем package.json и package-lock.json (если есть)
COPY package*.json ./

# Устанавливаем все зависимости
RUN npm install

# Копируем исходный код
COPY . .

# Генерируем Prisma Client
RUN npx prisma generate

# Компилируем TypeScript
RUN npm run build

# ============================================
# Stage 2: Production
# ============================================
FROM node:20-alpine AS production

WORKDIR /app

# Устанавливаем переменные окружения для продакшена
ENV NODE_ENV=production

# Копируем package.json для установки production зависимостей
COPY package*.json ./

# Устанавливаем только production зависимости
RUN npm install --omit=dev

# Копируем Prisma схему и генерируем клиент
COPY prisma ./prisma/
RUN npx prisma generate

# Копируем скомпилированный код из builder stage
COPY --from=builder /app/dist ./dist

# Открываем порт
EXPOSE 3000

# Health check
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
  CMD nc -z localhost 3000 || exit 1

# Запускаем приложение
CMD ["node", "dist/src/main.js"]
