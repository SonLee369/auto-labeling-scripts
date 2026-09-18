# 🤖 Bộ công cụ Auto-Labeling 

Bộ script này được thiết kế nhằm mục đích tự động hóa quá trình chú thích (annotation) cho dữ liệu hình ảnh, giúp tiết kiệm hàng trăm giờ làm việc thủ công và đẩy nhanh quá trình chuẩn bị dữ liệu cho việc huấn luyện mô hình học sâu (Deep Learning).

Repository này bao gồm 2 file notebook chính:

1. `Bbox-Polygon-Auto-Labeling-Script`
2. `Segment-Auto-Labeling-Script`

---

## 📖 Giới thiệu chi tiết

### 1. Bbox-Polygon-Auto-Labeling-Script

Notebook này được xây dựng để tự động nhận diện và tạo ra các **Bounding Box** (hộp giới hạn) và **Polygon** (đa giác) bao quanh các đối tượng mục tiêu trong tập dữ liệu hình ảnh.

* **Mục đích:** Hỗ trợ chuẩn bị dữ liệu nhanh chóng cho các bài toán Object Detection (như YOLO, Faster R-CNN, SSD) và các bài toán Instance Segmentation cơ bản.
* **Đầu ra (Output):** Xuất trực tiếp ra các định dạng chuẩn phổ biến cho Computer Vision như YOLO format (.txt) hoặc COCO format (.json).
* **Điểm nổi bật:** Có thể được tích hợp với các mô hình Zero-shot Object Detection để gán nhãn dựa trên văn bản (text-prompt) mà không cần huấn luyện lại từ đầu.

### 2. Segment-Auto-Labeling-Script

Notebook này tập trung vào bài toán chi tiết hơn là **Image Segmentation** (Phân vùng hình ảnh).

* **Mục đích:** Tự động tạo các lớp mặt nạ (masks) với độ chính xác đến từng pixel (pixel-perfect). Rất phù hợp cho các bài toán Semantic Segmentation, Instance Segmentation, hoặc Medical Image Analysis.
* **Đầu ra (Output):** Các ảnh mask nhị phân (Binary Masks) hoặc đa lớp (Multi-class masks) kết hợp cùng file cấu hình phân lớp.
* **Điểm nổi bật:** Ứng dụng sức mạnh của các mô hình nền tảng như SAM (Segment Anything Model) để trích xuất vật thể tự động thông qua thao tác quét toàn bộ ảnh hoặc qua tọa độ mồi (prompt points).

---

## 🚀 Hướng dẫn sử dụng 

Cả hai script đều được định dạng dưới dạng Jupyter Notebook và có thể chạy mượt mà trên **Google Colab** (Khuyến nghị sử dụng GPU).

### Bước 1: Chuẩn bị môi trường

1. Tải lên 2 file `Bbox-Polygon-Auto-Labeling-Script` và `Segment-Auto-Labeling-Script` lên Google Drive của bạn.
2. Mở file bằng **Google Colaboratory**.
3. Bật Runtime GPU: Chọn `Runtime` > `Change runtime type` > `Hardware accelerator` > Chọn `T4 GPU` hoặc các GPU cao hơn.

### Bước 2: Tải dữ liệu vào Workspace

* Chạy ô (cell) đầu tiên trong notebook để cấp quyền truy cập (Mount) vào Google Drive của bạn.
* Chỉnh sửa đường dẫn `dataset_path` trỏ đến thư mục chứa ảnh gốc (raw images) mà bạn muốn gán nhãn.

### Bước 3: Cấu hình siêu tham số (Hyperparameters)

Tùy thuộc vào script bạn đang chạy:

* **Đối với Bbox/Polygon:** Xác định `classes` (danh sách tên các vật thể cần nhận diện) và ngưỡng tin cậy `confidence_threshold`.
* **Đối với Segment:** Cấu hình đường dẫn lưu masks và các tham số nội suy mặt nạ để đảm bảo viền ảnh chính xác.

### Bước 4: Chạy Auto-Labeling

* Nhấn `Run All` hoặc chạy lần lượt các cells từ trên xuống dưới.
* Hệ thống sẽ chạy suy luận (inference) trên toàn bộ ảnh và lưu kết quả annotations/masks vào thư mục đầu ra `output_dir` mà bạn đã chỉ định.

### Bước 5: Hậu kiểm (Post-Processing)

* **Lưu ý quan trọng từ Chuyên gia:** Auto-labeling không bao giờ chính xác 100%. Bạn nên import các file gán nhãn tự động này vào các phần mềm quản lý như **CVAT**, **Roboflow**, hoặc **LabelImg/LabelMe** để con người review và chỉnh sửa lại các điểm lỗi trước khi đưa vào huấn luyện mô hình thực tế.

---

## 🛠 Yêu cầu hệ thống (Dependencies)

* Python 3.8+
* PyTorch & Torchvision
* OpenCV (cv2)
* Numpy, Matplotlib
* (Các thư viện model-specific khác sẽ được tải tự động qua lệnh `!pip install` trong notebook).

## 🤝 Đóng góp

Nếu bạn gặp vấn đề, bug, hoặc muốn mở rộng thêm tính năng, hãy thoải mái mở Issue hoặc tạo Pull Request. Chúng tôi luôn hoan nghênh những đóng góp từ cộng đồng Computer Vision!
