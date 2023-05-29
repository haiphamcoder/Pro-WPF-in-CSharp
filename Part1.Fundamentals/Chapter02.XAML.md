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
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="Window1" Height="300" Width="300">
    
    <Grid>
    </Grid>
</Window>
```

Tài liệu này chỉ bao gồm hai yếu tố—phần tử Window cấp cao nhất, đại diện cho toàn bộ cửa sổ và Grid, trong đó bạn có thể đặt tất cả các điều khiển của mình. Mặc dù bạn có thể sử dụng bất kỳ phần tử cấp cao nào, các ứng dụng WPF chỉ dựa vào một vài:

- Window
- Page (tương tự như Window nhưng được sử dụng cho các ứng dụng có thể điều hướng)
- Application (xác định tài nguyên ứng dụng và cài đặt khởi động)

Như trong tất cả các tài liệu XML, chỉ có thể có một phần tử cấp cao nhất. Trong ví dụ trước, điều đó có nghĩa là ngay sau khi bạn đóng phần tử Window bằng thẻ, bạn sẽ kết thúc tài liệu. Không còn nội dung nào có thể theo dõi

Nhìn vào thẻ mở cho phần tử Window, bạn sẽ tìm thấy một số thuộc tính thú vị, bao gồm tên lớp và hai không gian tên XML (được mô tả trong các phần sau). Bạn cũng sẽ tìm thấy ba thuộc tính được hiển thị ở đây:

```xaml
    Title="Window1" Height="300" Width="300">
```

Mỗi thuộc tính tương ứng với một thuộc tính riêng biệt của lớp Window. Nói chung, điều này cho WPF tạo một cửa sổ với tiêu đề Window1 và làm cho nó lớn 300x300 đơn vị.

■ Lưu ý: Như bạn đã học trong Chương 1, WPF sử dụng một hệ thống đo lường tương đối không phải là điều mà hầu hết các nhà phát triển Windows mong đợi. Thay vì cho phép bạn đặt kích thước bằng pixel vật lý, WPF sử dụng các đơn vị độc lập với thiết bị có thể chia tỷ lệ để phù hợp với các độ phân giải màn hình khác nhau và được định nghĩa là 1/96 inch. Điều đó có nghĩa là cửa sổ 300 x 300 đơn vị trong ví dụ trước sẽ được hiển thị dưới dạng cửa sổ 300 x 300 pixel nếu cài đặt DPI hệ thống của bạn là 96 dpi tiêu chuẩn. Tuy nhiên, trên một hệ thống có DPI hệ thống cao hơn, nhiều pixel hơn sẽ được sử dụng. Chương 1 có toàn bộ câu chuyện.

### Không gian tên XAML

Rõ ràng, nó không đủ để chỉ cung cấp một tên lớp. Bộ phân tích cú pháp XAML cũng cần biết không gian tên .NET nơi đặt lớp này. Ví dụ: lớp Window có thể tồn tại ở một số nơi—nó có thể tham chiếu đến lớp System.Windows.Window hoặc nó có thể tham chiếu đến lớp Window trong thành phần của bên thứ ba hoặc lớp bạn đã xác định trong ứng dụng của mình. Để tìm ra lớp nào bạn thực sự muốn, trình phân tích cú pháp XAML kiểm tra không gian tên XML được áp dụng cho phần tử.

Đây là cách nó hoạt động. Trong tài liệu mẫu được hiển thị trước đó, hai không gian tên được xác định:

```xaml
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
```

■ Lưu ý: Không gian tên XML được khai báo bằng cách sử dụng các thuộc tính. Các thuộc tính này có thể được đặt bên trong bất kỳ thẻ bắt đầu phần tử nào. Tuy nhiên, quy ước quy định rằng tất cả các không gian tên bạn cần sử dụng trong tài liệu phải được khai báo trong thẻ đầu tiên, như trong ví dụ này. Sau khi khai báo không gian tên, nó có thể được sử dụng ở bất kỳ đâu trong tài liệu.

Thuộc tính xmlns là một thuộc tính chuyên biệt trong thế giới XML được dành riêng để khai báo không gian tên. Đoạn mã đánh dấu này khai báo hai không gian tên mà bạn sẽ tìm thấy trong mọi tài liệu WPF XAML mà bạn tạo:

- http\://schemas.microsoft.com/winfx/2006/xaml/presentation là không gian tên WPF cốt lõi. Nó bao gồm tất cả các lớp WPF, bao gồm các điều khiển bạn sử dụng để xây dựng giao diện người dùng. Trong ví dụ này, không gian tên này được khai báo mà không có tiền tố vùng chứa tên, vì vậy nó trở thành không gian tên mặc định cho toàn bộ tài liệu. Nói cách khác, mọi phần tử được tự động đặt trong không gian tên này trừ khi bạn chỉ định khác.
- http\://schemas.microsoft.com/winfx/2006/xaml là không gian tên XAML. Nó bao gồm các tính năng tiện ích XAML khác nhau cho phép bạn ảnh hưởng đến cách diễn giải tài liệu của bạn. Không gian tên này được ánh xạ tới tiền tố x. Điều đó có nghĩa là bạn có thể áp dụng nó bằng cách đặt tiền tố không gian tên trước tên phần tử (như trong <x:ElementName>).

Như bạn có thể thấy, tên không gian tên XML không khớp với bất kỳ không gian tên .NET cụ thể nào. Có một vài lý do khiến những người tạo ra XAML chọn thiết kế này. Theo quy ước, không gian tên XML thường là mã định danh tài nguyên thống nhất (URI) như ở đây. Các URI này trông giống như chúng trỏ đến một vị trí trên Web, nhưng chúng không trỏ đến. Định dạng URI được sử dụng vì nó làm cho các tổ chức khác nhau không thể vô tình tạo ra các ngôn ngữ dựa trên XML khác nhau với cùng một không gian tên. Vì schemas.microsoft.com tên miền thuộc sở hữu của Microsoft, chỉ Microsoft mới sử dụng nó trong tên không gian tên XML

Lý do khác mà không có ánh xạ một-một giữa các không gian tên XML được sử dụng trong không gian tên XAML và .NET là vì nó sẽ làm phức tạp đáng kể các tài liệu XAML của bạn. Vấn đề ở đây là WPF bao gồm hơn một chục không gian tên (tất cả đều bắt đầu bằng System.Windows). Nếu mỗi không gian tên .NET có một không gian tên XML khác nhau, bạn cần chỉ định không gian tên phù hợp cho mỗi và mọi điều khiển bạn sử dụng, điều này nhanh chóng trở nên lộn xộn. Thay vào đó, những người tạo ra WPF đã chọn kết hợp tất cả các không gian tên .NET này thành một không gian tên XML duy nhất. Điều này hoạt động vì trong các không gian tên .NET khác nhau là một phần của WPF, không có bất kỳ lớp nào có cùng tên.

Thông tin không gian tên cho phép bộ phân tích cú pháp XAML tìm đúng lớp. Ví dụ: khi nó nhìn vào các phần tử Window và Grid, nó thấy rằng chúng được đặt trong không gian tên WPF mặc định. Sau đó, nó tìm kiếm các không gian tên .NET tương ứng cho đến khi tìm thấy System.Windows.Window và System. Windows.Controls.Grid.

### Lớp Code-Behind

XAML cho phép bạn xây dựng giao diện người dùng, nhưng để tạo một ứng dụng hoạt động, bạn cần một cách để kết nối các trình xử lý sự kiện có chứa mã ứng dụng của bạn. XAML làm cho điều này dễ dàng bằng cách sử dụng thuộc tính Class được hiển thị ở đây:

```xaml
<Window x:Class="WindowsApplication1.Window1"
```

Tiền tố không gian tên x đặt thuộc tính Class trong không gian tên XAML, có nghĩa đây là một phần tổng quát hơn của ngôn ngữ XAML. Trên thực tế, thuộc tính Class yêu cầu trình phân tích cú pháp XAML tạo một lớp mới với tên được chỉ định. Lớp đó xuất phát từ lớp được đặt tên bởi phần tử XML. Nói cách khác, ví dụ này tạo ra một lớp mới có tên là Window1, bắt nguồn từ lớp Window cơ sở

Lớp Window1 được tạo tự động tại thời điểm biên dịch. Nhưng đây là nơi mọi thứ trở nên thú vị. Bạn có thể cung cấp một phần của lớp Window1 sẽ được hợp nhất vào phần được tạo tự động. Phần bạn chỉ định là vùng chứa hoàn hảo cho mã xử lý sự kiện của bạn.

■ Lưu ý: Điều kỳ diệu này xảy ra thông qua tính năng C# được gọi là các lớp một phần. Các lớp một phần cho phép bạn chia một lớp thành hai hoặc nhiều phần riêng biệt để phát triển và hợp nhất chúng lại với nhau trong cụm được biên dịch. Các lớp một phần có thể được sử dụng trong nhiều kịch bản quản lý mã khác nhau, nhưng chúng hữu ích nhất trong các tình huống như thế này, nơi mã của bạn cần được hợp nhất với tệp do nhà thiết kế tạo.

Visual Studio giúp bạn bằng cách tự động tạo một lớp một phần nơi bạn có thể đặt mã xử lý sự kiện của mình. Ví dụ: nếu bạn tạo một ứng dụng có tên WindowsApplication1, chứa một cửa sổ có tên Window1 (như trong ví dụ trước), Visual Studio sẽ bắt đầu với bộ xương cơ bản này của một lớp:

```csharp
namespace WindowsApplication1
{
    /// <summary>
    /// Interaction logic for Window1.xaml
    /// </summary>
    public partial class Window1 : Window
    {
        public Window1()
        {
            InitializeComponent();
        }
    }
}
```

Khi bạn biên dịch ứng dụng của mình, XAML xác định giao diện người dùng của bạn (chẳng hạn như Window1. xaml) được dịch thành khai báo kiểu CLR (common language runtime) được hợp nhất với logic trong tệp lớp code-behind của bạn (chẳng hạn như Window1.xaml.cs) để tạo thành một đơn vị duy nhất.

### Phương thức InitializeComponent()

Hiện tại, mã lớp Window1 không bao gồm bất kỳ chức năng thực sự nào. Tuy nhiên, nó bao gồm một chi tiết quan trọng—hàm tạo mặc định, gọi InitializeComponent khi bạn tạo một thể hiện của lớp

■ Lưu ý: InitializeComponentmethod đóng một vai trò quan trọng trong các ứng dụng WPF. Do đó, bạn không bao giờ nên xóa lệnh gọi InitializeComponent() trong hàm tạo của cửa sổ. Tương tự, nếu bạn thêm một hàm tạo khác vào lớp cửa sổ của mình, hãy đảm bảo rằng nó cũng gọi InitializeComponent()

Phương thức InitializeComponent() không hiển thị trong mã nguồn của bạn vì nó được tạo tự động khi bạn biên dịch ứng dụng của mình. Về cơ bản, tất cả những gì InitializeComponent() làm là gọi phương thức LoadComponent của lớp System.Windows.Application. Phương thức LoadComponent() trích xuất BAML (XAML đã biên dịch) từ assembly của bạn và sử dụng nó để xây dựng giao diện người dùng của bạn. Khi nó phân tích cú pháp BAML, nó tạo ra từng đối tượng điều khiển, đặt các thuộc tính của nó và đính kèm bất kỳ trình xử lý sự kiện nào

■ Lưu ý: Nếu bạn không thể chịu được sự hồi hộp, hãy nhảy về phía trước đến cuối chương. Bạn sẽ thấy code cho phương thức InitializeComponent() được tạo tự động trong phần "Code and Compiled XAML".

### Các yếu tố đặt tên

Có một chi tiết nữa cần xem xét. Trong lớp code-behind của bạn, bạn sẽ thường muốn thao tác với các điều khiển theo chương trình. Ví dụ: bạn có thể muốn đọc hoặc thay đổi thuộc tính hoặc đính kèm và tách các trình xử lý sự kiện một cách nhanh chóng. Để thực hiện điều này, tùy chọn kiểm soát phải bao gồm thuộc tính Tên XAML. Trong ví dụ trước, điều khiển Grid không bao gồm thuộc tính Tên, vì vậy bạn sẽ không thể thao tác nó trong tệp mã phía sau của mình.

Dưới đây là cách bạn có thể đính kèm tên vào Grid:

```xaml
<Grid x:Name="grid1">
</Grid>
```

Bạn có thể thực hiện thay đổi này bằng tay trong tài liệu XAML hoặc bạn có thể chọn lưới trong trình thiết kế Visual Studio và đặt thuộc tính Tên bằng cách sử dụng cửa sổ Thuộc tính.

Dù bằng cách nào, thuộc tính Name yêu cầu bộ phân tích cú pháp XAML thêm một trường như thế này vào phần được tạo tự động của lớp Window1:

```csharp
private System.Windows.Controls.Grid grid1;
```

Bây giờ bạn có thể tương tác với lưới trong mã lớp Window1 của bạn bằng cách sử dụng tên grid1:

```csharp
MessageBox.Show(String.Format("The grid is {0}x{1} units in size.", grid1.ActualWidth, grid1.ActualHeight));
```

Kỹ thuật này không bổ sung nhiều cho ví dụ lưới đơn giản, nhưng nó trở nên quan trọng hơn nhiều khi bạn cần đọc các giá trị trong các điều khiển đầu vào như hộp văn bản và hộp danh sách.

Thuộc tính Name được hiển thị trước đó là một phần của ngôn ngữ XAML và nó được sử dụng để giúp tích hợp lớp code-behind của bạn. Hơi khó hiểu, nhiều lớp định nghĩa thuộc tính Name của riêng chúng. (Một ví dụ là lớp FrameworkElement cơ sở mà từ đó tất cả các phần tử WPF bắt nguồn.) Trình phân tích cú pháp XAML có một cách thông minh để xử lý vấn đề này. Bạn có thể đặt thuộc tính XAML Name (sử dụng tiền tố x) hoặc thuộc tính Name thuộc về phần tử thực tế (bằng cách bỏ tiền tố). Dù bằng cách nào, kết quả đều giống nhau — tên bạn chỉ định được sử dụng trong tệp mã được tạo tự động và nó được sử dụng để đặt thuộc tính Name.

Điều đó có nghĩa là đánh dấu sau đây tương đương với những gì bạn đã thấy:

```xaml
<Grid Name="grid1">
</Grid>
```

Chút phép thuật này chỉ hoạt động nếu lớp bao gồm thuộc tính Name tự trang trí bằng thuộc tính RuntimeNameProperty. RuntimeNameProperty cho biết thuộc tính nào sẽ được coi là tên cho các phiên bản thuộc loại đó. (Rõ ràng, đó thường là tài sản được đặt tên là Name.) Lớp FrameworkElement bao gồm thuộc tính RuntimeNameProperty, vì vậy không có vấn đề gì

■ Mẹo: Trong một ứng dụng Windows Forms kiểu cũ, mọi điều khiển đều có tên. Trong một ứng dụng WPF, không có yêu cầu như vậy. Các ví dụ trong cuốn sách này thường bỏ qua tên phần tử khi chúng không cần thiết, điều này làm cho đánh dấu ngắn gọn hơn.

Bây giờ, bạn sẽ có hiểu biết cơ bản về cách diễn giải tài liệu XAML xác định cửa sổ và cách tài liệu XAML đó được chuyển đổi thành lớp được biên dịch cuối cùng (với việc bổ sung bất kỳ mã nào bạn đã viết). Trong phần tiếp theo, bạn sẽ xem xét cú pháp thuộc tính chi tiết hơn và tìm hiểu cách kết nối các trình xử lý sự kiện.

## Thuộc tính và sự kiện trong XAML

Cho đến nay, bạn đã xem xét một ví dụ tương đối không thú vị — một cửa sổ trống lưu trữ điều khiển Lưới trống. Trước khi đi xa hơn, bạn nên giới thiệu một cửa sổ thực tế hơn bao gồm một số điều khiển. Hình 2-1 cho thấy một ví dụ với người trả lời câu hỏi tự động.

![Figure2-1](Figure2-1.png)

Figure 2-1. Ask the eight ball, and all will be revealed

Cửa sổ tám bóng bao gồm bốn điều khiển: Grid (công cụ phổ biến nhất để sắp xếp bố cục trong WPF), hai đối tượng TextBox và một Button. Đánh dấu cần thiết để sắp xếp và định cấu hình các điều khiển này dài hơn đáng kể so với các ví dụ trước. Dưới đây là danh sách viết tắt thay thế một số chi tiết bằng dấu chấm lửng (...) để hiển thị cấu trúc tổng thể:

```xaml
<Window x:Class="EightBall.Window1"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="Eight Ball Answer" Height="328" Width="412">
    <Grid Name="grid1">
        <Grid.Background>
            ... 
        </Grid.Background>
        <Grid.RowDefinitions>
            ...
        </Grid.RowDefinitions>
        <TextBox Name="txtQuestion" ... >
            ...
        </TextBox>
        <Button Name="cmdAnswer" ... >
            ...
        </Button>
        <TextBox Name="txtAnswer" ... >
            ...
        </TextBox>
    </Grid>
</Window>
```

Trong các phần sau, bạn sẽ khám phá các phần của tài liệu này — và tìm hiểu cú pháp của XAML trên đường đi

■ Lưu ý: XAML không giới hạn các lớp là một phần của WPF. Bạn có thể sử dụng XAML để tạo một thể hiện của bất kỳ lớp nào đáp ứng một vài quy tắc cơ bản. Bạn sẽ học cách sử dụng các lớp của riêng mình với XAML ở phần sau của chương này.

### Thuộc tính đơn giản và bộ chuyển đổi loại

Như bạn đã thấy, các thuộc tính của một phần tử đặt các thuộc tính của đối tượng tương ứng. Ví dụ: các hộp văn bản trong ví dụ tám bóng cấu hình căn chỉnh, lề và phông chữ:

```xaml
<TextBox Name="txtQuestion" VerticalAlignment="Stretch" HorizontalAlignment="Stretch" FontFamily="Verdana" FontSize="24" Foreground="Green" ... >
```

Để điều này hoạt động, lớp System.Windows.Controls.TextBox phải cung cấp các thuộc tính sau: VerticalAlignment, HorizontalAlignment, FontFamily, FontSize và Foreground. Bạn sẽ tìm hiểu ý nghĩa cụ thể cho từng thuộc tính này trong các chương sau.

Để hỗ trợ hệ thống này, trình phân tích cú pháp XAML cần thực hiện nhiều công việc hơn một chút so với những gì bạn có thể nhận ra ban đầu. Giá trị trong thuộc tính XML luôn là một chuỗi văn bản thuần túy. Tuy nhiên, thuộc tính đối tượng có thể là bất kỳ loại .Net nào.  Trong ví dụ trước, có hai thuộc tính sử dụng liệt kê (VerticalAlignment và HorizontalAlignment), một chuỗi (FontFamily), một số nguyên (FontSize) và một đối tượng Brush (Foreground).

Để thu hẹp khoảng cách giữa các giá trị chuỗi và thuộc tính không chuỗi, trình phân tích cú pháp XAML cần thực hiện chuyển đổi. Việc chuyển đổi được thực hiện bởi các trình chuyển đổi loại, một phần cơ bản của cơ sở hạ tầng .NET đã tồn tại từ .NET 1.0.

Về cơ bản, một bộ chuyển đổi kiểu có một vai trò trong cuộc sống — nó cung cấp các phương thức tiện ích có thể chuyển đổi một kiểu dữ liệu .NET cụ thể sang và từ bất kỳ loại .NET nào khác, chẳng hạn như biểu diễn chuỗi trong trường hợp này. Bộ phân tích cú pháp XAML sau hai bước để tìm bộ chuyển đổi kiểu:

1. Nó kiểm tra khai báo thuộc tính, tìm kiếm một thuộc tính TypeConverter. (Nếu có, thuộc tính TypeConverter cho biết lớp nào có thể thực hiện chuyển đổi.) Ví dụ: khi bạn sử dụng một thuộc tính như Foreground, .NET sẽ kiểm tra khai báo của thuộc tính Foreground.
2. Nếu không có thuộc tính TypeConverter trên khai báo thuộc tính, trình phân tích cú pháp XAML sẽ kiểm tra khai báo lớp của kiểu dữ liệu tương ứng. Ví dụ, thuộc tính Foreground sử dụng một đối tượng Brush. Lớp Brush (và các dẫn xuất của nó) sử dụng BrushConverter vì lớp Brush được trang trí bằng thuộc tính TypeConverter(typeof(BrushConverter)) declaration.converters

Nếu không có bộ chuyển đổi kiểu liên kết trên khai báo thuộc tính hoặc khai báo lớp, trình phân tích cú pháp XAML sẽ tạo ra lỗi

Hệ thống này đơn giản nhưng linh hoạt. Nếu bạn đặt bộ chuyển đổi kiểu ở cấp lớp, bộ chuyển đổi đó sẽ áp dụng cho mọi thuộc tính sử dụng lớp đó. Mặt khác, nếu bạn muốn tinh chỉnh cách thức hoạt động của chuyển đổi kiểu cho một thuộc tính cụ thể, bạn có thể sử dụng thuộc tính TypeConverter trên khai báo thuộc tính để thay thế.

Về mặt kỹ thuật, có thể sử dụng bộ chuyển đổi kiểu trong mã, nhưng cú pháp hơi phức tạp. Hầu như luôn luôn tốt hơn để thiết lập một thuộc tính trực tiếp — nó không chỉ nhanh hơn mà còn tránh các lỗi tiềm ẩn do gõ sai chuỗi, sẽ không bị bắt cho đến thời gian chạy. (Sự cố này không ảnh hưởng đến XAML, vì XAML được phân tích cú pháp và xác nhận tại thời điểm biên dịch.) Tất nhiên, trước khi bạn có thể thiết lập các thuộc tính trên một phần tử WPF, bạn cần biết thêm một chút về các thuộc tính và kiểu dữ liệu WPF cơ bản — một công việc bạn sẽ giải quyết trong vài chương tiếp theo.

■ Lưu ý: XAML, giống như tất cả các ngôn ngữ dựa trên XML, phân biệt chữ hoa chữ thường. Điều đó có nghĩa là bạn không thể thay thế \<button> cho \<Button>. Tuy nhiên, bộ chuyển đổi loại thường không phân biệt chữ hoa chữ thường, có nghĩa là cả Foreground = "White" và Foreground = "white" đều có cùng kết quả.

### Tính chất phức tạp

Tiện dụng như bộ chuyển đổi loại, chúng không thực tế cho tất cả các tình huống. Ví dụ: một số thuộc tính là các đối tượng chính thức với bộ thuộc tính riêng của chúng. Mặc dù có thể tạo biểu diễn chuỗi mà trình chuyển đổi kiểu có thể sử dụng, cú pháp đó có thể khó sử dụng và dễ bị lỗi.

May mắn thay, XAML cung cấp một tùy chọn khác: cú pháp phần tử thuộc tính. Với cú pháp phần tử thuộc tính, bạn thêm phần tử con có tên trong biểu mẫu Parent.PropertyName. Ví dụ: Grid có thuộc tính Background cho phép bạn cung cấp cọ vẽ được sử dụng để vẽ khu vực phía sau các điều khiển. Nếu bạn muốn sử dụng một brush phức tạp — một cọ nâng cao hơn tô màu đồng nhất — bạn sẽ cần thêm thẻ con có tên Grid.Background, như được hiển thị ở đây:

```xaml
<Grid Name="grid1">
    <Grid.Background>
        ... 
    </Grid.Background>
    ...
</Grid>
```

Chi tiết chính làm cho công việc này là dấu chấm (.) trong tên phần tử. Điều này phân biệt các thuộc tính với các loại nội dung lồng nhau khác.

Điều này vẫn để lại một chi tiết — cụ thể là, sau khi bạn đã xác định thuộc tính phức tạp mà bạn muốn cấu hình, bạn đặt nó như thế nào? Đây là mẹo: bên trong phần tử lồng nhau, bạn có thể thêm một thẻ khác để khởi tạo một lớp cụ thể. Trong ví dụ tám quả bóng (thể hiện trong Hình 2-1), nền được lấp đầy bằng một gradient. Để xác định gradient bạn muốn, bạn cần tạo một đối tượng LinearGradientBrush.

Sử dụng các quy tắc của XAML, bạn có thể tạo đối tượng LinearGradientBrush bằng cách sử dụng một phần tử có tên LinearGradientBrush

```xaml
<Grid Name="grid1">
    <Grid.Background>
        <LinearGradientBrush>
        </LinearGradientBrush>
    </Grid.Background>
    ...
</Grid>
```

Lớp LinearGradientBrush là một phần của tập hợp không gian tên WPF, vì vậy bạn có thể tiếp tục sử dụng không gian tên XML mặc định cho các thẻ của mình.

Tuy nhiên, nó không đủ để chỉ đơn giản là tạo đối tượng LinearGradientBrush — bạn cũng cần chỉ định màu sắc trong gradient đó. Bạn thực hiện việc này bằng cách điền thuộc tính LinearGradientBrush.GradientStops với một bộ sưu tập các đối tượng GradientStop. Một lần nữa, thuộc tính GradientStops quá phức tạp để chỉ được đặt với một giá trị thuộc tính. Thay vào đó, bạn cần dựa vào cú pháp phần tử thuộc tính:

```xaml
<Grid Name="grid1">
    <Grid.Background>
        <LinearGradientBrush>
            <LinearGradientBrush.GradientStops>
            </LinearGradientBrush.GradientStops>
        </LinearGradientBrush>
    </Grid.Background>
    ...
</Grid>
```

Cuối cùng, bạn có thể điền vào bộ sưu tập GradientStops với một loạt các đối tượng GradientStop. Mỗi đối tượng GradientStop có một thuộc tính Offset và Color. Bạn có thể cung cấp hai giá trị này bằng cú pháp thuộc tính thuộc tính thông thường:

```xaml
<Grid Name="grid1">
    <Grid.Background>
        <LinearGradientBrush>
            <LinearGradientBrush.GradientStops>
                <GradientStop Offset="0.00" Color="Red" />
                <GradientStop Offset="0.50" Color="Indigo" />
                <GradientStop Offset="1.00" Color="Violet" />
            </LinearGradientBrush.GradientStops>
        </LinearGradientBrush>
    </Grid.Background>
    ...
</Grid>
```

■ Lưu ý: Bạn có thể sử dụng cú pháp phần tử thuộc tính cho bất kỳ thuộc tính nào. Nhưng thông thường, bạn sẽ sử dụng phương pháp thuộc tính thuộc tính đơn giản hơn nếu thuộc tính có công cụ chuyển đổi loại phù hợp. Làm như vậy dẫn đến mã nhỏ gọn hơn.

Bất kỳ bộ thẻ XAML nào cũng có thể được thay thế bằng một tập hợp các câu lệnh mã thực hiện cùng một tác vụ. Các thẻ được hiển thị trước đó, lấp đầy nền bằng gradient bạn chọn, tương đương với mã sau:

```csharp
LinearGradientBrush brush = new LinearGradientBrush();

GradientStop gradientStop1 = new GradientStop();
gradientStop1.Offset = 0;
gradientStop1.Color = Colors.Red;
brush.GradientStops.Add(gradientStop1);

GradientStop gradientStop2 = new GradientStop();
gradientStop2.Offset = 0.5;
gradientStop2.Color = Colors.Indigo;
brush.GradientStops.Add(gradientStop2);

GradientStop gradientStop3 = new GradientStop();
gradientStop3.Offset = 1;
gradientStop3.Color = Colors.Violet;
brush.GradientStops.Add(gradientStop3);

grid1.Background = brush;
```

### Tiện ích mở rộng đánh dấu

Đối với hầu hết các thuộc tính, cú pháp thuộc tính XAML hoạt động hoàn toàn tốt. Nhưng trong một số trường hợp, không thể mã hóa cứng giá trị tài sản. Ví dụ: bạn có thể muốn đặt giá trị thuộc tính cho một đối tượng đã tồn tại. Hoặc bạn có thể muốn đặt giá trị thuộc tính động bằng cách liên kết nó với một thuộc tính trong điều khiển khác. Trong cả hai trường hợp này, bạn cần sử dụng tiện ích đánh dấu—cú pháp chuyên biệt đặt thuộc tính theo cách không chuẩn

Phần mở rộng đánh dấu có thể được sử dụng trong các thẻ lồng nhau hoặc trong các thuộc tính XML, phổ biến hơn. Khi chúng được sử dụng trong các thuộc tính, chúng luôn được ngoặc bằng dấu ngoặc nhọn {}. Ví dụ: đây là cách bạn có thể sử dụng, cho phép bạn tham chiếu đến một thuộc tính static trong một lớp khác:

```xaml
<Button ... Foreground="{x:Static SystemColors.ActiveCaptionBrush}" >
```

Phần mở rộng đánh dấu sử dụng cú pháp {MarkupExtensionClass Argument}. Trong trường hợp này, phần mở rộng markup là lớp StaticExtension. (Theo quy ước, bạn có thể bỏ từ cuối cùng Extension khi đề cập đến một lớp mở rộng.) Tiền tố x chỉ ra rằng StaticExtension được tìm thấy trong một trong các không gian tên XAML. Bạn cũng sẽ gặp các tiện ích mở rộng đánh dấu là một phần của không gian tên WPF và không có tiền tố x.

Tất cả các phần mở rộng đánh dấu được thực hiện bởi các lớp có nguồn gốc từ System.Windows.Markup. Đánh dấu Tiện ích mở rộng. Lớp MarkupExtension cơ sở cực kỳ đơn giản — nó cung cấp một phương thức ProvideValue duy nhất nhận được giá trị bạn muốn. Nói cách khác, khi trình phân tích cú pháp XAML gặp câu lệnh trước đó, nó sẽ tạo ra một thể hiện của lớp StaticExtension (truyền vào chuỗi "SystemColors. ActiveCaptionBrush" như một đối số cho hàm tạo) và sau đó gọi ProvideValue() để lấy đối tượng được trả về bởi thuộc tính tĩnh SystemColors.ActiveCaption.Brush. Thuộc tính Foreground của nút cmdAnswer sau đó được đặt với đối tượng được truy xuất.

Kết quả cuối cùng của phần XAML này giống như khi bạn viết điều này:

```csharp
cmdAnswer.Foreground = SystemColors.ActiveCaptionBrush;
```

Vì các phần mở rộng đánh dấu ánh xạ đến các lớp, chúng cũng có thể được sử dụng làm thuộc tính lồng nhau, như bạn đã học trong phần trước. Ví dụ: bạn có thể sử dụng StaticExtension với thuộc tính Button.Foreground như sau:

```xaml
<Button ... >
    <Button.Foreground>
        <x:Static Member="SystemColors.ActiveCaptionBrush"></x:Static>
    </Button.Foreground>
</Button>
```

Tùy thuộc vào độ phức tạp của tiện ích mở rộng đánh dấu và số lượng thuộc tính bạn muốn đặt, cú pháp này đôi khi đơn giản hơn.

Giống như hầu hết các tiện ích mở rộng đánh dấu, StaticExtension cần được đánh giá trong thời gian chạy vì chỉ sau đó bạn mới có thể xác định màu hệ thống hiện tại. Một số phần mở rộng đánh dấu có thể được đánh giá tại thời điểm biên dịch. Chúng bao gồm NullExtension (xây dựng một đối tượng đại diện cho kiểu .NET). Trong suốt cuốn sách này, bạn sẽ thấy nhiều ví dụ về các tiện ích mở rộng đánh dấu tại nơi làm việc, đặc biệt là với các tài nguyên và ràng buộc dữ liệu.

### Thuộc tính đính kèm

Cùng với các thuộc tính thông thường, XAML cũng bao gồm khái niệm các thuộc tính đính kèm — các thuộc tính có thể áp dụng cho một số điều khiển nhưng được định nghĩa trong một lớp khác. Trong WPF, các thuộc tính đính kèm thường được sử dụng để kiểm soát bố cục.

Đây là cách nó hoạt động. Mỗi điều khiển đều có tập hợp các thuộc tính nội tại riêng. (Ví dụ: hộp văn bản có phông chữ, màu văn bản và nội dung văn bản cụ thể như được quyết định bởi các thuộc tính như FontFamily, ForeGround và Text.) Khi bạn đặt một điều khiển bên trong một vùng chứa, nó sẽ đạt được các tính năng bổ sung, tùy thuộc vào loại vùng chứa. (Ví dụ: nếu bạn đặt một hộp văn bản bên trong lưới, bạn cần có khả năng chọn ô lưới nơi nó được đặt.) Các chi tiết bổ sung này được đặt bằng cách sử dụng các thuộc tính đính kèm.

Các thuộc tính đính kèm luôn sử dụng tên hai phần trong biểu mẫu này: DefiningType.PropertyName. Cú pháp đặt tên hai phần này cho phép trình phân tích cú pháp XAML phân biệt giữa một thuộc tính bình thường và một thuộc tính đính kèm

Trong ví dụ tám bóng, các thuộc tính đính kèm cho phép các điều khiển riêng lẻ tự đặt mình trên các hàng riêng biệt trong lưới (vô hình):

```xaml
<TextBox ... Grid.Row="0">
    [Place question here.]
</TextBox>
<Button ... Grid.Row="1">
    [Ask the Eight Ball]
</Button>
<TextBox ... Grid.Row="2">
    [Answer will appear here.]
</TextBox>
```

Các thuộc tính đính kèm hoàn toàn không phải là thuộc tính. Chúng được dịch thành các cuộc gọi phương thức. Bộ phân tích cú pháp XAML gọi phương thức tĩnh có dạng này: DefiningType.SetPropertyName(). Ví dụ: trong đoạn mã XAML trước đó, kiểu xác định là lớp Grid và thuộc tính là Row, vì vậy trình phân tích cú pháp gọi Grid.SetRow()

Khi gọi SetPropertyName(), trình phân tích cú pháp truyền hai tham số: đối tượng đang được sửa đổi và giá trị thuộc tính được chỉ định. Ví dụ: khi bạn đặt thuộc tính Grid.Row trên điều khiển TextBox, bộ phân tích cú pháp XAML thực thi mã này:

```csharp
Grid.SetRow(txtQuestion, 0);
```

Mô hình này (gọi một phương pháp tĩnh của loại xác định) là một sự tiện lợi che giấu những gì đang thực sự diễn ra. Đối với mắt thường, mã này ngụ ý rằng số hàng được lưu trữ trong đối tượng Grid. Tuy nhiên, số hàng thực sự được lưu trữ trong đối tượng mà nó áp dụng cho—trong trường hợp này, đối tượng TextBox.

Sự khéo léo này hoạt động vì TextBox bắt nguồn từ lớp cơ sở DependencyObject, cũng như tất cả các điều khiển WPF. Và như bạn sẽ tìm hiểu trong Chương 4, DependencyObject được thiết kế để lưu trữ một bộ sưu tập các thuộc tính phụ thuộc gần như không giới hạn. (Các thuộc tính đính kèm đã được thảo luận trước đó là một loại thuộc tính phụ thuộc đặc biệt.)

Trên thực tế, phương thức Grid.SetRow() là một phím tắt tương đương với việc gọi DependencyObject. Phương thức SetValue(), như được hiển thị ở đây:

```csharp
txtQuestion.SetValue(Grid.RowProperty, 0);
```

Các thuộc tính đính kèm là một thành phần cốt lõi của WPF. Chúng hoạt động như một hệ thống mở rộng đa năng. Ví dụ: bằng cách xác định thuộc tính Hàng là thuộc tính đính kèm, bạn đảm bảo rằng thuộc tính này có thể sử dụng được với bất kỳ tùy chọn kiểm soát nào. Tùy chọn khác, làm cho thuộc tính trở thành một phần của lớp cơ sở như FrameworkElement, làm phức tạp cuộc sống. Nó không chỉ làm lộn xộn giao diện công cộng với các thuộc tính chỉ có ý nghĩa trong một số trường hợp nhất định (trong trường hợp này, khi một phần tử đang được sử dụng bên trong Grid), mà còn khiến không thể thêm các loại container mới yêu cầu các thuộc tính mới

### Các yếu tố lồng nhau
