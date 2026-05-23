### Câu A1:

**1. Thẻ `<meta viewport>` chuẩn và giải thích:**
<meta name="viewport" content="width=device-width, initial-scale=1.0">

+ width=device-width: Yêu cầu trình duyệt thiết lập chiều rộng không gian hiển thị (viewport) bằng đúng với chiều rộng vật lý của màn hình thiết bị.
+ initial-scale=1.0: Thiết lập mức độ phóng to/thu nhỏ ban đầu ở mức 100% (không bị thu nhỏ hay phóng to), giúp nội dung giữ đúng kích thước nguyên bản khi vừa tải trang.

2. Nếu THIẾU thẻ này, iPhone sẽ hiển thị trang web như thế nào?

+ Nếu không có thẻ viewport, trình duyệt trên điện thoại (như iPhone) sẽ mặc định giả định rằng trang web được thiết kế dành cho màn hình máy tính (thường lấy mốc chiều rộng khoảng 980px).
+ Trình duyệt sẽ cố ép toàn bộ layout rộng lớn đó vào màn hình điện thoại bằng cách thu nhỏ mọi thứ lại.
+ Kết quả là trang web sẽ có hình ảnh và chữ cực kỳ bé, bắt buộc người dùng phải dùng tay phóng to (zoom in) mới có thể đọc được nội dung.

3. Mobile-First và Desktop-First khác nhau thế nào?
+ Mobile-First (Ưu tiên di động): Viết code CSS mặc định dành cho màn hình nhỏ (Mobile) trước, sau đó dùng Media Queries với min-width để bổ sung và mở rộng layout khi kích thước màn hình tăng lên (Tablet, Desktop)

/* Code mặc định cho Mobile (Ví dụ: 1 cột) */
.grid { display: block; } 

/* Breakpoint 768px: Mở rộng layout cho Tablet/Desktop */
@media (min-width: 768px) {
    .grid { display: flex; } 
}

*   **Desktop-First (Ưu tiên máy tính):** Viết code CSS mặc định dành cho màn hình lớn (Desktop) trước, sau đó dùng Media Queries với `max-width` để ẩn bớt, bóp nhỏ layout lại khi xuống các màn hình hẹp hơn.
    ```css
    /* Code mặc định cho Desktop (Ví dụ: Nhiều cột) */
    .grid { display: flex; } 

    /* Breakpoint 768px: Thu nhỏ layout khi xuống Mobile */
    @media (max-width: 768px) {
        .grid { display: block; } 
    }
+ Tại sao Mobile-First được khuyên dùng? 
  + Hiệu năng (Performance): Các thiết bị di động thường có mạng yếu và phần cứng thấp hơn, nên với Mobile-First, điện thoại chỉ cần tải lượng CSS tối thiểu, không phải tải trước toàn bộ file CSS phức tạp của máy tính rồi lại phải xử lý ghi đè để giấu chúng đi.  
  + Trải nghiệm người dùng (UX): Phương pháp này ép buộc lập trình viên phải tập trung thiết kế các nội dung và tính năng cốt lõi nhất đưa lên màn hình hẹp trước. Khi không gian mở rộng lên Desktop, việc thêm thắt các chi tiết sẽ dễ dàng và hợp lý hơn[cite: 3].

### Câu A2:

Dưới đây là các breakpoints chuẩn theo hệ thống của Bootstrap 5 để thiết kế Responsive[cite: 3]:

| Kích thước (Pixel) | Thiết bị đại diện | Ví dụ: Lưới sản phẩm (Product Grid) |
| :--- | :--- | :--- |
| `< 576px` | Điện thoại di động (Mobile dọc) | Hiển thị 1 cột |
| `≥ 576px` (576px - 767px) | Điện thoại quay ngang (Landscape mobile) | Hiển thị 2 cột |
| `≥ 768px` (768px - 991px) | Máy tính bảng (Tablet) | Hiển thị 2 hoặc 3 cột |
| `≥ 992px` (992px - 1199px) | Laptop / Máy tính bàn cỡ nhỏ (Desktop) | Hiển thị 3 hoặc 4 cột |
| `≥ 1200px` | Màn hình PC / Desktop cỡ lớn (Large Desktop) | Hiển thị 4 cột (hoặc nhiều hơn) |

### Câu A3:

Dựa vào các điểm neo (breakpoints) sử dụng `min-width` trong đoạn mã CSS[cite: 3], dưới đây là kích thước tương ứng của `.container`:

| Chiều rộng màn hình | `.container` width |
| :--- | :--- |
| 375px (iPhone SE) | `100%` |
| 600px | `540px` |
| 800px | `720px` |
| 1000px | `960px` |
| 1400px | `1140px` |

### Câu A4:

**1. Giải thích 4 tính năng chính của SCSS và ví dụ:**[cite: 3]

*   **Variables (Biến):** Cho phép lưu trữ các giá trị thường dùng (như mã màu, font chữ, kích thước) vào một biến để tái sử dụng ở nhiều nơi[cite: 3]. Khi cần thay đổi, chỉ cần sửa giá trị của biến thì toàn bộ file sẽ tự động được cập nhật.
```scss
    $primary-color: #14b8a6;
    .button {
        background-color: $primary-color;
    }
    ```

*   **Nesting (Lồng ghép CSS):** Cho phép viết các bộ chọn (selectors) CSS lồng vào nhau theo đúng cấu trúc phân cấp của HTML[cite: 3]. Tính năng này giúp mã nguồn gọn gàng, trực quan và dễ quản lý mối quan hệ cha-con.
```scss
    nav {
        background: #333;
        ul {
            list-style: none;
        }
        li {
            display: inline-block;
        }
    }
    ```

*   **Mixins:** Cho phép đóng gói một khối mã CSS (chứa nhiều thuộc tính) để tái sử dụng nhiều lần ở các class khác nhau[cite: 3]. Mixins rất mạnh mẽ vì nó cho phép truyền tham số (arguments) vào giống như một hàm trong lập trình.
```scss
    @mixin flex-center {
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .box {
        @include flex-center;
        width: 100px;
    }
    ```

*   **@extend / Inheritance (Kế thừa):** Cho phép một class chia sẻ (kế thừa) toàn bộ tập hợp các thuộc tính CSS từ một class khác[cite: 3]. Tính năng này giúp giảm thiểu việc viết lặp lại code (đảm bảo nguyên tắc DRY - Don't Repeat Yourself).

```scss
    .btn-base {
        padding: 10px 20px;
        border-radius: 5px;
    }
    .btn-primary {
        @extend .btn-base;
        background-color: blue;
        color: white;
    }
    ```

**2. Tại sao trình duyệt KHÔNG đọc được file `.scss`?**[cite: 3]
Trình duyệt web (như Chrome, Safari, Edge) mặc định chỉ được lập trình để đọc, hiểu và render bằng ngôn ngữ CSS nguyên thủy. SCSS là một ngôn ngữ "tiền xử lý" (preprocessor), được tạo ra nhằm hỗ trợ lập trình viên viết code CSS nhanh hơn, cấu trúc tốt hơn, chứ không phải là ngôn ngữ đích dành cho trình duyệt.

**3. Cần bước gì để chuyển SCSS → CSS?**[cite: 3]
Cần phải trải qua một bước gọi là **Biên dịch (Compile)**. Các công cụ biên dịch (như extension Live Sass Compiler trong VS Code, Node Sass, Dart Sass...) sẽ đọc file `.scss` của bạn, dịch các cú pháp đặc biệt (như biến, lồng ghép, mixin) và tạo ra một file `.css` chuẩn hóa để trình duyệt có thể sử dụng.