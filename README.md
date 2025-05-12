# Dự án Cảm biến siêu âm (Ultrasonic Sensor)

## Tác giả
**Phạm Lê Ngọc Sơn**

## Mô tả dự án
Dự án này triển khai một hệ thống đo khoảng cách sử dụng cảm biến siêu âm HC-SR04 và vi điều khiển TM4C123GH6PM (ARM Cortex-M4F). Hệ thống có khả năng đo khoảng cách chính xác và hiển thị kết quả thông qua LED cảnh báo khi phát hiện vật cản ở khoảng cách gần (dưới 15cm).

## Cấu trúc dự án
- `main.c`: File mã nguồn chính chứa các hàm điều khiển cảm biến siêu âm và xử lý dữ liệu
- `RTE/`: Thư mục môi trường chạy (Run-Time Environment)
- `Objects/`: Thư mục chứa các file biên dịch
- `Listings/`: Thư mục chứa thông tin liệt kê
- `ultrasonic_sensor.uvprojx`: File cấu hình dự án cho Keil MDK
- `ultrasonic_sensor.uvoptx`: File cấu hình tùy chọn dự án
- `EventRecorderStub.scvd`: File cấu hình ghi lại sự kiện

## Nguyên lý hoạt động
1. **Nguyên lý cảm biến HC-SR04**:
   - Cảm biến gửi xung siêu âm (trigger) qua chân PA4
   - Cảm biến nhận tín hiệu phản hồi (echo) qua chân PB6
   - Khoảng cách được tính dựa trên thời gian từ lúc gửi đến lúc nhận tín hiệu

2. **Quy trình đo**:
   - Gửi xung kích hoạt 12μs qua chân trigger (PA4)
   - Đo thời gian từ cạnh lên đến cạnh xuống của tín hiệu echo
   - Tính toán khoảng cách dựa trên tốc độ âm thanh
   - Kích hoạt đèn LED (PF2) khi phát hiện vật ở khoảng cách < 15cm

## Cấu hình phần cứng
- **Vi điều khiển**: TM4C123GH6PM (ARM Cortex-M4F)
- **Tần số hoạt động**: 16MHz
- **Các chân kết nối**:
  - PA4: Chân TRIGGER của cảm biến
  - PB6: Chân ECHO của cảm biến
  - PF2: Đèn LED cảnh báo
- **Timer sử dụng**:
  - TIMER0: Đo thời gian giữa cạnh lên và cạnh xuống của tín hiệu echo
  - TIMER1: Tạo độ trễ microsecond

## Hướng dẫn sử dụng
1. **Cài đặt phần mềm**:
   - Keil MDK (phiên bản 5 trở lên)
   - Gói thư viện TM4C123 của ARM

2. **Kết nối phần cứng**:
   - Kết nối chân TRIGGER của HC-SR04 với PA4
   - Kết nối chân ECHO của HC-SR04 với PB6
   - Kết nối đèn LED với PF2 (qua điện trở 220Ω)
   - Cung cấp nguồn 5V cho cảm biến HC-SR04
   - Kết nối GND chung

3. **Biên dịch và nạp chương trình**:
   - Mở file dự án ultrasonic_sensor.uvprojx bằng Keil MDK
   - Biên dịch dự án (Build)
   - Kết nối board với máy tính qua cổng USB/JTAG
   - Nạp chương trình vào vi điều khiển (Flash)

4. **Kiểm tra hoạt động**:
   - Đặt vật cản trước cảm biến
   - Quan sát đèn LED sẽ sáng khi vật cản ở khoảng cách < 15cm
   - Đèn LED sẽ tắt khi vật cản ở khoảng cách ≥ 15cm

## Ứng dụng
- Hệ thống đỗ xe tự động
- Robot tránh vật cản
- Đo khoảng cách tự động
- Hệ thống cảnh báo vật cản