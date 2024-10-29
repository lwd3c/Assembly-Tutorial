### 1. Khởi tạo kho lưu trữ
    > git init

### 2. Kết nối với kho lưu trữ từ xa trên GitHub
    > git remote add origin <URL-kho-luu-tru-GitHub>

### 3. Thêm file vào vùng chờ
    > git add .

**Nếu chưa có branch `main`:** `git checkout -b main`
    
### 4. Commit thay đổi
    > git commit -m "Thông điệp commit"

### 5. Push code lên GitHub
Lần đầu tiên:

    git push -u origin main
Từ sau trở đi chỉ cần:

    git push
    
### 6. Pull về local
    > git pull origin main
