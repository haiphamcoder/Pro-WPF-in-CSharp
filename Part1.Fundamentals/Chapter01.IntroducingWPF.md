# Chương 01: Giới thiệu WPF

Windows Presentation Foundation (WPF) là một hệ thống hiển thị đồ họa hiện đại cho Windows. Đó là một sự thay đổi căn bản so với các công nghệ đi trước, với các tính năng sáng tạo như tăng tốc phần cứng tích hợp và độc lập độ phân giải, cả hai đều bạn sẽ khám phá trong chương này.

WPF là bộ công cụ tốt nhất để sử dụng nếu bạn muốn xây dựng một ứng dụng máy tính để bàn phong phú chạy trên Windows Vista, Windows 7 và Windows 8 ở chế độ máy tính để bàn (cũng như các phiên bản tương ứng của Windows Server). Trên thực tế, đây là bộ công cụ có mục đích chung duy nhất nhắm mục tiêu đến các phiên bản Windows này. Để so sánh, bộ công cụ Metro mới của Microsoft - mặc dù thú vị - chỉ giới hạn ở các hệ thống Windows 8. (Các ứng dụng WPF thậm chí có thể được thực hiện để chạy trên các máy tính Windows XP cổ đại, vẫn được tìm thấy trong nhiều doanh nghiệp. Hạn chế duy nhất là bạn phải cấu hình Visual Studio để nhắm mục tiêu .NET 4.0 Framework cũ hơn một chút, thay vì .NET 4.5.)

Trong chương này, bạn sẽ có cái nhìn đầu tiên về kiến trúc của WPF. Bạn sẽ tìm hiểu cách nó xử lý các độ phân giải màn hình khác nhau và bạn sẽ nhận được một cuộc khảo sát cấp cao về các cụm và lớp cốt lõi của nó. Bạn cũng sẽ xem xét WPF đã phát triển như thế nào từ bản phát hành ban đầu lên phiên bản 4.5.

## Sự phát triển của đồ họa Windows

Trước WPF, các nhà phát triển Windows đã dành gần 15 năm để sử dụng công nghệ hiển thị tương tự. Đó là bởi vì mọi ứng dụng Windows truyền thống, trước WPF đều dựa vào hai phần cũ của hệ điều hành Windows để tạo giao diện người dùng của nó:

- ***User32***: Điều này cung cấp giao diện Windows truyền thống cho các yếu tố như cửa sổ, nút, hộp văn bản, v.v
- ***GDI/GDI+***: Điều này cung cấp hỗ trợ vẽ để hiển thị hình dạng, văn bản và hình ảnh với chi phí phức tạp bổ sung (và hiệu suất thường mờ nhạt).

Trong những năm qua, cả hai công nghệ đã được tinh chỉnh và các API mà các nhà phát triển sử dụng để tương tác với chúng đã thay đổi đáng kể. Nhưng cho dù bạn đang tạo một ứng dụng với .NET và Windows Forms hay thậm chí Visual Basic 6 hoặc mã C++ dựa trên MFC, đằng sau hậu trường, các phần tương tự của hệ điều hành Windows đang hoạt động. Các framework khác nhau chỉ đơn giản là cung cấp các wrappers khác nhau để tương tác với User32 và GDI/GDI+. Chúng có thể cung cấp các cải tiến về hiệu quả, giảm độ phức tạp và thêm các tính năng được nướng sẵn để bạn không phải tự viết mã; Nhưng họ không thể loại bỏ những hạn chế cơ bản của một thành phần hệ thống được thiết kế hơn một thập kỷ trước.

■ Lưu ý: Sự phân công lao động cơ bản giữa User32 và GDI/GDI+ đã được giới thiệu hơn 15 năm trước và được thiết lập tốt trong Windows 3.0. Tất nhiên, User32 chỉ đơn giản là User vào thời điểm đó, bởi vì phần mềm chưa bước vào thế giới 32-bit.

### DirectX: Công cụ đồ họa mới

Microsoft đã tạo ra một cách xung quanh những hạn chế của thư viện User32 và GDI/GDI+: DirectX. DirectX bắt đầu như một bộ công cụ dễ bị lỗi để tạo trò chơi trên nền tảng Windows. Nhiệm vụ thiết kế của nó là tốc độ, và vì vậy Microsoft đã hợp tác chặt chẽ với các nhà cung cấp card màn hình để cung cấp cho DirectX khả năng tăng tốc phần cứng cần thiết cho các kết cấu phức tạp, các hiệu ứng đặc biệt như độ trong suốt một phần và đồ họa ba chiều.

Trong những năm kể từ khi được giới thiệu lần đầu tiên (ngay sau Windows 95), DirectX đã trưởng thành. Bây giờ nó là một phần không thể thiếu của Windows, với sự hỗ trợ cho tất cả các card màn hình hiện đại. Tuy nhiên, API lập trình cho DirectX vẫn phản ánh nguồn gốc của nó như một bộ công cụ của nhà phát triển trò chơi. Do sự phức tạp thô của nó, DirectX hầu như không bao giờ được sử dụng trong các loại ứng dụng Windows truyền thống (chẳng hạn như phần mềm doanh nghiệp).

WPF thay đổi tất cả điều này. Trong WPF, công nghệ đồ họa cơ bản không phải là GDI / GDI +. Thay vào đó, đó là DirectX. Trên thực tế, các ứng dụng WPF sử dụng DirectX bất kể bạn tạo loại giao diện người dùng nào. Điều đó có nghĩa là cho dù bạn đang thiết kế đồ họa ba chiều phức tạp (sở trường của DirectX) hay chỉ vẽ các nút và văn bản thuần túy, tất cả các công việc vẽ đều đi qua đường ống DirectX. Do đó, ngay cả những ứng dụng kinh doanh trần tục nhất cũng có thể sử dụng các hiệu ứng phong phú như làm mờ và khử răng cưa. Bạn cũng được hưởng lợi từ việc tăng tốc phần cứng, điều đó đơn giản có nghĩa là DirectX giao càng nhiều công việc càng tốt cho bộ xử lý đồ họa (GPU), là bộ xử lý chuyên dụng trên card màn hình.

■ Lưu ý: DirectX hiệu quả hơn vì nó hiểu các thành phần cấp cao hơn như kết cấu và độ dốc có thể được hiển thị trực tiếp bởi card màn hình. GDI / GDI + thì không, vì vậy nó cần chuyển đổi chúng thành các hướng dẫn từng pixel, được hiển thị chậm hơn nhiều bởi các thẻ video hiện đại.

Một thành phần vẫn còn trong hình ảnh (ở một mức độ hạn chế) là User32. Đó là bởi vì WPF vẫn dựa vào User32 cho một số dịch vụ nhất định, chẳng hạn như xử lý và định tuyến đầu vào và sắp xếp ứng dụng nào sở hữu phần bất động sản màn hình nào. Tuy nhiên, tất cả các bản vẽ được chuyển qua DirectX.

### Tăng tốc phần cứng và WPF

Thẻ video khác nhau trong việc hỗ trợ các tính năng kết xuất và tối ưu hóa chuyên dụng. May mắn thay, đây không phải là vấn đề, vì hai lý do. Đầu tiên, hầu hết các máy tính hiện đại đều có phần cứng video đủ mạnh cho các tính năng WPF như vẽ 3D và hoạt hình. Điều này đúng ngay cả với máy tính xách tay và máy tính để bàn có đồ họa tích hợp (bộ xử lý đồ họa được tích hợp vào bo mạch chủ, thay vì trên một thẻ riêng). Thứ hai, WPF có một dự phòng phần mềm cho mọi thứ nó làm. Điều đó có nghĩa là WPF đủ thông minh để sử dụng tối ưu hóa phần cứng nếu có thể, nhưng có thể thực hiện công việc tương tự bằng cách sử dụng các tính toán phần mềm nếu cần thiết. Vì vậy, nếu bạn chạy một ứng dụng WPF trên máy tính có card màn hình cũ, giao diện sẽ vẫn xuất hiện theo cách bạn thiết kế nó. Tất nhiên, phần mềm thay thế có thể chậm hơn nhiều, vì vậy bạn sẽ thấy rằng các máy tính có card màn hình cũ hơn sẽ không chạy tốt các ứng dụng WPF phong phú, đặc biệt là những ứng dụng kết hợp hoạt ảnh phức tạp hoặc các hiệu ứng đồ họa mạnh khác.

## WPF: Một API cao cấp

## Độc lập độ phân giải

### Đơn vị WPF

### DPI hệ thống

### Bitmap và đồ họa vector

## Kiến trúc của WPF

### Hệ thống phân cấp lớp
