# Báo cáo bản địa hóa tiếng Việt

**Dự án:** HoyoLab Auto

**Nhánh Git:** `codex/vietnamese-translation`

**Trạng thái:** Đã thêm catalog tiếng Việt cho hệ thống bản địa hóa của ứng dụng Node.js.

## Tóm tắt

Đã thêm tiếng Việt vào cơ chế bản địa hóa hiện có của dự án. Catalog mới bao phủ toàn bộ **800/800 chuỗi tiếng Anh** trong catalog đang dùng làm nguồn đối chiếu. Phần dịch gồm nhãn và trợ giúp trong trình tạo cấu hình, lệnh, thông báo, trạng thái trò chơi, mô tả tác vụ định kỳ, lỗi và log.

Các vị trí chính:

- `localization/vi.js`: catalog tiếng Việt, mã ngôn ngữ `vi`, locale `vi-VN`.
- `setup/config/catalogs.js`: chỉ mục được tạo lại để trình tạo cấu hình nhận diện `vi.js`.
- `reports/bao-cao-ban-dia-hoa-tieng-viet/BAO-CAO.md`: báo cáo này.

## Cách bật tiếng Việt

Trong `config.json5`, đặt ngôn ngữ cấp cao nhất như sau rồi khởi động lại ứng dụng:

```json5
language: 'vi-vn',
```

Trình tạo cấu hình cũng có mục ngôn ngữ và có thể chọn tiếng Việt. Khi trang được mở trực tiếp từ dự án, chỉ mục catalog đã được cập nhật để trình tạo tải bản dịch.

## Phạm vi và quy ước

- Dịch toàn bộ 800 thông điệp có trong catalog nguồn hiện tại.
- Giữ nguyên các placeholder dạng `{0}`, `{1}`, tên cấu hình, trạng thái giao thức, tên game, UID, token, URL và mã lệnh.
- Giữ cú pháp Markdown/định dạng nền tảng trong nội dung Discord và Telegram.
- Tên người chơi, dữ liệu do API trả về và giá trị người dùng nhập không bị dịch tự động.
- README và tài liệu công khai vẫn bằng tiếng Anh theo quy ước trong `localization/README.md`.
- Google Apps Script là bản độc lập, không tự tải catalog từ dự án; phần đó chưa được bản địa hóa trong thay đổi này.

## Kiểm tra đã thực hiện

- Nạp `localization/vi.js` bằng Node.js để xác nhận catalog hợp lệ về cú pháp và metadata.
- Đối chiếu từng khóa với catalog nguồn: đủ 800/800 khóa.
- So sánh placeholder nguồn và bản dịch: không có sai khác.
- Chạy `scripts/generate-localization-index.js`; chỉ mục tạo ra liệt kê cả `it.js` và `vi.js`.
- Chạy `npm test`: 41/42 test đạt. Test `the setup index discovers only existing catalog files with Node filename precedence` thất bại trên Windows vì fixture tạo đồng thời `IT.js` và `it.js`, hai tên không thể tồn tại riêng biệt trên hệ thống tệp không phân biệt hoa/thường. Đây là giới hạn của fixture theo hệ điều hành; các test kiểm tra catalog tiếng Việt và placeholder đều đạt.
- Chạy `npm run lint`: catalog tiếng Việt không còn cảnh báo. Lint toàn dự án vẫn báo 3 lỗi `no-undef` cho `ScriptApp` trong `services/google-script/index.js` (API môi trường Google Apps Script) và 17 cảnh báo ở các tệp khác.

## Lưu ý khi sử dụng

Thiết lập `language` hiện được ứng dụng dùng cho cả ngôn ngữ giao diện lẫn locale gửi tới HoYoLAB, theo thiết kế hiện hữu. Nếu máy chủ/API HoYoLAB không hỗ trợ một locale cụ thể, điều đó có thể ảnh hưởng phản hồi API; các thông điệp phần mềm vẫn có thể dùng catalog tiếng Việt. Khi thêm chuỗi mới vào mã nguồn, cần bổ sung bản dịch vào `localization/vi.js` để giữ độ bao phủ đầy đủ.
