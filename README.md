# Restaurant

Dự án này là một ứng dụng web với:
- **Backend**: Laravel 11.44.7 (PHP 8.3.19)
- **Frontend**: Next.js 15.3.2
- **Database**: MySQL 8.0
- **Database Management**: phpMyAdmin

## Yêu cầu

Để chạy dự án, bạn cần cài đặt:
- **Git**: Để clone mã nguồn từ GitHub. Tải tại [git-scm.com](https://git-scm.com/).
- **Docker**: Để chạy các dịch vụ (Laravel, Next.js, MySQL, phpMyAdmin). Tải Docker Desktop (Windows/Mac) hoặc Docker cho Linux tại [docker.com](https://www.docker.com/get-started).
- **Docker Compose**: Thường đi kèm với Docker Desktop. Kiểm tra bằng lệnh `docker-compose --version`.
- Máy tính có ít nhất 4GB RAM và kết nối internet ổn định.

## Cài đặt và chạy dự án

### 1. Clone repository
Mở terminal (Command Prompt, PowerShell, hoặc Terminal trên Mac/Linux) và chạy:
```bash
git clone https://github.com/hOOANGhUUUY/restaurant.git
cd restaurant
```

### 2. Tạo tệp môi trường
- **Backend (Laravel)**:
  - Sao chép tệp `backend/.env.example` thành `backend/.env`:
    ```bash
    cp backend/.env.example backend/.env
    ```
  - Mở `backend/.env` và kiểm tra các cấu hình, đặc biệt là phần database:
    ```
    APP_NAME=Restaurant
    APP_ENV=local
    APP_KEY=
    APP_DEBUG=true
    APP_URL=http://localhost

    DB_CONNECTION=mysql
    DB_HOST=db
    DB_PORT=3306
    DB_DATABASE=restaurant
    DB_USERNAME=root
    DB_PASSWORD=root
    ```
  - Sau khi chạy Docker (bước 3), tạo khóa ứng dụng:
    ```bash
    docker exec -it laravel_backend php artisan key:generate
    ```

- **Frontend (Next.js)**:
  - Sao chép tệp `frontend/.env.local.example` thành `frontend/.env.local`:
    ```bash
    cp frontend/.env.local.example frontend/.env.local
    ```
  - Mở `frontend/.env.local` và kiểm tra:
    ```
    NEXT_PUBLIC_API_URL=http://backend:8000
    ```
  - Nếu cần thêm biến môi trường (như API keys), liên hệ trưởng nhóm để được hướng dẫn.

### 3. Chạy dự án với Docker
- Trong thư mục `restaurant/`, chạy:
  ```bash
  docker-compose up --build
  ```
- Chờ vài phút để Docker tải images, build container, và cài đặt phụ thuộc. Nếu lần đầu, quá trình có thể mất 5-10 phút.
- Truy cập các dịch vụ:
  - Backend: `http://localhost:8000`
  - Frontend: `http://localhost:3000`
  - phpMyAdmin: `http://localhost:8080` (đăng nhập: `root`/`root`)

### 4. Chạy migration (cho backend)
- Để tạo bảng database cho Laravel, chạy:
  ```bash
  docker exec -it laravel_backend bash
  php artisan migrate
  ```
- Nhấn Enter để thoát sau khi hoàn tất.

### 5. Dừng dự án
- Để dừng các container:
  ```bash
  docker-compose down
  ```

## Đóng góp mã

### 1. Tạo nhánh mới
- Tạo nhánh riêng để làm việc, ví dụ `feature/add-login`:
  ```bash
  git checkout -b feature/add-login
  ```
- Kiểm tra nhánh hiện tại:
  ```bash
  git branch
  ```
  (Nhánh của bạn sẽ có dấu `*`.)

### 2. Viết mã
- **Backend**: Chỉnh sửa mã trong `backend/` (ví dụ: thêm controller trong `backend/app/Http/Controllers/`).
- **Frontend**: Chỉnh sửa mã trong `frontend/` (ví dụ: thêm component trong `frontend/app/` hoặc `frontend/pages/`).
- Kiểm tra dự án sau khi sửa:
  ```bash
  docker-compose up --build
  ```

### 3. Commit và đẩy mã
- Thêm các tệp đã chỉnh sửa:
  ```bash
  git add .
  ```
- Commit với thông điệp rõ ràng:
  ```bash
  git commit -m "Thêm tính năng đăng nhập cho frontend và backend"
  ```
- Đẩy nhánh lên GitHub:
  ```bash
  git push origin feature/add-login
  ```

### 4. Tạo Pull Request
- Truy cập `https://github.com/hOOANGhUUUY/restaurant`.
- Vào tab **Pull Requests**, nhấn **New Pull Request**.
- Chọn nhánh `feature/add-login` để merge vào `main`.
- Viết mô tả (ví dụ: “Thêm trang đăng nhập và API đăng nhập”).
- Nhấn **Create Pull Request** và chờ trưởng nhóm review.

### 5. Cập nhật mã từ nhánh chính
- Để lấy mã mới từ `main`:
  ```bash
  git checkout main
  git pull origin main
  ```
- Nếu đang làm trên nhánh của bạn, merge `main` vào:
  ```bash
  git checkout feature/add-login
  git merge main
  ```
- Nếu có xung đột, mở tệp xung đột, sửa thủ công, sau đó:
  ```bash
  git add .
  git commit
  ```

## Xử lý lỗi phổ