# 🤖 Animal Detector API (Backend)

Đây là server backend (FastAPI, Python) cho dự án nhận diện động vật.

Nó cungZ cấp một API endpoint (`/detect`) để nhận file ảnh, xử lý ảnh bằng mô hình YOLOv8 (ONNX), và trả về thông tin chi tiết về các động vật được phát hiện.

## Công nghệ sử dụng

* **Python 3.10+**
* **FastAPI:** Để xây dựng API.
* **ONNX Runtime:** Để chạy mô hình AI.
* **OpenCV (cv2):** Để tiền xử lý và hậu xử lý ảnh.
* **Uvicorn:** Để chạy server.

## Cài đặt & Chạy Local

1.  **Di chuyển vào thư mục:**
    ```bash
    cd backend
    ```

2.  **Tạo môi trường ảo (venv):**
    ```bash
    # Trên Windows
    py -m venv venv
    
    # Trên macOS/Linux
    python3 -m venv venv
    ```

3.  **Kích hoạt môi trường ảo:**
    ```bash
    # Trên Windows (PowerShell)
    .\venv\Scripts\activate
    
    # Trên macOS/Linux
    source venv/bin/activate
    ```

4.  **Cài đặt thư viện:**
    ```bash
    pip install -r requirements.txt
    ```

5.  **THÊM CÁC FILE QUAN TRỌNG:**
    Đây là bước quan trọng nhất. Bạn phải tự sao chép 3 file sau vào thư mục `backend` này:
    * `model.onnx` (File mô hình AI của bạn)
    * `labels.txt` (File nhãn)
    * `species.json` (File thông tin chi tiết các loài)

6.  **Chạy server:**
    ```bash
    uvicorn main:app --reload --host 0.0.0.0 --port 8000
    ```

Server của bạn bây giờ đang chạy tại `http://127.0.0.1:8000`.

## Triển khai (Deploy)

Project này được cấu hình để deploy lên **Render**:

* **Root Directory:** `backend`
* **Build Command:** `pip install -r requirements.txt`
* **Start Command:** `python main.py`

Project sẽ tự động đọc `PORT` từ biến môi trường của Render.

# 📸 Animal Detector (Frontend)

Đây là giao diện người dùng (Frontend) cho dự án nhận diện động vật, được xây dựng bằng **Next.js** và **TypeScript**.

Nó cho phép người dùng:
* Tải ảnh lên từ máy.
* Mở camera (trên điện thoại) để chụp ảnh mới.
* Gửi ảnh đến server backend AI để xử lý.
* Vẽ các hộp (bounding box) và hiển thị thông tin chi tiết về các đối tượng được nhận diện.

## Công nghệ sử dụng

* **Next.js 13+** (App Router)
* **React**
* **TypeScript**
* **CSS Modules**

## Cài đặt & Chạy Local

1.  **Di chuyển vào thư mục:**
    ```bash
    cd frontend
    ```

2.  **Cài đặt các gói (packages):**
    ```bash
    npm install
    ```

3.  **Chạy server (chế độ phát triển):**
    ```bash
    npm run dev
    ```

Trang web của bạn bây giờ đang chạy tại `http://localhost:3000`.

## Kết nối đến Backend

* **Khi chạy Local:** Code trong `page.tsx` được thiết lập để tự động tìm backend tại `http://127.0.0.1:8000`. Bạn *phải* chạy server `backend` trước khi chạy `frontend`.
* **Khi Deploy:** Project được cấu hình để đọc biến môi trường `NEXT_PUBLIC_API_URL` để tìm địa chỉ của backend (ví dụ: URL của Render).

## Triển khai (Deploy)

Project này được cấu hình để deploy lên **Vercel**:

* **Framework:** Next.js (tự động nhận diện)
* **Root Directory:** `frontend`
