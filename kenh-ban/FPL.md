# KÊNH FPL — FPT Play (SaleChannelID 10)

> Tách từ `RULE-CHINH-SACH-KENH-BAN.md` (nguồn: user cung cấp 03/11/2026). Rule chung: [00-CHUNG.md](00-CHUNG.md) · Rule XHD: [`../RULE-XHD.md`](../RULE-XHD.md).

## Thông tin chung

| Mục | Nội dung |
|---|---|
| Owner | Chưa có thông tin |
| Nơi tạo đơn | Web FPL: **dev.fptplay.vn** |
| Host | Không cần host |

## Rule xuất hóa đơn riêng (theo `RULE-XHD.md`)
- **Thông tin khách (BR-DB-03):** khách chọn có lấy hóa đơn không; nếu có thì tự nhập 7 trường (tên, email, SĐT, MST, mã định danh, mã quan hệ ngân sách, số hộ chiếu) trong **tối đa 2 giờ**. Không lấy / quá 2 giờ ⇒ phát hành theo thông tin hợp đồng; quá 2 giờ thì ẩn nút Xuất hóa đơn.
- **Điều kiện (BR-XHD-03):** delay **2 giờ** từ lúc tạo đơn, áp cả DV và TB.
- **Lịch (BR-XHD-01):** worker **2 giờ/lần** (0h–2h, 2h–4h, …) + mốc **22:05** chốt dữ liệu 0h–22h.
- **Phân luồng (BR-XHD-02):** tín hiệu sau **22h** ⇒ realtime.

## Phạm vi test XHD
Chỉ nhóm 5 — FPT Play Stands Alone — `RULE-XHD.md` §1.1.

## Hình thức triển khai
Kênh FPL **không có hình thức triển khai** ⇒ không có phiếu triển khai; **BBĐT auto ký** (nguồn: user cung cấp 04/11/2026).

## Chưa có thông tin
Cách tạo đơn chi tiết, luồng khoản thu.
