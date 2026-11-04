# RULE TOOL CHÍNH SÁCH & CÁC KÊNH BÁN HÀNG (STG)

> Nguồn: thông tin user cung cấp ngày 03/11/2026. Dùng kèm `RULE-XHD.md`.

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

## 2. Quy tắc hình thức triển khai thiết bị (chung)

Thiết bị có nhiều hình thức triển khai tùy theo chính sách khai báo:

| Hình thức triển khai | Đẩy qua |
|---|---|
| Không, Quầy, Sale | **Tool quầy** |
| NCC-Samsung, NCC-Casper | **M-Vendor** |
| TIN/PNC | **Phiếu triển khai** |

### 2.1 Dịch vụ nào triển khai TIN/PNC (theo qc-iia)

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

**Theo kênh bán (thông tin user cung cấp):**
- **W-Sale:** đơn chỉ có hình thức TIN/PNC (Internet, Pay).
- **Shopee, TikTok:** 2 hình thức — Quầy (chính sách shipper giao hàng) và TIN/PNC.
- **DKOL:** Camera triển khai Quầy (shipper giao hàng) hoặc TIN/PNC; TV đẩy qua Vendor; Ultra Fast SA, FPT Play SA, HyperFast SA **không có phiếu triển khai**.
- **Desktop, Mobile:** theo chính sách khai báo (bảng §2).

---

## 3. Bảng tổng hợp kênh bán

| Kênh | Owner | Nơi tạo đơn | Loại đơn | Trạng thái / ghi chú |
|---|---|---|---|---|
| API | — | — | — | Gồm TGDD và F-Retail, **chưa tách** |
| App Partner | — | — | — | Chưa có thông tin |
| CRM-APP | PhuongTT3 | App FPT Life | — | Chỉ bán **cloud** trong nhóm FPT Camera Only |
| CRM | HoangPHD | Web CRM | — | Chỉ bán dịch vụ **FPL** |
| Desktop | KhiemBT | Web SOP | Bán mới + bán thêm | 19 dịch vụ |
| Mobile | KhiemBT | App SOP | Bán mới + bán thêm | 19 dịch vụ |
| F-Retail | — | — | — | Đang có issue 3-2 cấp |
| TGDD | — | — | — | Đang có issue 3-2 cấp |
| HiFPT | — | — | — | Đã **move sang DKOL** |
| MBBank | — | — | — | Chưa có trên PRO do vướng chính sách hợp tác 2 bên |
| Momo | HaiPV7 | Nhờ owner tạo | — | Đang bán Play và combo Play; Camera đang off, chưa hẹn mở lại |
| Shop | — | — | — | Chưa có thông tin |
| Shopee | HaiPV7 | Web admin SPF (Retry Order) | Bán mới | Hạn key 4h |
| TikTok | HaiPV7 | Web admin SPF (Retry Order) | Bán mới | |
| SR-KPDV | — | — | — | Chưa có thông tin |
| Ven-vrace | — | — | — | Chưa có thông tin |
| WebSDK | — | — | — | Chưa có thông tin |
| W-Sale | HoangVT11 | Web W-Sale | — | Internet, Pay; chỉ TIN/PNC |
| DKOL | TaiTT13 | HiFPT / FPT.vn | Bán mới + bán thêm | Gồm luồng HiFPT, FPT.vn |
| FPL | — | Web FPL (dev.fptplay.vn) | — | |
| Outside | — | — | — | Chưa có thông tin |
| VNTT | HaiPV7 | — | — | Owner chỉ ghi nhận HĐ, **không tạo khoản thu** |

---

## 4. Chi tiết từng kênh

### 4.0 Sau khi tạo đơn hàng (chung mọi kênh)
- Tạo đơn hàng xong sẽ có **thông tin hợp đồng**.
- Kiểm tra thông tin hợp đồng ở **tool Tình trạng** trên **Inside** (vd: hợp đồng con có thông tin hợp đồng cha cũng xem ở đây).
- Hợp đồng được dùng khi xuất hóa đơn: thông tin khách, hiệu lực hợp đồng, chi nhánh quản lý, mã tỉnh theo địa chỉ hợp đồng; các loại hợp đồng tổ chức / con / SST / nghiệp vụ có rule riêng (xem `RULE-XHD.md` §4, §6, §7).

### 4.1 CRM
- **Owner:** HoangPHD
- **Web:** https://crm-stag.fpt.net/
- **Chỉ bán dịch vụ FPL.**
- **Cách tạo đơn:**
  1. Tạo đơn cơ hội
  2. Tạo báo giá
  3. Đánh dấu version
  4. Chờ 5 phút
  5. Tạo đơn hàng

### 4.2 CRM-APP
- **Owner:** PhuongTT3
- Lên đơn từ **App FPT Life**.
- Chỉ bán **cloud** trong nhóm dịch vụ **FPT Camera Only**.

### 4.3 Desktop
- **Owner:** KhiemBT
- **Web SOP:** https://portal-sop-stg.fpt.vn/user/login/basic-auth
- **Loại đơn:** bán mới + bán thêm
- **Dịch vụ (19):** Internet, FPT Camera Only, FPT Camera Combo, FPT Play Stands Alone, Sản phẩm khác, FPT Play, Tổng đài Oncall, FPT Smart Home, Ultra Fast Stand Alone, FPro, FSafe Go, VioEdu Stand Alone, VIP 247, SIM data, Pay Wifi, Ultra Fast, FPT Camera B2B, HyperFast, FPT AI Wi-Fi
- **Hình thức triển khai thiết bị:** theo bảng §2.
- **Cách tạo đơn:**
  1. Chọn **Thêm khách hàng**.
  2. Nhập thông tin đầy đủ.
  3. Chọn **Tạo và lên đơn** → bấm **Xác nhận**.
  4. Lựa chọn đơn bán thêm / bán mới.
  5. Chọn menu **Đơn hàng**.
  6. Tại tab bán thêm / bán mới chọn dấu **+**.
  - **Bán mới:**
    1. Chọn **+** ở bán mới
    2. Nhấn icon tìm kiếm ở thông tin địa chỉ
    3. Chọn/nhập địa chỉ
    4. Nhấn **Xác nhận**
    5. Chọn đối tượng khách hàng (nếu muốn thay đổi)
    6. Chọn dịch vụ cần mua
    7. Nhấn **Chi tiết giỏ hàng** → chọn **Xác nhận**
    8. Cập nhật thông tin khách hàng
    9. Chọn **Tạo báo giá**
    10. Chọn **Tạo hợp đồng**
    11. Có thể cập nhật hợp đồng nếu muốn
  - **Bán thêm:**
    1. Chọn **+** ở bán thêm
    2. Tìm kiếm hợp đồng → chọn HĐ bán thêm
    3. Nhấn icon **+**
    4. Chọn dịch vụ cần mua
    5. Nhấn **Chi tiết giỏ hàng** → chọn **Xác nhận**
    6. Cập nhật thông tin khách hàng (nếu muốn)
    7. Chọn **Tạo báo giá**
    8. Chọn **Tạo hợp đồng**
    9. Có thể cập nhật hợp đồng nếu muốn

### 4.4 Mobile
- **Owner:** KhiemBT
- Tạo đơn từ **App SOP**.
- **Loại đơn, dịch vụ, hình thức triển khai:** giống Desktop (§4.3).
- **Cách tạo đơn:**
  1. Chọn menu **Đơn hàng**.
  2. Tại tab bán thêm / bán mới chọn dấu **+**.
  - **Bán mới:** giống bước Bán mới của Desktop (chọn + ở bán mới → tìm địa chỉ → xác nhận → đối tượng KH → dịch vụ → chi tiết giỏ hàng → cập nhật thông tin KH → tạo báo giá → tạo hợp đồng → cập nhật HĐ nếu muốn).
  - **Bán thêm:** giống bước Bán thêm của Desktop (chọn + ở bán thêm → tìm HĐ → icon + → dịch vụ → chi tiết giỏ hàng → cập nhật thông tin KH → tạo báo giá → tạo hợp đồng → cập nhật HĐ nếu muốn).

### 4.5 Momo
- **Owner:** HaiPV7
- Tạo đơn: **nhờ owner**.
- Đang bán **Play** và **combo Play**. Camera đang **off**, chưa hẹn mở lại.

### 4.6 Shopee
- **Owner:** HaiPV7
- **Bán mới:** Internet, FPT Camera Only, FPT Play Stands Alone, FPT Play, Sản phẩm khác.
- **Chuẩn bị:** nhờ owner kéo đơn từ PRO về (kèm **refcode**), sao chép chính sách về staging, nhờ owner **map SKU**.
- ⚠️ Đơn Shopee có **hạn key 4 giờ** — hết 4h thì nhờ owner kéo key về lại.
- **Hình thức triển khai:** **Quầy** (có chính sách shipper giao hàng) và **TIN/PNC**.
- **Cách tạo đơn:** xem §4.8.

### 4.7 TikTok
- **Owner:** HaiPV7
- **Bán mới:** Internet, FPT Camera Only, FPT Play Stands Alone, FPT Play, Sản phẩm khác, FPT Camera Combo.
- **Chuẩn bị:** nhờ owner kéo đơn từ PRO về (kèm **refcode**), sao chép chính sách về staging, nhờ owner **map SKU**.
- **Hình thức triển khai:** **Quầy** (có chính sách shipper giao hàng) và **TIN/PNC**.
- **Cách tạo đơn:** xem §4.8.

### 4.8 Cách tạo đơn Shopee / TikTok (Web admin SPF)
1. Truy cập web admin: http://saleplatform-stag.fpt.net/web-admin/Account/Login
2. Chọn menu **Retry Order**.
3. Tìm kiếm đơn hàng với **refcode** owner cung cấp.
4. Nếu có thông tin thì thao tác **ngắt kết nối đơn hàng**.
5. Chuyển qua tab **Cập nhật địa chỉ, SĐT**.
6. Tìm kiếm đơn hàng với refcode owner cung cấp.
7. Nhấn **Load**.
8. Nhập thông tin đầy đủ.
9. Nhấn **Submit**.

### 4.9 W-Sale
- **Owner:** HoangVT11
- **Web:** http://wsale-stag.fpt.net/ — host `172.20.18.252  wsale-stag.fpt.net`
- **Dịch vụ:** Internet, Pay.
- Tạo đơn dịch vụ **Swap**: nhờ anh **HaiTN16** cung cấp data rồi lên tạo đơn.
- Đơn **chỉ có hình thức triển khai TIN/PNC**.

### 4.10 DKOL
- **Owner:** TaiTT13
- FPT.vn và HiFPT đều có **SaleChannel = DKOL**.
- **Sale team:**
  - Lên đơn từ **HiFPT:** sale team *Khách hàng bình thường HiFPT*.
  - Lên đơn từ **FPT.vn:** DKOL (KH vãng lai), AM (sale IBB), CTV_sale (208), ANCS (239), Đối tác (238).
- **HiFPT:**
  - Bán mới: Net, combo Net–Camera, combo Net–PayTV, TripleF Net–PayTV–Cam, Ultra Fast SA, FPT Play SA, Smart Home, Smart TV, thiết bị modem, thiết bị y tế, Camera combo (lẻ).
  - Bán thêm: Cloud, Camera, FPT Play (billing).
- **FPT.vn:**
  - KH vãng lai: như bán mới HiFPT + **HyperFast SA**, **trừ thiết bị y tế**.
  - Sale team còn lại: chủ yếu Net và combo của Net.
  - Prepaid là bán mới nhưng ghi nhận cho sale.
  - Bán thêm: Camera ưu đãi, FPT Play sub.
  - Nâng cấp FPT Play (sub).
- **Hình thức triển khai:**
  - Camera: **Quầy** (có chính sách shipper giao hàng) hoặc **TIN/PNC**.
  - TV: đang đẩy qua **Vendor**.
  - Ultra Fast SA, FPT Play SA, HyperFast SA: **không có phiếu triển khai**.

### 4.11 FPL
- Lên đơn từ web FPL: **dev.fptplay.vn**

### 4.12 VNTT
- **Owner:** HaiPV7
- Owner chỉ **ghi nhận HĐ**, **không tạo khoản thu**.

### 4.13 Kênh có issue / chưa có thông tin
- **API:** gồm TGDD và F-Retail, chưa tách.
- **F-Retail, TGDD:** đang có issue 3-2 cấp.
- **HiFPT:** đã move sang DKOL.
- **MBBank:** chưa có trên PRO do vướng chính sách hợp tác 2 bên.
- **Chưa có thông tin:** App Partner, Shop, SR-KPDV, Ven-vrace, WebSDK, Outside.

---

## 5. Danh sách URL / host STG

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

---

## 6. Luồng thanh toán & tạo đơn theo phương thức thanh toán (PTTT)

> Nguồn: thông tin user cung cấp ngày 03/11/2026.

### 6.1 PTTT = Thanh toán khi triển khai (mọi kênh có khoản thu)
Hệ thống gen **đồng thời**:
- Khoản thu
- Phiếu thi công
- Biên bản điện tử
- Tình trạng đơn hàng = **Chưa thanh toán**

### 6.2 PTTT khác "Thanh toán khi triển khai"

| Kênh | Luồng |
|---|---|
| **DKOL** | Khách hàng **phải thanh toán xong** mới tạo đơn ⇒ đơn tạo ra với tình trạng **Đã thanh toán**, khoản thu **Đã thanh toán** ⇒ sau đó mới gen **phiếu thi công** và **biên bản điện tử**. |
| **Desktop / Mobile** | Tạo đơn **Chưa thanh toán** + khoản thu **Chưa thanh toán** ⇒ khách thanh toán xong ⇒ mới gen **phiếu thi công** và **biên bản điện tử**. |

### 6.3 Sau khi thanh toán khoản thu
- Khoản thu phải chuyển sang **Đã thanh toán**.
- Tiền được **đẩy vào cọc**.
- **Kiểm tra khoản thu:** Inside › menu **Foxpay › Thanh toán online › Đối soát khoản thu online**.

### 6.4 Shopee / TikTok (TMĐT) — không có khoản thu

**Lần 1 — Đơn ghi nhận khách hàng đã thanh toán cho sàn**
1. TikTok/Shopee gửi đơn.
2. SPF tạo đơn với trạng thái **Chưa thanh toán**.
3. Tạo **Order Transaction** với trạng thái **Thanh toán tạm** (KH đã thanh toán cho sàn).
4. Cập nhật đơn SPF sang **Đã thanh toán**.
5. Phiếu thi công (PTC) hoàn tất.
6. Xuất hóa đơn theo rule quy định (xem `RULE-XHD.md`) và **gạch nợ hóa đơn tạm**.

**Lần 2 — Sàn quyết toán tiền về FTEL**
1. TikTok/Shopee gửi thông tin quyết toán.
2. SPF **không cập nhật** đơn hàng.
3. Order Transaction cập nhật trạng thái **Đã thanh toán**; **Order Paid** ghi nhận:
   - Phí sàn
   - Số tiền FTEL thực lãnh
4. IIA thực hiện **gạch nợ hóa đơn thật**.

---

## 7. Cách hoàn tất phiếu giao hàng / triển khai (STG)

> Nguồn: thông tin user cung cấp ngày 03/11/2026. Hoàn tất phiếu = sinh **tín hiệu giao hàng hoàn tất** để xuất hóa đơn thiết bị (xem `RULE-XHD.md` §2, §4).

### 7.1 Hoàn tất phiếu thi công (PTC) — hình thức TIN/PNC
1. Vào **Inside new v5 › Thông tin chung › Triển khai**.
2. Nhập số hợp đồng.
3. **Phân tuyến**.
4. Truy cập http://partner-stag.fpt.net/pt-portal/bypass
5. Chọn **Bypass** → tích **tất cả** → nhập hợp đồng → nhập **Thời gian hết hạn bypass** (tối đa 24 giờ) → nhập **Nguyên nhân bypass** → nhấn **Cập nhật**.
6. Quay lại phiếu thi công → chọn trạng thái **Đã xử lý hoàn tất**.

### 7.2 Hoàn tất phiếu giao hàng tại quầy có shipper giao hàng
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

### 7.3 Hoàn tất phiếu giao hàng tại quầy không có shipper giao hàng

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

### 7.4 Thao tác khác với phiếu thi công
- **Hủy PTC / Chuyển thi công (thi công lại):** Inside › **Quản lý hợp đồng › HĐ NOT OK V3 › PTC NOT OK**.
- **Phân công quota phiếu thi công:** Fox ERP › **Quản lý đối tác › Quản lý Block › Quota PTC - TUT**.
