# Stage 1: Build Quasar SPA
FROM node:20-alpine AS builder

WORKDIR /app

# เอา source code ทั้งโปรเจกต์เข้าไปก่อน
COPY . .

# ติดตั้ง dependencies (จะรัน quasar prepare ได้เพราะมีไฟล์ครบแล้ว)
RUN npm ci --legacy-peer-deps

# Build Quasar (สร้าง dist/spa)
RUN npm run build

# Stage 2: Production - serve ด้วย Nginx
FROM nginx:1.27-alpine

# คัดลอกไฟล์ static ที่ build แล้วไปไว้ในโฟลเดอร์ของ nginx
COPY --from=builder /app/dist/spa /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
