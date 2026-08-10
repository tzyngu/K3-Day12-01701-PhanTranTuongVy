# Thông Tin Deploy — Checkpoint 5

## Thông Tin Học Viên

| Mục | Nội dung |
| --- | --- |
| Họ và tên | Phan Tran Tuong Vy |
| Mã học viên | 01701 |
| Repo | https://github.com/tzyngu/K3-Day12-01701-PhanTranTuongVy |

## Service

| Mục | Nội dung |
| --- | --- |
| Public URL | Chưa có — đang dùng phương án local fallback |
| Platform | Railway/Render chưa được cấu hình tài khoản; kiểm chứng bằng Docker Compose local |
| Ngày deploy | 2026-08-10 |

## Biến Môi Trường Đã Set

| Biến | Nguồn giá trị |
| --- | --- |
| `PORT` | Dockerfile dùng mặc định 8000 khi chạy local |
| `AGENT_API_KEY` | File `.env`, không commit giá trị vào repo |
| `REDIS_URL` | Docker Compose: `redis://redis:6379/0` |
| `RATE_LIMIT_PER_MINUTE` | Mặc định ứng dụng: 10 |
| `MONTHLY_BUDGET_USD` | Mặc định ứng dụng: 10.0 |
| `LOG_LEVEL` | Mặc định ứng dụng: INFO |

## Kết Quả Chạy Local Fallback

Stack `agent` và `redis` được chạy bằng `docker compose up -d --build`.

- `GET http://localhost:8000/health` trả 200 với `{"status":"ok"}`.
- `GET http://localhost:8000/ready` trả 200 với `{"status":"ready","redis":true}`.
- `POST /ask` không có API key trả 401.

Ảnh kiểm chứng cần được chụp từ máy local sau khi chạy stack và lưu tại `screenshots/health.png`.

## Ghi Chú

Phương án fallback được sử dụng vì chưa có tài khoản Railway hoặc Render để tạo service HTTPS công khai. Khi có tài khoản, sẽ tạo Redis trên platform, set `AGENT_API_KEY` và `REDIS_URL` trong dashboard, sau đó thay phần Public URL bằng địa chỉ HTTPS thật.
