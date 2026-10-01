# Báo cáo bài 4 — Tường lửa hai lớp

## Chính sách truy cập

Mục tiêu là chỉ để SSH và HTTP truy cập được từ ngoài. Ở lớp máy chủ, UFW dùng chính sách mặc định `deny incoming` và `allow outgoing`, sau đó cho phép `22/tcp` để quản trị SSH và `80/tcp` để phục vụ website. Ở lớp biên, DigitalOcean Cloud Firewall cho phép inbound TCP 22 và TCP 80 từ `0.0.0.0/0` và `::/0` (hoặc giới hạn SSH theo IP quản trị), rồi gắn vào Droplet. Các cổng không có rule allow sẽ bị chặn.

## Kết quả mẫu UFW

File `evidence/ufw-status-example.txt` thể hiện dạng kết quả dự kiến của `sudo ufw status verbose`, dựa theo yêu cầu bài. Đây là output minh họa tạo cho bài nộp, không phải output đo từ máy Ubuntu. Ảnh do người học cung cấp trong `screenshots/` cho thấy lệnh đặt policy và thông báo UFW đã active; ảnh không phải ảnh cấu hình Cloud Firewall.

## Vì sao dùng hai lớp

Cloud Firewall lọc lưu lượng trước khi đến máy chủ, còn UFW cung cấp lớp kiểm soát tại hệ điều hành. Nếu một lớp bị cấu hình nhầm, lớp còn lại vẫn giới hạn bề mặt cổng mạng. Kiểm tra thiết kế bằng cách đối chiếu rule inbound của Cloud Firewall với `ufw status verbose`; SSH cần được cho phép trước khi bật UFW trên máy thật để tránh tự khóa phiên quản trị.

## Bộ luật minh họa

```text
Default incoming: deny
Default outgoing: allow
Allow: 22/tcp (SSH)
Allow: 80/tcp (HTTP)
All other inbound ports: denied
```

Không có kết nối hoặc thay đổi nào được thực hiện trên DigitalOcean trong quá trình chuẩn bị các tệp này. Muốn chứng minh cấu hình Cloud Firewall đã áp dụng thật, cần ảnh chụp Console sau khi tạo firewall và gán Droplet; ảnh hiện có chỉ minh chứng bước UFW.
