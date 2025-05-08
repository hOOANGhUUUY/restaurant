FROM node:20-alpine

# Thiết lập thư mục làm việc
WORKDIR /app

# Sao chép package.json và package-lock.json
COPY package*.json ./

# Cài đặt phụ thuộc
RUN npm install

# Sao chép toàn bộ mã nguồn
COPY . .

# Build ứng dụng Next.js và kiểm tra lỗi
RUN npm run build || { echo "Next.js build failed"; exit 1; }

# Mở cổng
EXPOSE 3000

# Khởi động ứng dụng Next.js
CMD ["npm", "start"]