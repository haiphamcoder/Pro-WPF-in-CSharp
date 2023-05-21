# Chương 2: XAML

XAML (viết tắt của Extensible Application Markup Language và phát âm là zammel) là một ngôn ngữ đánh dấu được sử dụng để khởi tạo các đối tượng .NET. Mặc dù XAML là một công nghệ có thể được áp dụng cho nhiều lĩnh vực có vấn đề, vai trò chính của nó trong cuộc sống là xây dựng giao diện người dùng WPF. Nói cách khác, tài liệu XAML xác định sự sắp xếp của các bảng, nút và điều khiển tạo nên các cửa sổ trong ứng dụng WPF

Không chắc là bạn sẽ viết XAML bằng tay. Thay vào đó, bạn sẽ sử dụng một công cụ tạo ra XAML bạn cần. Nếu bạn là một nhà thiết kế đồ họa, công cụ đó có thể là một chương trình thiết kế đồ họa như Microsoft Expression Blend. Nếu bạn là nhà phát triển, có thể bạn sẽ bắt đầu với Microsoft Visual Studio. Bởi vì cả hai công cụ đều như nhau ở nhà với XAML, bạn có thể tạo giao diện người dùng cơ bản với Visual Studio và sau đó giao nó cho một nhóm thiết kế crack có thể đánh bóng nó bằng đồ họa tùy chỉnh trong Expression Blend. Trên thực tế, khả năng tích hợp quy trình làm việc giữa các nhà phát triển và nhà thiết kế là một trong những lý do chính mà Microsoft tạo ra XAML.

Chương này trình bày giới thiệu chi tiết về XAML. Bạn sẽ xem xét mục đích của nó, kiến trúc tổng thể và cú pháp của nó. Khi bạn hiểu các quy tắc rộng của XAML, bạn sẽ biết những gì có thể và không thể trong giao diện người dùng WPF và cách thực hiện thay đổi bằng tay khi cần thiết. Quan trọng hơn, bằng cách khám phá các thẻ trong tài liệu WPF XAML, bạn có thể tìm hiểu một chút về mô hình đối tượng làm nền tảng cho giao diện người dùng WPF và sẵn sàng cho việc khám phá sâu hơn sắp tới.

## Hiểu về XAML

Các nhà phát triển đã nhận ra từ lâu rằng cách hiệu quả nhất để giải quyết các ứng dụng phức tạp, giàu đồ họa là tách phần đồ họa khỏi mã cơ bản. Bằng cách đó, các nghệ sĩ có thể sở hữu đồ họa và các nhà phát triển có thể sở hữu mã. Cả hai phần có thể được thiết kế và tinh chỉnh riêng biệt, mà không phải đau đầu về phiên bản.

### Giao diện người dùng đồ họa trước WPF

Với các công nghệ hiển thị truyền thống, không có cách nào dễ dàng để tách nội dung đồ họa khỏi mã. Vấn đề chính với ứng dụng Windows Forms là mọi biểu mẫu bạn tạo đều được xác định hoàn toàn bằng mã C#. Khi bạn thả điều khiển vào bề mặt thiết kế và cấu hình chúng, Visual Studio lặng lẽ điều chỉnh mã trong lớp biểu mẫu tương ứng. Đáng buồn thay, các nhà thiết kế đồ họa không có bất kỳ công cụ nào có thể làm việc với mã C#.

Thay vào đó, các nghệ sĩ buộc phải lấy nội dung của họ và xuất nó sang định dạng bitmap. Những bitmap này sau đó có thể được sử dụng cho các cửa sổ da, nút và các điều khiển khác. Cách tiếp cận này hoạt động tốt cho các giao diện đơn giản không thay đổi nhiều theo thời gian, nhưng nó cực kỳ hạn chế trong các tình huống khác. Một số vấn đề của nó bao gồm:

- Mỗi yếu tố đồ họa (nền, nút, v.v.) cần được xuất dưới dạng bitmap riêng biệt. Điều đó hạn chế khả năng kết hợp bitmap và sử dụng các hiệu ứng động như khử răng cưa, độ trong suốt và bóng.
- Một chút logic giao diện người dùng cần được nhà phát triển nhúng vào mã. Điều này bao gồm kích thước nút, định vị, hiệu ứng di chuột và hoạt ảnh. Nhà thiết kế đồ họa không thể kiểm soát bất kỳ chi tiết nào trong số này.
- Không có kết nối nội tại giữa các yếu tố đồ họa khác nhau, vì vậy thật dễ dàng để kết thúc với một bộ hình ảnh chưa từng có. Theo dõi tất cả các mục này làm tăng thêm sự phức tạp.
- Bitmap không thể được thay đổi kích thước mà không ảnh hưởng đến chất lượng của chúng. Vì lý do đó, giao diện người dùng dựa trên bitmap phụ thuộc vào độ phân giải. Điều đó có nghĩa là nó không thể chứa màn hình lớn và độ phân giải cao , đó là một sự vi phạm lớn đối với triết lý thiết kế WPF.

Nếu bạn đã từng trải qua quá trình thiết kế ứng dụng Windows Forms với đồ họa tùy chỉnh trong cài đặt nhóm, bạn đã phải chịu đựng rất nhiều thất vọng. Ngay cả khi giao diện được thiết kế từ đầu bởi một nhà thiết kế đồ họa, bạn sẽ cần phải tạo lại nó bằng mã C#. Thông thường, nhà thiết kế đồ họa sẽ chỉ cần chuẩn bị một mô hình mà bạn cần để dịch cẩn thận vào ứng dụng của mình.

WPF giải quyết vấn đề này với XAML. Khi thiết kế ứng dụng WPF trong Visual Studio, cửa sổ bạn đang thiết kế không được dịch thành mã. Thay vào đó, nó được tuần tự hóa thành một tập hợp các thẻ XAML. Khi bạn chạy ứng dụng, các thẻ này được sử dụng để tạo các đối tượng soạn giao diện người dùng.

■ Lưu ý: Điều quan trọng là phải hiểu rằng WPF không yêu cầu XAML. Không có lý do gì Visual Studio không thể sử dụng phương pháp Windows Forms và tạo các câu lệnh mã xây dựng cửa sổ WPF của bạn. Nhưng nếu có, cửa sổ của bạn sẽ bị khóa vào môi trường Visual Studio và chỉ có sẵn cho các lập trình viên.

Nói cách khác, WPF không yêu cầu XAML. Tuy nhiên, XAML mở ra thế giới khả năng hợp tác, bởi vì các công cụ thiết kế khác hiểu định dạng XAML. Ví dụ: một nhà thiết kế hiểu biết có thể sử dụng một công cụ như Microsoft Expression Design để tinh chỉnh đồ họa trong ứng dụng WPF của bạn hoặc một công cụ như Expression Blend để xây dựng các hình ảnh động phức tạp cho nó.

■ Mẹo: XAML đóng vai trò tương tự cho các ứng dụng Windows như các thẻ điều khiển làm cho các ứng dụng web ASP.NET. Sự khác biệt là cú pháp gắn thẻ ASP.NET được thiết kế để trông giống như HTML, vì vậy các nhà thiết kế có thể tạo các trang web bằng cách sử dụng các ứng dụng thiết kế web thông thường như Microsoft Expression và Adobe Dreamweaver. Như với WPF, mã thực tế cho một trang web ASP.NET thường được đặt trong một tệp riêng biệt để tạo điều kiện thuận lợi cho thiết kế này

### Các biến thể của XAML

Mọi người sử dụng thuật ngữ XAML theo nhiều cách khác nhau. Cho đến nay, tôi đã sử dụng nó để chỉ toàn bộ ngôn ngữ của XAML, một cú pháp dựa trên XML đa năng để đại diện cho một cây các đối tượng .NET. (Các đối tượng này có thể là các nút và hộp văn bản trong cửa sổ hoặc các lớp tùy chỉnh mà bạn đã xác định. Trên thực tế, XAML thậm chí có thể được sử dụng trên các nền tảng khác để đại diện cho các đối tượng non-.NET.)

Ngoài ra còn có một số tập hợp con của XAML:

- WPF XAML bao gồm các yếu tố mô tả nội dung WPF, chẳng hạn như đồ họa vector, điều khiển và tài liệu. Hiện tại, đây là ứng dụng quan trọng nhất của XAML và đó là tập hợp con bạn sẽ khám phá trong cuốn sách này
- XPS XAML là một phần của WPF XAML xác định biểu diễn XML cho các tài liệu điện tử được định dạng. Nó đã được xuất bản dưới dạng tiêu chuẩn XML Paper Specification (XPS) riêng biệt. Bạn sẽ khám phá XPS trong Chương 28.
- Silverlight XAML là một tập hợp con của WPF XAML dành cho các ứng dụng Microsoft Silverlight. Silverlight là một trình cắm trình duyệt đa nền tảng cho phép bạn tạo nội dung web phong phú với đồ họa hai chiều, hoạt hình và âm thanh và video. Chương 1 có nhiều hơn về Silverlight, hoặc bạn có thể truy cập [https://www.microsoft.com/silverlight/](https://www.microsoft.com/silverlight/) để tìm hiểu chi tiết về nó.
- WF XAML bao gồm các yếu tố mô tả nội dung Windows Workflow Foundation (WF). Bạn có thể tìm hiểu thêm về WF tại [https://learn.microsoft.com/en-us/dotnet/framework/windows-workflow-foundation/conceptual-overview?redirectedfrom=MSDN](https://learn.microsoft.com/en-us/dotnet/framework/windows-workflow-foundation/conceptual-overview?redirectedfrom=MSDN).

### Biên soạn XAML

Những người tạo ra WPF biết rằng XAML không chỉ cần giải quyết vấn đề hợp tác thiết kế mà còn cần phải nhanh chóng. Và mặc dù các định dạng dựa trên XML như XAML rất linh hoạt và dễ dàng di chuyển sang các công cụ và nền tảng khác, nhưng chúng không phải lúc nào cũng là lựa chọn hiệu quả nhất. XML được thiết kế hợp lý, dễ đọc và đơn giản, nhưng không nhỏ gọn.

WPF giải quyết thiếu sót này với Ngôn ngữ đánh dấu ứng dụng nhị phân (BAML). BAML thực sự không gì khác hơn là một đại diện nhị phân của XAML. Khi bạn biên dịch một ứng dụng WPF trong Visual Studio, tất cả các tệp XAML của bạn được chuyển đổi thành BAML và BAML đó sau đó được nhúng dưới dạng tài nguyên vào cụm DLL hoặc EXE cuối cùng. BAML được token hóa, có nghĩa là các bit dài hơn của XAML được thay thế bằng các token ngắn hơn. BAML không chỉ nhỏ hơn đáng kể mà còn được tối ưu hóa theo cách giúp phân tích cú pháp nhanh hơn trong thời gian chạy

Hầu hết các nhà phát triển sẽ không lo lắng về việc chuyển đổi XAML sang BAML vì trình biên dịch thực hiện nó đằng sau hậu trường. Tuy nhiên, có thể sử dụng XAML mà không cần biên dịch trước. Điều này có thể có ý nghĩa trong các tình huống yêu cầu một số giao diện người dùng được cung cấp đúng lúc (ví dụ: rút ra khỏi cơ sở dữ liệu dưới dạng một khối thẻ XAML). Bạn sẽ thấy cách này hoạt động trong phần sắp tới "Tải và biên dịch XAML".

### Tạo XAML với Visual Studio

Trong chương này, bạn sẽ xem xét tất cả các chi tiết của đánh dấu XAML. Tất nhiên, khi bạn thiết kế một ứng dụng, bạn sẽ không viết tất cả XAML của mình bằng tay. Thay vào đó, bạn sẽ sử dụng một công cụ như Visual Studio có thể kéo và thả giao diện người dùng của bạn vào sự tồn tại. Dựa trên đó, bạn có thể tự hỏi liệu có đáng để dành quá nhiều thời gian nghiên cứu cú pháp của XAML hay không

Câu trả lời là có. Hiểu XAML là rất quan trọng đối với thiết kế ứng dụng WPF. Nó sẽ giúp bạn tìm hiểu các khái niệm WPF chính, chẳng hạn như các thuộc tính đính kèm (trong chương này), bố cục (Chương 3), các sự kiện được định tuyến (Chương 4), mô hình nội dung (Chương 6), v.v. Quan trọng hơn, một loạt các nhiệm vụ là có thể - hoặc dễ dàng hơn nhiều để hoàn thành - với XAML viết tay. Chúng bao gồm những điều sau đây:

Hầu hết các nhà phát triển WPF sử dụng kết hợp các kỹ thuật, đặt ra một số giao diện người dùng của họ với một công cụ thiết kế (Visual Studio hoặc Expression Blend) và sau đó tinh chỉnh nó bằng cách chỉnh sửa đánh dấu XAML bằng tay. Tuy nhiên, có thể bạn sẽ thấy rằng dễ dàng nhất để viết tất cả XAML của bạn bằng tay cho đến khi bạn tìm hiểu về các container bố cục trong Chương 3. Đó là bởi vì bạn cần sử dụng một bộ chứa bố cục để sắp xếp hợp lý nhiều điều khiển trong một cửa sổ.

## Khái niệm cơ bản về XAML

Tiêu chuẩn XAML khá đơn giản khi bạn hiểu một vài quy tắc cơ bản:

- Mỗi phần tử trong tài liệu XAML ánh xạ đến một phiên bản của lớp .NET. Tên của phần tử khớp chính xác với tên của lớp. Ví dụ, phần tử <Button hướng dẫn WPF tạo một đối tượng Button.
- Như với bất kỳ tài liệu XML nào, bạn có thể lồng một phần tử vào bên trong một phần tử khác. Như bạn sẽ thấy, XAML cung cấp cho mọi lớp sự linh hoạt để quyết định cách xử lý tình huống này. Tuy nhiên, lồng nhau thường là một cách để thể hiện sự ngăn chặn — nói cách khác, nếu bạn tìm thấy phần tử Nút bên trong phần tử Lưới, giao diện người dùng của bạn có thể bao gồm một lưới chứa một nút bên trong.
- Bạn có thể thiết lập các thuộc tính của mỗi lớp thông qua các thuộc tính. Tuy nhiên, trong một số tình huống, một thuộc tính không đủ mạnh để xử lý công việc. Trong những trường hợp này, bạn sẽ sử dụng các thẻ lồng nhau với cú pháp đặc biệt.

■ Lưu ý: Nếu bạn hoàn toàn mới với XML, có thể bạn sẽ thấy dễ dàng hơn để xem lại những điều cơ bản trước khi bạn giải quyết XAML. Để bắt kịp tốc độ nhanh chóng, hãy thử hướng dẫn dựa trên web miễn phí tại [www.w3schools.com/xml](https://www.w3schools.com/xml).

Trước khi tiếp tục, hãy xem tài liệu XAML xương trần này, đại diện cho một cửa sổ trống mới (như được tạo bởi Visual Studio). Các dòng đã được đánh số để dễ dàng tham khảo:

```xaml
<Window x:Class="WindowsApplication1.Window1"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="Window1" Height="300" Width="300">
    
    <Grid>
    </Grid>
</Window>
```
