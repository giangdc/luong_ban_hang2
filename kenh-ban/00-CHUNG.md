# RULE CHUNG CHO MỌI KÊNH BÁN (STG)

> Tách từ `RULE-CHINH-SACH-KENH-BAN.md` (nguồn: thông tin user cung cấp ngày 03/11/2026). Dùng kèm [`../RULE-XHD.md`](../RULE-XHD.md).
> Rule riêng từng kênh: xem [mục lục](../RULE-CHINH-SACH-KENH-BAN.md).

---

## 1. Tool chính sách (BP)

- **URL:** http://bp-stag.fpt.net/
- **Host:** `172.20.18.252  bp-stag.fpt.net`
- **Mục đích:** khai báo chính sách bán hàng cho các kênh FTEL.

### Chính sách quyết định gì
- **Giá bán** của SPDV.
- **Các gói bán** của dịch vụ.
- **Khu vực bán** (bán ở khu vực nào).
- **Thiết bị đi kèm** (bán kèm thiết bị gì).
- **Đối tượng khách hàng** được bán.
- **Kênh bán** (bán ở kênh nào).
- **Đơn vị bán hàng**.
- **Phương thức thanh toán**.
- **Loại khách hàng:** khách hàng mới hay khách hàng cũ.
- **Hình thức triển khai** của thiết bị (xem §2).

### Cách tạo chính sách bán hàng
1. Tìm chính sách bán hàng có sẵn với dịch vụ muốn bán.
2. **Sao chép** chính sách đó.
3. Chọn **Sửa** → chọn/nhập thông tin muốn tạo → **Lưu**.
4. Nhấn **Trở về** → chọn **Gửi đề xuất**.
5. Vào menu **Bán hàng** → tab **Bán hàng**.
6. Tìm mã chính sách vừa gửi đề xuất → tích chọn → **Tạo quyết định**.
7. Nhập thông tin hợp lệ → **Lưu**.

---

## 2. Quy tắc hình thức triển khai thiết bị

Thiết bị có nhiều hình thức triển khai tùy theo chính sách khai báo:

| Hình thức triển khai | Đẩy qua |
|---|---|
| Không, Quầy, Sale | **Tool quầy** |
| NCC-Samsung, NCC-Casper | **M-Vendor** |
| TIN/PNC | **Phiếu triển khai** |

### 2.1 Dịch vụ nào triển khai theo hình thức nào (theo qc-iia)

> Nguồn: `qc-iia/00_input/v2.0/Doc/AnhNQ75-List HT Triển khai.xlsx` (sheet "1. HT Triển khai") + các clarification CL-XHD-27, CL-XHD-34 (chốt 20/10/2026).
> ⚠️ File này **không có bảng liệt kê từng dịch vụ ↔ hình thức triển khai**; hình thức thực tế của mỗi thiết bị do **chính sách khai báo** trên tool BP quyết định.

| HT triển khai | Áp dụng cho dịch vụ | Chủ thể | Đầu ra / tín hiệu |
|---|---|---|---|
| **TIN/PNC** | Thiết bị cần **triển khai, kích hoạt tại địa chỉ đăng ký** của đơn (không giới hạn nhóm dịch vụ — vd Internet kèm modem, như TC của qc-iia) | TIN/PNC | Phiếu thi công theo đơn hàng, loại **Triển khai** |
| **TIN/PNC giao hàng** | **Chỉ Camera Offnet** và **Thiết bị lẻ** — giao hàng, không yêu cầu kích hoạt | TIN/PNC | Phiếu thi công theo đơn hàng, loại **Giao hàng** |
| Quầy | Chỉ Camera Offnet, Thiết bị lẻ | DVKH CN | Phiếu giao dịch bán thiết bị tại quầy |
| Sale | Chỉ Thiết bị lẻ (quản lý MAC) | Nhân viên bán hàng | Phiếu giao dịch bán thiết bị tại quầy |
| NCC Samsung / Sony / Casper | Chỉ Thiết bị lẻ mua từ NCC bán lại (TV…) | Nhà cung cấp | Đơn đặt hàng Vendor + mã vận đơn |
| FTI | SPDV đặc thù, dự án: **OnCall, Camera B2B, ListLine**… (HN, HCM, CNx) | Đối tác FTI | Phiếu thi công, loại Triển khai |
| Không / None | Dịch vụ không cần triển khai, vd **dịch vụ Code SA** (đẩy code qua SMS) | — | Không có phiếu |

**Quy tắc gộp về luồng TIN/PNC:**
- Đơn có **≥1 SPDV** mix TIN/PNC với Quầy/Sale ⇒ **cả đơn** tự xử lý theo luồng TIN/PNC (thiết bị giao tại quầy cũng chờ phiếu thi công).
- Hàng hóa mix "Không" + TIN/PNC ⇒ triển khai bởi TIN/PNC (theo phiếu thi công).
- Chỉ có "Không" ⇒ không đẩy triển khai/giao hàng; thiết bị "Không" chỉ xuất hóa đơn nếu quầy gửi tín hiệu.

**Hình thức triển khai theo kênh** (chi tiết trong file từng kênh):

| Kênh | Hình thức triển khai |
|---|---|
| Desktop, Mobile | Theo chính sách khai báo (bảng §2) |
| DKOL | Camera: Quầy (shipper) hoặc TIN/PNC · TV: Vendor · Ultra Fast SA, FPT Play SA, HyperFast SA: không có phiếu |
| Shopee, TikTok | Quầy (chính sách shipper giao hàng) và TIN/PNC |
| W-Sale | Chỉ TIN/PNC |

---

## 3. Sau khi tạo đơn hàng (mọi kênh)

- Tạo đơn hàng xong sẽ có **thông tin hợp đồng**.
- Kiểm tra thông tin hợp đồng ở **tool Tình trạng** trên **Inside** (vd: hợp đồng con có thông tin hợp đồng cha cũng xem ở đây).
- Hợp đồng được dùng khi xuất hóa đơn: thông tin khách, hiệu lực hợp đồng, chi nhánh quản lý, mã tỉnh theo địa chỉ hợp đồng; các loại hợp đồng tổ chức / con / SST / nghiệp vụ có rule riêng (xem `RULE-XHD.md` §4, §6, §7).

---

## 4. Thanh toán & khoản thu (chung)

### 4.1 PTTT = Thanh toán khi triển khai (mọi kênh có khoản thu)
Hệ thống gen **đồng thời**:
- Khoản thu
- Phiếu thi công
- Biên bản điện tử
- Tình trạng đơn hàng = **Chưa thanh toán**

### 4.2 PTTT khác "Thanh toán khi triển khai" — theo kênh

| Kênh | Luồng | Chi tiết |
|---|---|---|
| DKOL | KH thanh toán xong mới tạo đơn ⇒ đơn và khoản thu **Đã thanh toán** ⇒ gen phiếu thi công, biên bản điện tử | [DKOL.md](DKOL.md) |
| Desktop / Mobile | Tạo đơn và khoản thu **Chưa thanh toán** ⇒ KH thanh toán ⇒ gen phiếu thi công, biên bản điện tử | [DESKTOP.md](DESKTOP.md), [MOBILE.md](MOBILE.md) |
| Shopee / TikTok | **Không có khoản thu**, dùng Order Transaction (2 lần) | [SHOPEE.md](SHOPEE.md), [TIKTOK.md](TIKTOK.md) |
| VNTT | Chỉ ghi nhận HĐ, **không tạo khoản thu** | [VNTT.md](VNTT.md) |

### 4.3 Sau khi thanh toán khoản thu
- Khoản thu phải chuyển sang **Đã thanh toán**.
- Tiền được **đẩy vào cọc**.
- **Kiểm tra khoản thu:** Inside › menu **Foxpay › Thanh toán online › Đối soát khoản thu online**.

---

## 5. Cách hoàn tất phiếu giao hàng / triển khai (STG)

> Hoàn tất phiếu = sinh **tín hiệu giao hàng hoàn tất** để xuất hóa đơn thiết bị (xem `RULE-XHD.md` §2, §4).

### 5.1 Hoàn tất phiếu thi công (PTC) — hình thức TIN/PNC
1. Vào **Inside new v5 › Thông tin chung › Triển khai**.
2. Nhập số hợp đồng.
3. **Phân tuyến**.
4. Truy cập http://partner-stag.fpt.net/pt-portal/bypass
5. Chọn **Bypass** → tích **tất cả** → nhập hợp đồng → nhập **Thời gian hết hạn bypass** (tối đa 24 giờ) → nhập **Nguyên nhân bypass** → nhấn **Cập nhật**.
6. Quay lại phiếu thi công → chọn trạng thái **Đã xử lý hoàn tất**.

### 5.2 Hoàn tất phiếu giao hàng tại quầy có shipper giao hàng
1. Vào tool **Quản lý chuỗi cung ứng › Giao dịch thiết bị** → tìm hợp đồng.
2. **Nhận xử lý** phiếu.
3. Chọn kho xuất **KTN test**.
4. **Đề nghị xuất vật tư**.
5. Trên tool **SCM** (https://ftelscm-uat.fpt.net — host `172.20.18.252  ftelscm-uat.fpt.net`): **Quản lý kho › Nhập kho › Tạo phiếu nhập** với hàng hóa đang cần giao, chọn kho **KTN test MAC**.
6. **Quản lý kho › Xác nhận tạm ứng từ Inside**.
7. Quay lại phiếu giao dịch thiết bị → chọn **Lưu và đóng hàng**.
8. Trên tool GHTK (https://khachhang-staging.ghtklab.com/web/): **Thông tin tài khoản › Cấu hình API**.
9. **Webhook** → chọn **Test** → nhập **mã vận đơn** vào ô Mã đơn hàng.
10. Chọn **cập nhật trạng thái 5**.

### 5.3 Hoàn tất phiếu giao hàng tại quầy không có shipper giao hàng

**Trường hợp đã có MAC:**
1. Vào tool **Quản lý chuỗi cung ứng › Giao dịch thiết bị** → tìm hợp đồng.
2. Chọn đối tác **Bến Thành**, **Tổ 300**.
3. Chọn **Chỉnh sửa** → chọn **danh sách MAC** → nhấn **Lưu**.
4. Chọn kết quả xử lý **Hoàn tất**.
5. Nhấn **Xác nhận**.

**Trường hợp chưa có MAC** (tạo MAC trước, rồi làm lại các bước trên):
1. Vào tool **Quản lý vật tư quầy**.
2. Chọn **Tạm ứng vật tư**.
3. Chọn **Đề nghị tạm ứng**.
4. Chọn đối tác, tổ, vật tư muốn tạm ứng.
5. Nhấn **Tạo phiếu**.
6. Nhập số lượng → **Xác nhận**.
7. Trên tool **SCM** (https://ftelscm-uat.fpt.net — host `172.20.18.252  ftelscm-uat.fpt.net`): **Quản lý kho › Nhập kho › Tạo phiếu nhập** với hàng hóa đang cần giao, chọn kho **KTN test MAC**.
8. **Quản lý kho › Xác nhận tạm ứng từ Inside**.
9. Chọn kho **KTN test MAC**, tích **Bảo hành V2**.
10. Chọn **phiếu tạm ứng** → nhập **MAC vừa tạo ở phiếu nhập**.
11. Nhấn **Xác nhận V2**.

### 5.4 Thao tác khác với phiếu thi công
- **Hủy PTC / Chuyển thi công (thi công lại):** Inside › **Quản lý hợp đồng › HĐ NOT OK V3 › PTC NOT OK**.
- **Phân công quota phiếu thi công:** Fox ERP › **Quản lý đối tác › Quản lý Block › Quota PTC - TUT**.

---

## 6. Danh sách URL / host STG

| Hệ thống | URL | Host |
|---|---|---|
| Tool chính sách (BP) | http://bp-stag.fpt.net/ | 172.20.18.252 bp-stag.fpt.net |
| CRM | https://crm-stag.fpt.net/ | — |
| SOP (Desktop) | https://portal-sop-stg.fpt.vn/user/login/basic-auth | — |
| SPF Web admin | http://saleplatform-stag.fpt.net/web-admin/Account/Login | — |
| W-Sale | http://wsale-stag.fpt.net/ | 172.20.18.252 wsale-stag.fpt.net |
| Partner portal (bypass PTC) | http://partner-stag.fpt.net/pt-portal/bypass | — |
| SCM (quản lý kho) | https://ftelscm-uat.fpt.net | 172.20.18.252 ftelscm-uat.fpt.net |
| GHTK staging (webhook shipper) | https://khachhang-staging.ghtklab.com/web/ | — |
| FPL | dev.fptplay.vn | — |
