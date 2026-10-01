# Bài 4 — UFW và Cloud Firewall (tài liệu mô phỏng)

Nguyễn Đăng Dương — CNTT2 — IT209 — SS2.

Tài liệu trình bày bộ luật dự kiến chỉ mở SSH `22/tcp` và HTTP `80/tcp`, cùng file text minh họa kết quả `ufw status verbose`. Không có UFW hay DigitalOcean Cloud Firewall nào được cấu hình từ repo này; đầu ra trong `evidence/` là mẫu để đối chiếu.

Ảnh [ufw-setup-provided.png](screenshots/ufw-setup-provided.png) do người học cung cấp cho thấy các lệnh đặt chính sách UFW và thông báo firewall đã kích hoạt. Ảnh không hiển thị cấu hình Cloud Firewall trên DigitalOcean.

## Thiết kế hai lớp

1. **UFW trong Ubuntu:** mặc định deny incoming, allow outgoing; chỉ allow `22/tcp` và `80/tcp`.
2. **Cloud Firewall:** inbound chỉ cho TCP 22 và TCP 80; gắn firewall vào Droplet. Egress có thể để mặc định theo nhu cầu bài lab.

File [evidence/ufw-status-example.txt](evidence/ufw-status-example.txt) là output mô phỏng phù hợp với các rule nêu trên. Nội dung hướng dẫn thực hành và giới hạn minh chứng nằm trong [FIREWALL-REPORT.md](FIREWALL-REPORT.md).
