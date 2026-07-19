---
title: Tổng quan về Bug và Debug trong lập trình
slug: tong-quan-ve-bug-va-debug-trong-lap-trinh
date: 2023-09-01
author: Phat
tags:
  - debugging
---

Trong bài viết này, mình chia sẻ một cách tổng quan về bug và debug trong lập trình. Khi đi làm, debug là một phần rất quan trọng. Bởi vì phần mềm nào cũng có bug cả, phần mềm càng lớn thì càng dễ có bug. Và khi có bug có nghĩa là phần mềm có lỗi xảy ra ngoài ý muốn. Khách hàng thường rất khó chịu với bug và muốn fix ngay lập tức. Cho nên, kỹ năng debug hiệu quả là một kỹ năng rất quan trọng và thường xuyên được sử dụng.

## Định nghĩa

**Bug** dùng để ám chỉ các lỗi (error) xảy ra trong các chương trình. Các lỗi này làm cho chương trình không thể hoạt động hoặc hoạt động không đúng.

**Các loại bug thường gặp** là:

- **Lỗi cú pháp** (Syntax error hay Compile error): Các ngôn ngữ lập trình có cú pháp riêng. Nếu dùng sai cú pháp, code sẽ không thể chuyển thành mã máy để thực thi. Lỗi này xảy ra trước khi chương trình chạy, và dễ xử lý. Các IDE (intergated development environment) hiện nay đều có chức năng phát hiện lỗi cú pháp và gợi ý sửa lỗi.
- **Lỗi logic** (Logic error): Lỗi này xảy ra khi các đoạn code bị sai logic. Ví dụ như khi có một vòng lặp vô tận trong code, chương trình sẽ bị ảnh hưởng nghiêm trọng.
- **Lỗi triển khai** (Deploy error): Lỗi này xảy ra khi thiếu các cấu hình cần thiết để chương trình có thể triển khai hoặc thực thi.

**Debug** là quá trình tìm ra nguyên nhân và sửa lỗi (fix bug hay remove bug) để đảm bảo chương trình hoạt động bình thường.

## Một số cách debug

**Printlining**: Chèn các dòng code để in ra các thông tin cần thiết về trạng thái của chương trình ra màn hình console. Mục đích là để quan sát trạng thái của chương trình, ví dụ như là các giá trị của biến, các kết quả của phép tính,… Từ đó, so sánh xem các kết quả có đúng như mong muốn hay không. Lưu ý là sau khi debug xong, chúng ta phải xóa các dòng đã code đã chèn vào. Nếu quên xóa thì các dòng code này sẽ ảnh hưởng đến performance của chương trình.

**Logging**: Là một công cụ ghi lại các thông tin quan trọng trong quá trình chương trình chạy. Logging không chỉ được sử dụng để debug mà dùng như một công cụ để tracking hoạt động của cả chương trình. Khi chương trình xảy ra lỗi, logging có thể ghi lại cụ thể thể dòng code nào gây ra lỗi. Chúng ta cũng có thể chèn thêm các dòng lệnh để logging để in ra các thông tin mà chúng ta muốn giống như printlining.

**Debugging Tool:** Các debugging tool thường được tích hợp vào các IDE, ví dụ như là Eclipse, IntelliJ,… Cho phép chúng ta quan sát trạng thái chương trình theo từng dòng code. Chúng ta có thể thấy được sự thay đổi giá trị của các biến, kết quả của các phép tính,… Từ đó, chúng ta có thể so sánh kết quả thực tế và kết quả mong muốn để nhận ra dòng nào đang bị lỗi, logic nào đang sai.

## Quy trình debug cơ bản

**Bước 1. Xác định được chức năng hoặc phần xử lý có bug.** Thường thì bước này sẽ do tester hoặc end-user báo cáo (report bug). Vì trong quá trình họ test hoặc sử dụng, ở một số trường hợp cụ thể nào đó, chương trình xảy ra lỗi. Các báo cáo bug thường sẽ liệt kê cụ thể chức năng bị lỗi, các bước mà người dùng đã thực hiện, người dùng đã nhập những gì, kết quả mong muốn và kết quả thực tế.

**Bước 2. Tái hiện bug (reproduce).** Mục đích của bước này là tái hiện lại lỗi trên môi trường development dựa vào các mô tả trong bug report. Cần lưu ý là lỗi có thể xảy ra do có sự khác biệt về môi trường sử dụng. Bởi vì tester sẽ test ở môi trường test, end-user sẽ sử dụng ở môi trường production. Chỉ khi các dev tái hiện được bug thì mới có thể thực hiện bước tiếp theo.

**Bước 3. Tìm và xử lý bug (debug).** Mục đích của bước này là tìm ra nguyên nhân xảy ra bug và sửa lại. Quá trình debug bao gồm một số bước cơ bản như sau:

- **Định vị bug:** Một chức năng có thể được thực thi bởi nhiều dòng code. Mục đích của bước này là xác định phần code cụ thể nào có khả năng xảy ra lỗi. Giới hạn được phạm vi càng nhỏ càng tốt. Từ đó, chúng ta tập trung vào quan sát và phân tích nó. **Logging** là một công cụ tốt để định vị bug. Khi có bug xảy ra, **bước đầu tiên thường là xem log** để biết lỗi xảy ra ở đâu. Nhiều trường hợp lỗi được ghi cụ thể vào log file, chúng ta dễ dàng xác định vị trí xảy ra bug.
- **Sử dụng debug tool để quan sát quá trình chạy code:** Hầu hết các IDE đều có chức năng debuging, chức năng này cho phép chúng ta quan sát trạng thái chương trình theo từng dòng code. Sau khi chúng ta xác định được phần code có khả năng lỗi, chúng ta đặt breakpoint vào đầu đoạn code. Sau đó, chạy debug mode để quan sát và phân tích đoạn code đó. Mục đích của bước này là quan sát và phân tích để xác định nguyên nhân xảy ra lỗi.
- **Sửa lỗi (fix bug):** Sau khi tìm được nguyên nhân, chúng ta cần phải xác định các giải pháp để sửa. Có thể có nhiều cách để sửa lỗi và chúng ta cần phải chọn cách phù hợp. Lưu ý là đoạn code chúng ta sửa có thể đang được sử dụng ở các chức năng khác. Cho nên sau khi fix bug, chúng ta cần phải kiểm tra lại.

**Bước 4. Kiểm thử lại (testing).** Sau khi sửa lỗi, phải đảm bảo chương trình hoạt động bình thường. Thứ nhất là bug không còn nữa. Thứ hai là đảm bảo các chức năng liên quan không bị ảnh hưởng. Vì khi fix bug, phần code bị sửa có thể được dùng ở các chức năng khác.

**Ví dụ quá trình debug:**

Ví dụ như, ở chức năng đăng nhập, sau khi người dùng nhập đúng username và password, người dùng nhấn nút Đăng nhập thì được chuyển sang trang chủ. Nhưng người dùng đã nhập đúng username và password nhưng hệ thống không cho chuyển sang trang chủ. Vậy là bug. Người dùng báo về cho dev. Dev khoanh vùng là chức năng đăng nhập có vấn đề. Đầu tiên, các dev sẽ reproduce lại bug trên môi trường dev. Sau khi tái hiện được bug, các dev thường vào file log xem chương trình có hoạt động bình thường không. Trong log file thì thấy có một dòng thông tin là username hoặc password không đúng. Như vậy, rất có thể là đoạn code kiểm tra username và password có vấn đề. Sau khi vào đọc lại code thì chưa thấy vấn đề gì. Cần phải bật chế độ debug lên xem kỹ quá trình chương trình chạy. Khi chạy thì thấy, username lấy từ database lên khác so với username người dùng nhập vào. Khác ở chỗ username từ database có thêm kí tự khoảng trắng ở cuối. Vậy là code phần login ok nhưng code phần signup có vấn đề. Qua bên đó check lại thì thấy là lúc người dùng tạo tài khoản, không có check phần khoảng trắng ở username và lúc lưu xuống database thì cũng không có phần xóa khoảng trắng thừa ở đầu và cuối. Như vậy, solution khả thi là ở phần frontend là thêm phần check để không cho người dùng nhập khoảng trắng trong username, có thông báo để người dùng biết. Ở phần backend thì check username, nếu có khoảng trắng thì quăng ra lỗi, nếu không thì lưu xuống database. Đưa solution cho leader và khách hàng xem. Nếu họ say ok thì mình triển khai. Sau đó, phải testing lại cả hai chức năng đăng nhập và đăng kí, đảm bảo mọi thứ hoạt động ok. (Ví dụ chỉ mang tính minh họa)

Hết.
