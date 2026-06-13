# AO3 Vietnamese Font Bookmarklet

AO3 Vietnamese Font Bookmarklet là một Bookmarklet nhỏ giúp đổi font hiển thị trên Archive of Our Own để đọc tiếng Việt dễ hơn.

Mặc định cả 2 code dùng **Cambria** vì font này có sẵn trên Windows, hỗ trợ tiếng Việt tốt, dễ đọc, và hợp với giao diện đọc truyện.

## Bookmarklet

```js
javascript:(function(){document.head.insertAdjacentHTML('beforeend','<style>*{font-family:"Cambria",sans-serif!important}</style>')})()
```

## Cách dùng

1. Nhấn `Ctrl + Shift + B` để hiện thanh Bookmark của trình duyệt.
2. Nhấp chuột phải lên thanh Bookmark, chọn `Add page...`, rồi đặt tên, ví dụ `AO3 Vietnamese Font`.
3. Dán nội dung trong `bookmarklet.txt` vào phần URL.
4. Mở một trang AO3.
5. Nhấn Bookmark đó một lần để đổi font trên trang hiện tại.

Bookmarklet chỉ áp dụng cho trang đang mở. Khi mở tab mới hoặc reload trang, cần nhấn lại.

## Đổi font

Nếu muốn dùng font khác, thay chữ `Cambria` bằng tên font bạn muốn:

```js
javascript:(function(){document.head.insertAdjacentHTML('beforeend','<style>*{font-family:"Bookerly",sans-serif!important}</style>')})()
```

Tên font phải là tên mà trình duyệt nhận trong CSS. Tên hiển thị trong Microsoft Word hoặc ứng dụng khác có thể không giống tên mà AO3/trình duyệt dùng được.

Ví dụ, Microsoft Word có thể hiển thị:

```text
Source Serif 4
```

Nhưng trình duyệt có thể nhận font đó là:

```text
Source Serif 4 14pt
```

Khi đó Bookmarklet hoặc Site Skin phải dùng đúng tên trình duyệt nhận.

Bookmarklet:

```js
javascript:(function(){document.head.insertAdjacentHTML('beforeend','<style>*{font-family:"Source Serif 4 14pt",sans-serif!important}</style>')})()
```

Site Skin:

```css
* {
  font-family: "Source Serif 4 14pt", sans-serif !important;
}
```

## Tìm đúng tên font

Trên Chrome hoặc Edge, có thể kiểm tra tên font bằng DevTools (Nếu trình duyệt hỏi quyền xem font local thì chọn Allow):

Bạn có thể lấy tên font hiển thị trong Microsoft Word làm từ khóa kiểm tra. Sau khi chạy đoạn Javascript bên dưới, hãy ưu tiên dùng giá trị `family` vào Bookmarklet hoặc Site Skin.

1. Mở một trang bất kỳ.
2. Nhấn `F12`.
3. Mở tab `Console`.
4. Chạy đoạn Javascript kiểm tra sau, thay `MSWord_Font` bằng tên font hiển thị trong Microsoft Word:

```js
const fontName = 'MSWord_Font';
const fonts = await window.queryLocalFonts();
fonts
  .filter(font => `${font.family} ${font.fullName} ${font.postscriptName}`.toLowerCase().includes(fontName.toLowerCase()))
  .map(font => ({
    family: font.family,
    fullName: font.fullName,
    postscriptName: font.postscriptName,
    style: font.style
  }));
```

Ví dụ nếu kết quả trả về:

```js
{
  family: "Source Serif 4 14pt",
  fullName: "Source Serif 4 14pt",
  postscriptName: "SourceSerif4-Regular",
  style: "14pt"
}
```

thì dùng `"Source Serif 4 14pt"` như hiển thị ở family.

Nếu vừa cài font mới, hãy khởi động lại thiết bị.

## AO3 Site Skin

Nếu muốn đổi font lâu dài mà không cần nhấn Bookmarklet mỗi lần, có thể dùng AO3 Site Skin (yêu cầu tài khoản AO3) với file `site-skin.css`:

```css
* {
  font-family: "Cambria", sans-serif !important;
}
```

Nếu dùng font khác, thay `Cambria` bằng tên font trình duyệt nhận được.

## Về font dự phòng

Bookmarklet và site-skin dùng `sans-serif` làm font dự phòng:

```css
font-family: "Cambria", sans-serif !important;
```

Nếu máy không có font đứng trước, trình duyệt sẽ dùng font không chân mặc định, thường dễ đọc hơn cho Tiếng Việt. Nếu bạn thích font có chân hoàn toàn, có thể đổi `sans-serif` thành `serif`.

## Quyền riêng tư

Bookmarklet này chỉ chèn CSS vào trang AO3 đang mở để đổi font hiển thị.
Nó không gửi dữ liệu ra ngoài, không đọc tài khoản, không lưu lịch sử đọc và không theo dõi người dùng.

## Files

- `bookmarklet.txt`: Bookmarklet một dòng.
- `site-skin.css`: CSS để dùng trong AO3 Site Skin.

## License

AO3 Vietnamese is licensed under AGPL-3.0-only. See `LICENSE` for the full license text.

Copyright (c) 2026 phairiceismyotp (or3zz - Nguyen Tin)
