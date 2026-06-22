# Screenshots

## Nội dung thư mục này

Bao gồm các ảnh chụp màn hình chứng minh pipeline Delta Lake hoạt động đúng.

## Checklist theo rubric.md

| # | Ảnh | Nội dung |
|---|---|---|
| 1 | `tree_lakehouse_1.png` | Cấu trúc thư mục `_lakehouse/` — Bronze, Gold đang hiển thị |
| 2 | `tree_lakehouse_2.png` | Cấu trúc thư mục `_lakehouse/` — Silver, scratch đang hiển thị |
| 3 | `tree_lakehouse_3.png` | `_delta_log/` của `events_smallfiles` — thấy rõ hàng trăm JSON version |
| 4 | `tree_lakehouse_4.png` | `events_smallfiles` parquet files sau Z-ORDER |
| 5 | `tree_lakehouse_5.png` | Toàn bộ cây thư mục — 35 directories, 640 files |

## Xác nhận deliverables

- ✅ Bronze: `_lakehouse/bronze/llm_calls_raw/` tồn tại
- ✅ Silver: `_lakehouse/silver/llm_calls/` tồn tại, phân vùng theo ngày
- ✅ Gold: `_lakehouse/gold/llm_daily_metrics/` tồn tại — **8 ngày** (2026-04-01 → 2026-04-08) ≥ 7 ngày yêu cầu
- ✅ `_delta_log/` JSON files hiển thị rõ ràng trong từng table
- ✅ `events_smallfiles` có nhiều file nhỏ trước OPTIMIZE (thấy trong log)
- ✅ Tổng cộng 35 directories, 640 files
