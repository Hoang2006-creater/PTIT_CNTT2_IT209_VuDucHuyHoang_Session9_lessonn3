# Bài 3: Đóng gói trang Web HTML tĩnh với Dockerfile

## 1. Giới thiệu
Bài thực hành tạo một Docker image siêu nhẹ dựa trên base image `nginx:alpine` để phục vụ một trang web HTML tĩnh.

---

## 2. Cấu trúc thư mục
```text
.
├── Dockerfile
├── index.html
└── README.md
```

---

## 3. Nội dung các tệp

### `index.html`
```html
<h1>Hello Docker Session 09!</h1>
```

### `Dockerfile`
```dockerfile
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
```

- `FROM nginx:alpine`: Sử dụng base image Nginx chạy trên hệ điều hành Alpine Linux (kích thước siêu nhỏ, tối ưu hiệu năng).
- `COPY index.html /usr/share/nginx/html/index.html`: Sao chép file `index.html` từ máy host vào thư mục phục vụ web mặc định của Nginx.

---

## 4. Hướng dẫn chạy và kiểm tra

### Bước 1: Build Docker image
Chạy lệnh sau tại thư mục chứa `Dockerfile`:
```bash
docker build -t my-html-app:v1 .
```

### Bước 2: Khởi chạy container
Khởi chạy container chạy ngầm (detached) và ánh xạ cổng `8081` ở máy host vào cổng `80` trong container:
```bash
docker run -d -p 8081:80 --name html-app my-html-app:v1
```

### Bước 3: Kiểm tra kết quả
Dùng lệnh `curl` hoặc truy cập trình duyệt tại `http://localhost:8081`:
```bash
curl http://localhost:8081
```

**Kết quả mong đợi:**
```html
<h1>Hello Docker Session 09!</h1>
```

---

## 5. Dọn dẹp tài nguyên (tùy chọn)
Sau khi kiểm tra xong, có thể dừng và xóa container bằng lệnh:
```bash
docker rm -f html-app
```
