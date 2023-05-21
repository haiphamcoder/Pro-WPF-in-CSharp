# Chương 2: XAML

XAML (viết tắt của Extensible Application Markup Language và phát âm là zammel) là một ngôn ngữ đánh dấu được sử dụng để khởi tạo các đối tượng .NET. Mặc dù XAML là một công nghệ có thể được áp dụng cho nhiều lĩnh vực có vấn đề, vai trò chính của nó trong cuộc sống là xây dựng giao diện người dùng WPF. Nói cách khác, tài liệu XAML xác định sự sắp xếp của các bảng, nút và điều khiển tạo nên các cửa sổ trong ứng dụng WPF

Không chắc là bạn sẽ viết XAML bằng tay. Thay vào đó, bạn sẽ sử dụng một công cụ tạo ra XAML bạn cần. Nếu bạn là một nhà thiết kế đồ họa, công cụ đó có thể là một chương trình thiết kế đồ họa như Microsoft Expression Blend. Nếu bạn là nhà phát triển, có thể bạn sẽ bắt đầu với Microsoft Visual Studio. Bởi vì cả hai công cụ đều như nhau ở nhà với XAML, bạn có thể tạo giao diện người dùng cơ bản với Visual Studio và sau đó giao nó cho một nhóm thiết kế crack có thể đánh bóng nó bằng đồ họa tùy chỉnh trong Expression Blend. Trên thực tế, khả năng tích hợp quy trình làm việc giữa các nhà phát triển và nhà thiết kế là một trong những lý do chính mà Microsoft tạo ra XAML.

Chương này trình bày giới thiệu chi tiết về XAML. Bạn sẽ xem xét mục đích của nó, kiến trúc tổng thể và cú pháp của nó. Khi bạn hiểu các quy tắc rộng của XAML, bạn sẽ biết những gì có thể và không thể trong giao diện người dùng WPF và cách thực hiện thay đổi bằng tay khi cần thiết. Quan trọng hơn, bằng cách khám phá các thẻ trong tài liệu WPF XAML, bạn có thể tìm hiểu một chút về mô hình đối tượng làm nền tảng cho giao diện người dùng WPF và sẵn sàng cho việc khám phá sâu hơn sắp tới.

## Hiểu về XAML

Các nhà phát triển đã nhận ra từ lâu rằng cách hiệu quả nhất để giải quyết các ứng dụng phức tạp, giàu đồ họa là tách phần đồ họa khỏi mã cơ bản. Bằng cách đó, các nghệ sĩ có thể sở hữu đồ họa và các nhà phát triển có thể sở hữu mã. Cả hai phần có thể được thiết kế và tinh chỉnh riêng biệt, mà không phải đau đầu về phiên bản.
