# Bài 2: Đóng gói Backend bằng Single-stage Dockerfile

## 1. Mục tiêu
Đóng gói ứng dụng Web Backend Node.js bằng Docker sử dụng Single-stage Dockerfile.

## 2. Công nghệ sử dụng
- Node.js 18 Alpine
- Express.js
- Docker

## 3. Cấu trúc project

```text
ex2/
├── Dockerfile
├── package.json
├── server.js
└── README.md
```

## 4. Nội dung Dockerfile
- `FROM node:18-alpine`: sử dụng image nền Node.js 18 Alpine.
- `WORKDIR /app`: thiết lập thư mục làm việc.
- `COPY package*.json ./`: sao chép file khai báo thư viện.
- `RUN npm install`: cài đặt thư viện cần thiết.
- `COPY . .`: sao chép mã nguồn vào image.
- `ENV PORT=3000`: thiết lập cổng ứng dụng.
- `EXPOSE 3000`: khai báo cổng ứng dụng trong container.
- `CMD ["node", "server.js"]`: khởi chạy backend.

## 5. Build Docker image

```bash
docker build -t hw-backend:v1 .
```

## 6. Chạy container

```bash
docker run -d --name app-single-stage -p 8080:3000 hw-backend:v1
```

## 7. Kiểm tra container và log

```bash
docker ps
docker logs app-single-stage
```

## 8. Kiểm tra API

```bash
curl -i http://localhost:8080/
```

Kết quả mong đợi: HTTP 200 OK và dữ liệu JSON:

```json
{
  "status": "success",
  "message": "Hello from Docker Single-stage!"
}
```