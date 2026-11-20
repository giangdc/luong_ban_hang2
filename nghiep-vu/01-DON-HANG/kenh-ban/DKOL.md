# KÊNH DKOL (SaleChannelID 4)

> Tách từ `RULE-CHINH-SACH-KENH-BAN.md` (nguồn: user cung cấp 03/11/2026). Rule chung: [00-CHUNG.md](00-CHUNG.md) · Rule XHD: [`../../../RULE-XHD.md`](../../../RULE-XHD.md).

## Thông tin chung

| Mục | Nội dung |
|---|---|
| Owner | TaiTT13 |
| Nơi tạo đơn | **HiFPT** và **FPT.vn** — cả 2 đều có **SaleChannel = DKOL** |
| Loại đơn | Bán mới + bán thêm |
| Ghi chú | Kênh HiFPT cũ đã move sang DKOL |

## Sale team
- Lên đơn từ **HiFPT:** sale team *Khách hàng bình thường HiFPT*.
- Lên đơn từ **FPT.vn:** DKOL (KH vãng lai), AM (sale IBB), CTV_sale (208), ANCS (239), Đối tác (238).

## Dịch vụ

### HiFPT
- **Bán mới:** Net, combo Net–Camera, combo Net–PayTV, TripleF Net–PayTV–Cam, Ultra Fast SA, FPT Play SA, Smart Home, Smart TV, thiết bị modem, thiết bị y tế, Camera combo (lẻ).
- **Bán thêm:** Cloud, Camera, FPT Play (billing).

### FPT.vn
- **KH vãng lai:** như bán mới HiFPT + **HyperFast SA**, **trừ thiết bị y tế**.
- **Sale team còn lại:** chủ yếu Net và combo của Net.
- Prepaid là bán mới nhưng ghi nhận cho sale.
- **Bán thêm:** Camera ưu đãi, FPT Play sub.
- **Nâng cấp:** FPT Play (sub).

## Hình thức triển khai
- **TIN/PNC (phiếu thi công):** dịch vụ cần triển khai, kích hoạt tại địa chỉ đăng ký. Phiếu thi công **không phải** dịch vụ Camera (nguồn: user cung cấp 17/11/2026).
- **Camera:** **Quầy** (có chính sách shipper giao hàng).
- **TV:** đang đẩy qua **Vendor**.
- **Ultra Fast SA, FPT Play SA, HyperFast SA:** **không có phiếu triển khai**, **BBĐT auto ký**.

Cách hoàn tất phiếu: [00-CHUNG.md §5](00-CHUNG.md#5-cách-hoàn-tất-phiếu-giao-hàng--triển-khai-stg).

## Thanh toán & khoản thu
- **PTTT = Thanh toán khi triển khai:** gen đồng thời khoản thu, phiếu thi công, biên bản điện tử; đơn = **Chưa thanh toán**.
- **PTTT Online:** khách hàng **phải thanh toán xong** mới tạo đơn ⇒ đơn tạo ra với tình trạng **Đã thanh toán**, khoản thu **Đã thanh toán** ⇒ sau đó mới gen **phiếu thi công** và **biên bản điện tử**.
- Sau khi thanh toán: tiền **đẩy vào cọc**. Kiểm tra: Inside › Foxpay › Thanh toán online › Đối soát khoản thu online.
- **Thanh toán → cọc → hóa đơn → gạch nợ** (nguồn: user cung cấp 17/11/2026): khách thanh toán ⇒ khoản thu **Đã thanh toán** ⇒ **nhập cọc** ⇒ nhận tín hiệu xuất hóa đơn thì xuất hóa đơn ⇒ có cọc thì **gạch nợ hóa đơn**, cập nhật hóa đơn **Đã thanh toán** ⇒ hóa đơn dịch vụ **trả trước** thì **add tiền trả trước**. Chi tiết: [00-CHUNG.md §4.3](00-CHUNG.md#43-sau-khi-thanh-toán-khoản-thu).

## Phạm vi test XHD
Bán mới 8 nhóm {1,4,5,6,7,9,10,21} · bán thêm 3 nhóm {1,4,7} — `RULE-XHD.md` §1.1.
