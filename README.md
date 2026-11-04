# Ăn Xin Online

Trang xin lòng hảo tâm một file duy nhất (`index.html`), có mã **VietQR** để khách quét bằng app ngân hàng nào cũng chuyển được (Napas 247).

## Có gì trong trang

- Tấm bìa carton "XIN LÒNG HẢO TÂM", chữ trên bìa đổi theo món khách chọn.
- **Cái bát** (khung bên phải, trên điện thoại nằm ngay dưới tấm bìa): chọn món (5K trà đá, 10K mì tôm, …) hoặc tự nhập số tiền, nhập tên. Mã QR tự cập nhật số tiền và nội dung chuyển khoản. Có nút chép số tài khoản, số tiền, nội dung.
- Đơn xin ủng hộ, bảng giá lòng tốt, phần tiền đi đâu, bảng vàng ân nhân, lời người quen, hỏi đáp, nút chia sẻ.
- Bấm "Em đã bỏ vào bát rồi" thì hiện **bằng khen** cho khách chụp màn hình.
- Tự đổi giao diện sáng hoặc tối theo máy, hiển thị tốt trên điện thoại.

## Đổi sang tài khoản của bạn

Mở `index.html`, tìm khối `CONFIG` ở đầu phần `<script>` rồi sửa:

```js
const CONFIG = {
  bank: "MB",                     // VCB, MB, TCB, ACB, BIDV, VIETINBANK, TPBANK, VPBANK, …
  accountNumber: "0000000000",    // số tài khoản của bạn
  accountName: "NGUYEN VAN NGHEO",// tên chủ TK, viết hoa không dấu
  ownerName: "Nguyễn Văn Nghèo",
  ...
  goal: { title: "Đóng tiền trọ tháng 12", target: 2000000, raised: 0 },
  contactUrl: "",                 // link Facebook/Zalo để khách nhắn
  donors: []                      // { name: "Anh Tuấn", amount: 50000 }
};
```

Khi `accountNumber` còn là `0000000000`, trang hiện chữ **Bản mẫu** để không ai chuyển nhầm.
Danh sách mã ngân hàng nằm trong `BANKS`, ngay dưới `CONFIG`.

## Đưa lên mạng miễn phí bằng GitHub Pages

1. Vào repo trên GitHub, chọn **Settings → Pages**.
2. Ở **Build and deployment**, chọn *Deploy from a branch*, chọn nhánh chứa `index.html`, thư mục `/ (root)`, bấm **Save**.
3. Khoảng 1 phút sau trang chạy ở `https://<tên-github>.github.io/an-xin-online-/`.

Lưu ý: GitHub Pages của tài khoản miễn phí chỉ bật được cho repo **public**.

## Kỹ thuật

- Mã QR theo chuẩn EMVCo/VietQR (dịch vụ `QRIBFTTA`, có CRC16), tạo ngay trên trình duyệt, không gửi dữ liệu đi đâu.
- Thư viện vẽ QR `qrcode-generator@1.4.4` tải từ cdnjs, nếu lỗi thì tự chuyển sang jsDelivr, rồi unpkg.
- Font: Sriracha (chữ viết tay), Be Vietnam Pro, JetBrains Mono, đều có bộ tiếng Việt.
