-- phpMyAdmin SQL Dump
-- version 5.2.1
-- https://www.phpmyadmin.net/
--
-- Máy chủ: 127.0.0.1
-- Thời gian đã tạo: Th10 25, 2024 lúc 05:14 PM
-- Phiên bản máy phục vụ: 10.4.32-MariaDB
-- Phiên bản PHP: 8.2.12

SET SQL_MODE = "NO_AUTO_VALUE_ON_ZERO";
START TRANSACTION;
SET time_zone = "+00:00";


/*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
/*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
/*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
/*!40101 SET NAMES utf8mb4 */;

--
-- Cơ sở dữ liệu: `bookland`
--

-- --------------------------------------------------------

--
-- Cấu trúc bảng cho bảng `contacts`
--

CREATE TABLE `contacts` (
  `id` int(10) UNSIGNED NOT NULL,
  `fullname` varchar(255) NOT NULL,
  `phone` varchar(15) NOT NULL,
  `email` varchar(255) NOT NULL,
  `message` varchar(255) NOT NULL,
  `subject` text NOT NULL,
  `answer` text DEFAULT NULL,
  `user_id` int(10) UNSIGNED NOT NULL,
  `created_at` timestamp NULL DEFAULT NULL,
  `updated_at` timestamp NULL DEFAULT NULL,
  `status` enum('Chưa phản hồi','Đã phản hồi') DEFAULT 'Chưa phản hồi'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;

--
-- Đang đổ dữ liệu cho bảng `contacts`
--

INSERT INTO `contacts` (`id`, `fullname`, `phone`, `email`, `message`, `subject`, `answer`, `user_id`, `created_at`, `updated_at`, `status`) VALUES
(1, 'Lê Minh Tâm', '0123456789', 'minhtam123@gmail.com', 'Web load không được', 'Lỗi Web', 'Chúng tôi đã sửa lỗi giúp bạn rồi ạ\r\n', 1235, '2024-11-25 10:06:05', NULL, 'Đã phản hồi');

-- --------------------------------------------------------

--
-- Cấu trúc bảng cho bảng `info`
--

CREATE TABLE `info` (
  `id` int(11) NOT NULL,
  `user_id` int(10) UNSIGNED NOT NULL,
  `fullname` varchar(255) DEFAULT NULL,
  `phone` varchar(15) DEFAULT NULL,
  `address` varchar(255) DEFAULT NULL,
  `years` date DEFAULT NULL,
  `avatar` varchar(255) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;

--
-- Đang đổ dữ liệu cho bảng `info`
--

INSERT INTO `info` (`id`, `user_id`, `fullname`, `phone`, `address`, `years`, `avatar`) VALUES
(2, 1235, 'Lê Minh Tâm', '0123456789', 'Cần Thơ', '2004-01-25', NULL);

-- --------------------------------------------------------

--
-- Cấu trúc bảng cho bảng `orders`
--

CREATE TABLE `orders` (
  `id` int(11) NOT NULL,
  `customer_name` varchar(100) NOT NULL,
  `customer_phone` varchar(15) NOT NULL,
  `customer_address` varchar(255) NOT NULL,
  `total_amount` decimal(10,2) NOT NULL,
  `created_at` timestamp NOT NULL DEFAULT current_timestamp(),
  `user_id` int(10) UNSIGNED DEFAULT NULL,
  `order_status` varchar(50) DEFAULT 'Pending',
  `shipment_date` date DEFAULT NULL,
  `sender_name` varchar(100) DEFAULT NULL,
  `shipment_notes` text DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;

--
-- Đang đổ dữ liệu cho bảng `orders`
--

INSERT INTO `orders` (`id`, `customer_name`, `customer_phone`, `customer_address`, `total_amount`, `created_at`, `user_id`, `order_status`, `shipment_date`, `sender_name`, `shipment_notes`) VALUES
(1, 'Lê Minh Tâm', '0123456789', 'Cần Thơ', 330000.00, '2024-11-25 16:03:30', 1235, 'Accepted', '0000-00-00', '', '');

-- --------------------------------------------------------

--
-- Cấu trúc bảng cho bảng `order_items`
--

CREATE TABLE `order_items` (
  `id` int(11) NOT NULL,
  `order_id` int(11) DEFAULT NULL,
  `product_name` varchar(255) DEFAULT NULL,
  `quantity` int(11) DEFAULT NULL,
  `price` decimal(10,2) DEFAULT NULL,
  `image` varchar(255) DEFAULT NULL,
  `user_id` int(11) DEFAULT NULL,
  `product_id` int(11) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;

--
-- Đang đổ dữ liệu cho bảng `order_items`
--

INSERT INTO `order_items` (`id`, `order_id`, `product_name`, `quantity`, `price`, `image`, `user_id`, `product_id`) VALUES
(1, 1, 'How Psychology Works - Hiểu Hết Về Tâm Lý Học', 1, 210000.00, 'img/tamly8.jpg', 1235, NULL),
(2, 1, 'Đứa Trẻ Hiểu Chuyện Thường Không Có Kẹo Ăn', 1, 120000.00, 'img/tamly6.jpg', 1235, NULL);

-- --------------------------------------------------------

--
-- Cấu trúc bảng cho bảng `products`
--

CREATE TABLE `products` (
  `id` int(11) NOT NULL,
  `name` varchar(255) NOT NULL,
  `price` decimal(10,2) NOT NULL,
  `date_entered` datetime NOT NULL,
  `image` varchar(255) DEFAULT NULL,
  `description` text DEFAULT NULL,
  `category` int(11) DEFAULT NULL,
  `status` varchar(20) DEFAULT NULL,
  `old_price` decimal(10,2) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;

--
-- Đang đổ dữ liệu cho bảng `products`
--

INSERT INTO `products` (`id`, `name`, `price`, `date_entered`, `image`, `description`, `category`, `status`, `old_price`) VALUES
(124, 'Thao Túng Tâm Lý Đám Đông', 80000.00, '2024-11-25 22:04:54', 'img/tl1.jpg', 'Sách Thao Túng Tâm Lý Đám Đông của Dale Carnegie là một tác phẩm cần thiết cho những ai muốn phát triển tư duy và kỹ năng giao tiếp. Cuốn sách này, được phát hành bởi SBOOKS, cung cấp những chiến lược và nguyên tắc cơ bản để hiểu và thao túng tâm lý đám đông, giúp bạn nâng cao khả năng ảnh hưởng và thuyết phục trong giao tiếp. Đây là cuốn sách mà bất kỳ ai muốn rèn luyện kỹ năng tư duy và giao tiếp cũng nên đọc. Cuốn sách chỉ cho chúng ta rằng, nghệ thuật giao tiếp không phải bạn nói được bao nhiêu mỹ từ, vẽ ra được bao nhiêu viễn cảnh, mà quan trọng là nếu bạn muốn lấy được nước mắt của người nghe thì bạn phải cho họ thấy được sự đau khổ chân thực, nếu bạn muốn thuyết phục ai đó tin vào luận điểm của bạn thì bạn phải sử dụng hệ thống dữ kiện thực tế và gần gũi với những người nghe ấy. ', 1, 'active', 0.00),
(125, 'Ký Ức Theo Dòng Đời', 175000.00, '2024-11-25 22:15:04', 'img/kinhte1.jpg', 'Ký ức theo dòng đời là tập hồi ký của Phan Chánh Dưỡng – một con người hăm hở góp phần vào công cuộc đưa nền kinh tế của TP.HCM “vượt sóng ra Biển Đông”.\r\nCuốn sách là nguồn tài liệu quý giá, cẩm nang thuyết phục về tư duy sáng tạo, cách làm đột phá và tinh thần cống hiến cho xã hội của Phan Chánh Dưỡng cùng những trí thức thế hệ ông trong Nhóm Thứ Sáu – nghiên cứu và cố vấn chính sách kinh tế.\r\nKý ức theo dòng đời là cuốn hồi ký mà thông qua chuyện dòng đời và chọn lựa lẽ sống, ta thấy được sự cống hiến và tâm tình của một trí thức trong bức tranh thời cuộc đất nước từ Bao Cấp sang Đổi Mới và Hội nhập – Toàn cầu hóa, từ thời chiến dịch chuyển sang thời bình.\r\n', 2, 'active', 0.00),
(126, 'SỬ KÝ FPT 35 NĂM - Từ Tay Trắng Đến Tập Đoàn Toàn Cầu', 300000.00, '2024-11-25 22:17:25', 'img/kinhte2.jpg', 'Trên hành trình 35 năm gây dựng và phát triển, từ không vốn liếng, không kinh nghiệm, bạn có tò mò liệu FPT đã làm những gì để vươn lên trở thành tập đoàn công nghệ tư nhân lớn nhất Việt Nam? Cuốn sách này sẽ cho bạn một phác họa chân thực về con đường gian nan mà FPT đã trải qua.\r\n\r\n \r\n“FPT 35 năm - Từ tay trắng đến tập đoàn toàn cầu” không phải là cuốn sách về kinh doanh hay quản trị. Đây là một cuốn sách ghi lại những câu chuyện, sự kiện quan trọng được chắt lọc từ những gì các nhà sáng lập, nhà lãnh đạo, quản lý và cán bộ nhân viên FPT nhiều thế hệ đã trải qua trong suốt hành trình lập nghiệp và kiến tạo FPT từ tay trắng trở thành tập đoàn toàn cầu.\r\n\r\n \r\nTiến sĩ Mai Liêm Trực - Nguyên Thứ trưởng thường trực Bộ thông tin và Truyền thông giới thiệu: Bạn đọc có thể tìm thấy trong cuốn sách nhiều bài học thực tiễn về việc xây dựng mô hình và tổ chức hoạt động của một công ty từ khởi nghiệp với con số 0 ở Việt Nam đến khi trở thành tập đoàn hùng mạnh hàng chục nghìn người trên toàn cầu, từ công tác định hướng chiến lược, lập kế hoạch, tuyển dụng và đào tạo, tiếp thị và bán hàng, nghiên cứu và phát triển, xây dựng môi trường văn hóa doanh nghiệp….', 2, 'active', 0.00),
(127, 'Kiếp nào ta cũng tìm thấy nhau', 110000.00, '2024-11-25 22:19:57', 'img/tamly1.jpg', 'Kiếp nào ta cũng tìm thấy nhau là cuốn sách thứ ba của Brain L. Weiss – một nhà tâm thần học có tiếng. Trước đó ông đã viết hai cuốn sách: cuốn đầu tiên là Ám ảnh từ kiếp trước, cuốn sách mô tả câu chuyện có thật về một bệnh nhân trẻ tuổi cùng với những liệu pháp thôi miên về kiếp trước đã làm thay đổi cả cuộc đời tác giả lẫn cô ấy. Cuốn sách đã bán chạy trên toàn thế giới với hơn 2 triệu bản in và được dịch sang hơn 20 ngôn ngữ. Cuốn sách thứ hai Through  Time  into  Healing (Đi  qua  thời  gian  để chữa lành), mô tả những gì tác giả đã học được về tiềm năng chữa bệnh của liệu pháp hồi quy tiền kiếp. Trong cuốn sách đều là những câu chuyện người thật việc thật. Nhưng  câu  chuyện  hấp  dẫn  nhất lại  nằm  trong cuốn sách thứ ba.\r\n\r\nKiếp nào ta cũng tìm thấy nhau nói về những linh hồn tri kỷ, những người có mối liên kết vĩnh viễn với nhau bằng tình yêu thương, luôn gặp lại nhau hết lần này đến lần khác, qua hết kiếp này tới kiếp khác. Chúng ta sẽ tìm thấy và nhận ra tri kỷ của mình như thế nào, rồi đưa ra những quyết định làm thay đổi cuộc sống của chính mình ra sao là những khoảnh khắc quan trọng và xúc động nhất trong cuộc đời mỗi người.\r\n\r\nĐịnh  mệnh  sẽ dẫn  lối cho  những  linh  hồn tri  kỷ hội ngộ. Chúng ta sẽ gặp họ. Nhưng quyết định làm gì sau đó lại là quyền tự do lựa chọn của mỗi người. Một lựa chọn sai lầm hoặc một cơ hội bị bỏ lỡ có thể dẫn đến nỗi cô đơn và thống khổ tột cùng. Và một lựa chọn đúng đắn, một cơ hội được nắm bắt có thể mang lại niềm hạnh phúc sâu sắc.\r\n\r\nNhững gì tác giả viết trong sách được ghi lại từ hồ sơ bệnh án, băng thu âm và trí nhớ. Chỉ có tên và một vài chi tiết nhỏ được thay đổi để giữ tính bảo mật. Đây là câu chuyện về vận mệnh và hy vọng. Đây là câu chuyện xảy ra âm thầm mỗi ngày.\r\n\r\nNgày này năm đó, đã có người lắng nghe.\r\n\r\nLinh hồn tựa như nước\r\n\r\nRơi xuống từ thiên đường\r\n\r\nLên trời như khói sương\r\n\r\nRồi trở về với đất\r\n\r\nChuỗi tuần hoàn bất tận.\r\n\r\nGOETHE', 1, 'active', 0.00),
(128, 'Trump 101: Con Đường Dẫn Đến Thành Công', 80000.00, '2024-11-25 22:21:12', 'img/kinhte3.jpg', 'Bạn đã đọc Tôi đã làm giàu như thế, Đường đến thành công đỉnh cao, Nghĩ như một tỷ phú của Donald J. Trump thì không thể bỏ qua Trump 101, con đường dẫn đến thành công.\r\n\r\nTrong cuốn sách này với vai trò vừa là nhà tư vấn, vừa là bạn đồng hành, Donald J. Trump sẽ chia sẻ cùng bạn những bí quyết cũng như những chiến lược giúp bạn phát triển khả năng của mình một cách tốt nhất và có được những định hướng đúng đắn nhất trong nghề nghiệp cũng như trong cuộc sống.', 2, 'active', 0.00),
(129, 'KINH TẾ NHẬT BẢN', 180000.00, '2024-11-25 22:22:35', 'img/kinhte4.jpg', 'Sau khi Chiến Tranh Thế giới thứ 2 kết thúc, Nhật Bản khó khăn về mọi mặt. Ngoài Hiroshima và Nagasaki bị di hại lâu dài vì chất phóng xạ của bom nguyên tử, những thành phố lớn như Tokyo cũng bị phá hủy nặng. Tái thiết đất nước lúc này là một điều vô cùng khó khăn.\r\n\r\nTuy nhiên với việc mở cửa hội nhập cùng với những chính sách của nhà nước Nhật Bản đã thay đổi hoàn toàn diện mạo kinh tế của đất nước chỉ trong vài thập kỷ, khiến cộng đồng quốc tế ngỡ ngàng.\r\n\r\nGiai đoạn phát triển ngoạn mục 18 năm (1955-1973) đã làm thay đổi hoàn toàn đời sống của người dân và vị trí của Nhật trên vũ đài quốc tế.\r\n\r\nYếu tố nào mang lại hiện tượng phát triển thần kỳ đó?', 2, 'discount', 230000.00),
(130, 'Sự Giàu Và Nghèo Của Các Dân Tộc', 280000.00, '2024-11-25 22:24:36', 'img/kinhte5.jpg', '“Sự giàu và nghèo của các dân tộc” của sử gia David Landes (1924-2013) là tác phẩm kinh điển đã tuyệt bản tại thị trường Việt Nam.\r\n\r\nTrên thế giới có khoảng 200 quốc gia và vùng lãnh thổ. Tuy nhiên, chỉ có khoảng chưa đến 20% là các quốc gia phát triển. Theo báo cáo của Oxfam (2018), 26 người giàu nhất thế giới sở hữu khối tài sản bằng với tài sản của 3,8 tỷ người thuộc nhóm nghèo nhất. Người giàu ngày càng giàu lên, trong khi người nghèo lại càng nghèo thêm. Vậy tại sao khoảng cách giàu nghèo lại lớn như vậy? Đây chính là câu hỏi mà David Landes tìm cách giải đáp trong cuốn sách này.', 2, 'discount', 460000.00),
(131, 'Trước Bình Minh Luôn Là Đêm Tối', 160000.00, '2024-11-25 22:26:17', 'img/kinhte6.jpg', 'Trước bình minh luôn là đêm tối là hành trình của một chàng trai sắp 30 tuổi, với những thành tích đáng nể và tinh thần không ngừng nỗ lực khẳng định vị thế, tầm vóc của khởi nghiệp Việt trên toàn thế giới.\r\n\r\nQua câu chuyện thành công của chính mình, tác giả chia sẻ nhiều điều về khởi nghiệp. Cụ thể: đừng để khởi nghiệp Việt Nam dừng lại ở mức “phong trào khởi nghiệp”, mà phải phát triển nó đến mức “văn hóa khởi nghiệp” thì sẽ bền vững hơn. Muốn như vậy, chúng ta cần tạo ra một thế hệ doanh nhân khởi nghiệp có trách nhiệm. Vậy, thế nào là khởi nghiệp có trách nhiệm? Khởi nghiệp có trách nhiệm không phải là hôm nay hứng… khởi nghiệp, liền nộp đơn xin nghỉ việc, không quan tâm công việc ở công ty đã được bàn giao đầy đủ hay chưa, sếp hỏi lý do tại sao thì trả lời “Tại em thích”, mặc dù sếp và công ty đối đãi mình không tệ. Vào làm có văn hóa thì nghỉ việc cũng phải có văn hóa! Khởi nghiệp có trách nhiệm không phải là bán kem trắng da, trắng liền trong 3 ngày, bất chấp hậu quả sức khỏe của khách hàng, để bán được hàng, còn khuyên là kem này mẹ bầu dùng vẫn được. Cái đó là tạo nghiệp chứ không phải khởi nghiệp!...\r\n\r\nCuốn sách còn chứa chan tình yêu thương gia đình – nơi để trở về mỗi lần mệt mỏi với dông bão ngoài kia với lòng biết ơn sâu sắc. “Những người sẵn lòng đặt con tim của họ vào “cái hòm kín” của bạn, sẵn sàng lấp đầy con tim của bạn, sẵn sàng ở bên cạnh bạn dù lúc thành công hay khi thất bại, không ai khác, chính là Gia đình của bạn!”\r\n\r\nNgoài ra còn nhiều chia sẻ bổ ích, thú vị, sâu sắc về thành công, nỗi buồn, hạnh phúc khác từ chính cuộc đời tác giả, chắc chắn sẽ khiến độc giả vỡ ra nhiều điều trong cuộc sống.', 1, 'active', 0.00),
(132, 'Vanderbilt - Tài Phiệt Đầu Tiên Của Nước Mỹ', 400000.00, '2024-11-25 22:27:46', 'img/kinhte7.jpg', 'Cuốn tiểu sử này cung cấp những thông tin sâu rộng về sự nghiệp kinh doanh và cuộc sống cá nhân của Phó đề đốc Vanderbilt — ông trùm doanh nghiệp vĩ đại đầu tiên trong lịch sử Hoa Kỳ và là người sáng lập triều đại Vanderbilt.\r\n\r\nTrong số tất cả các nhà công nghiệp và nhân vật tài chính quan trọng của lịch sử Hoa Kỳ, Vanderbilt có thể coi là người đóng vai trò quan trọng nhất. Tuy nhiên, không giống như Jay Gould, JP Morgan, John D. Rockefeller và Andrew Carnegie, Ngài Phó đề đốc chưa bao giờ có được cho mình một cuốn tiểu sử đầy đủ và chính xác. Cuốn sách của tác giả T.J. Stiles là thành quả của sáu năm nghiên cứu chuyên sâu (trong các kho lưu trữ chưa được khai thác trước đây), được tổng hợp thành một câu chuyện có nhịp độ nhanh về một con người và đất nước cùng nhau vươn lên.\r\nTừ tuổi thơ có phần khiêm tốn trên Đảo Staten dưới thời Tổng thống George Washington cho đến thời của John D. Rockefeller (người mà Vanderbilt đã thực hiện các giao dịch), cuốn sách kể lại quá trình thăng tiến của Vanderbilt từ người lái thuyền buồm đến doanh nhân tàu hơi nước, từ bậc thầy điều hành các tuyến tàu hơi nước xuyên đại dương đến người xây dựng đế chế đường sắt. Trong quá trình ấy, Stiles mô tả những cuộc phiêu lưu cá nhân của Vanderbilt trong rừng rậm Nicaragua, những chiến dịch hoành tráng của ông ở Phố Wall và cả những âm mưu chia rẽ gia đình ông. Quan trọng nhất, Stiles cho thấy Vanderbilt đã giúp hình thành tư duy của người Mỹ về sự bình đẳng và cơ hội cũng như tạo ra thế giới kinh tế hiện đại như thế nào.', 2, 'active', 0.00),
(133, 'Hoảng Loạn, Hỗn Loạn Và Cuồng Loạn', 95000.00, '2024-11-25 22:28:42', 'img/kinhte8.jpg', 'Trong Hoảng loạn, Hỗn loạn và Cuồng loạn Kindleberger đã tiếp cận chủ đề khủng hoảng theo cách thức khác biệt mà rất ít người lựa chọn. Thay vì liệt kê hàng loạt phương trình toán học phức tạp, ông lại lý giải các cuộc khủng hoảng xác thực hơn bằng những giai thoại và ví dụ thực tiễn. Kindleberger chỉ ra quan niệm thông thường cho rằng hành động của con người là hợp lý và minh chứng một thực tế rằng nạn đầu cơ dẫn đến sự bất ổn định là hiện tượng rất phổ biến, và rằng rất nhiều cuộc khủng hoảng lại xuất phát từ những hành vi phi lý của con người, ví dụ như sự điên cuồng và hoảng loạn.\r\n\r\nSúc tích, giàu thông tin. Hoảng loạn, Hỗn loạn và Cuồng loạn thâu tóm gần 400 năm lịch sử tài chính thế giới với 10 cuộc khủng hoảng lớn. Xuyên suốt cuốn sách, ông đưa ra một câu hỏi mấu chốt là liệu những người cho vay cuối cùng có xuất hiện trong các cuộc khủng hoảng đó không, và nếu không thì liệu thực tế có khác đi? Theo Kindleberger, bên cạnh những tác động tích cực mang lại một số vấn đề.\r\n\r\nBằng cách bơm thêm tiền cho các công ty quản lý tồi, những tổ chức này sẽ góp phần tạo ra thông lệ nguy hiểm và làm tiêu tan động lực cải thiện hoạt động của các công ty Có thể coi Hoảng loạn, Hỗn loạn và Cuồng loạn là bản sử ký thú vị và hấp dẫn về con đường dẫn đến các cuộc khủng hoảng tài chính qua hàng thế kỷ nay. Bất cứ ai quan tâm và muốn học hỏi từ lịch sử, hay muốn đầu tư khôn ngoan đều không thể không đọc cuốn sách này.', 1, 'active', 0.00),
(134, 'Facebook - Bí Mật Về Quốc Gia Lớn Nhất Thế Giới', 300000.00, '2024-11-25 22:29:34', 'img/kinhte9.jpg', 'Cuốn sách nói về sự hình thành và phát triển của Facebook cùng những khó khăn, thách thức mà công ty này từng phải trải qua. Trong năm thứ hai đại học, Mark Zuckerberg đã tạo ra một trang web đơn giản hoạt động như một mạng xã hội trong khuôn viên trường. Trang này được đón nhận vô cùng mạnh mẽ và rất nhanh sau đó sinh viên trên toàn quốc đã đăng ký sử dụng Facebook. Từ một trang web đơn giản ban đầu, Mark Zuckerberg cùng đội ngũ đã nghiên cứu và phát triển thêm nhiều tính năng và ứng dụng cho Facebook, có những tính năng được đón nhận nhưng cũng có những tính năng thất bại và nhanh chóng biến mất sau đó. Và khi Facebook phát triển cũng là lúc các đối thủ cạnh tranh bắt đầu xuất hiện như Instagram, Snapchat… Cuốn sách cũng đưa ra thông tin về những cuộc đàm phán mua lại các công ty này của Zuckerberg. Càng phát triển mạnh mẽ, Facebook càng phải đối mặt với nhiều thách thức, khó khăn khi gặp phải những cáo buộc liên quan đến việc Facebook là nhân tố góp phần tác động vào kết quả của cuộc tranh cử tổng thống Mỹ năm 2016 giữa Donald Trump và Hillary Clinton khi công ty này không xử lý được việc những tin giả lan truyền trên Facebook và những hacker sử dụng nó để đánh cắp thông tin, cùng vụ bê bối dữ liệu Cambridge Analytica. Tác giả cũng đưa ra những thông tin về cách xử lý của Facebook cũng như Mark Zuckerberg đối với tin giả mạo, việc xử lý dữ liệu thông tin của người dùng cũng như kiểm duyệt nội dung.  ', 2, 'active', 0.00),
(136, 'Sói Già Phố Wall - Phần 3', 120000.00, '2024-11-25 22:33:44', 'img/kinhte11.jpg', 'Jordan Belfort với vẻ ngoài lịch lãm, cuốn hút cùng tài ăn nói khéo léo. Từ một kẻ vô danh tiểu tốt trở thành một ông trùm chứng khoán đứng trên đỉnh của phố Wall. Nhưng phía sau những hào nhoáng đó hẳn phải chứa đựng những bí mật \"động trời\" với những mánh khóe chỉ trong vài phút hàng triệu đô-la đã bỏ túi của gã vô danh khéo ăn khéo nói đó.\r\n\r\nCuốn tự truyện \"Sói già phố Wall\" của Jordan Belfort ra mắt vào tháng 9 năm 2007, đã trở thành hiện tượng xuất bản toàn cầu với nhiều bản sách đã được bán ra. Cuốn tự truyện không đơn giản chỉ là kể về cuộc đời của một gã \"lọc lừa\" với nhiều những mánh khóe tinh vi, mà sâu xa hơn nữa là toàn cảnh bức tranh về phố Wall và thị trường chứng khoán. Chân thực và lôi cuốn là hai từ có thể nói về cuốn hồi ký này.\r\n\r\n\"Sói già phố Wall\" đã được đạo diện gạo cội Martin Scorsese chuyển thể thành phim vào năm 2013 với sự tham gia của các diễn viên nổi tiếng Hollywood như Leonardo DiCaprio, Jonah Hill, Margot Robbie và Matthew McConaughey. Bộ phim đem tới cho người xem một trải nghiệm mới mẻ, góp phần \"tái hiện\" lại một cách chân thực về chân dung của \"Ông trùm phố Wall - Jordan Belfort\".\r\n\r\nTập cuối \"Sói già phố Wall 3 - Con đường của sói” sẽ cho ta thấy hồi kết cho bộ hồi ký nối tiếng và hấp dẫn này.', 1, 'active', 0.00),
(137, 'Thuật Thao Túng - Góc Tối Ẩn Sau Mỗi Câu Nói', 140000.00, '2024-11-25 22:34:52', 'img/tamly2.jpg', 'Bạn có muốn giành phần thắng cuối cùng trong các cuộc tranh luận?\r\n\r\nBạn có muốn dẹp đi bộ mặt kiêu ngạo của các đồng nghiệp xung quanh mình?\r\n\r\nBạn có muốn chứng minh rằng bạn đã đúng về mọi thứ?\r\n\r\nĐây là quyển sách chứa đựng đáp án mà bạn mong muốn. Thuật thao túng sẽ giúp bạn thuần thục các kỹ năng thuộc bộ môn “nghệ thuật” làm chủ cảm xúc, làm chủ vận mệnh, điều chỉnh tâm lý và đạt được thứ bạn muốn một cách tinh vi: thao túng tâm lý người đối diện, khiến họ hành động theo hướng ta mong đợi. Không những vậy, quyển sách còn giúp bạn nhìn nhận lại về định nghĩa thao túng, những tốt-xấu ẩn giấu đằng sau và giải đáp vấn đề đạo đức con người mà bạn luôn trăn trở khi thực hiện những hành vi này. Bật mí, con người khi vừa sinh ra đã làm một thao tác thao túng tâm lý người khác rồi đấy!\r\n\r\nCó thể bạn chưa biết, bạn đã và đang thao túng người khác hoặc bị người khác thao túng thông qua cử chỉ ngôn hành mỗi ngày, như-một-trò-đùa.\r\n\r\nCó thể bạn chưa biết, nạn nhân bị thao túng chưa chắc đã rơi vào tình thế bất lợi, nhưng rơi vào tình thế bất lợi chắc chắn đã bị thao túng.\r\n\r\nCó thể bạn chưa biết, người có đạo đức chắc chắn không thao túng người khác, nhưng kẻ thao túng người khác chưa chắc đã vô đạo đức.', 1, 'active', 0.00),
(138, 'Định Luật Murphy- Mọi Bí Mật Tâm Lý Thao Túng Cuộc Đời Bạn', 150000.00, '2024-11-25 22:36:43', 'img/tamly4.jpg', 'Định Luật Murphy – Mọi Bí Mật Tâm Lý Thao Túng Cuộc Đời Bạn\r\n\r\nNếu một điều tồi tệ có thể xảy ra, nó sẽ xảy ra!\r\n\r\nKhi một món đồ quan trọng bị rơi, nó có xu hướng lăn tới dưới ngăn tủ nặng nhất.\r\n\r\nKhi hai tay bạn cầm đầy đồ đạc, mũi bạn bắt đầu ngứa. \r\n\r\nKhi bạn sợ gặp một người nào đó ở bên ngoài, bạn luôn vô tình gặp phải người đó.\r\n\r\n…\r\n\r\nCó phải hằng ngày bạn hay gặp những chuyện dở khóc dở cười tương tự như vậy? Những hiện tượng này đều có thể giải thích bằng một khái niệm tâm lý học thú vị: Định luật Murphy. Nó nhắc nhở chúng ta rằng việc xấu luôn có “cơ may” cao hơn và sai lầm luôn là một phần của thế giới này. Dù cho mỗi chúng ta đều cố gắng hết sức để tránh khỏi sai lầm, nhưng trên thực tế đó là điều bất khả thi.\r\n\r\nTuy nhiên, định luật Murphy mang tính cảnh tỉnh và dẫn dắt rất lớn trong cuộc sống hằng ngày. Cuốn sách này giới thiệu đến với bạn đọc về kiến thức cơ bản, hiện tượng thường gặp cùng với các hiệu ứng tâm lý học biểu hiện trong ý thức cá nhân, tính cạnh tranh, quan hệ xã hội,… của định luật Murphy thông qua góc nhìn thực tiễn. Từ đó giúp bạn đọc hiểu được bản chất con người, bản chất xã hội rồi ứng dụng nó vào giải quyết các vấn đề gặp phải trong cuộc sống.', 1, 'active', 0.00),
(139, 'Lý Thuyết Trò Chơi', 120000.00, '2024-11-25 22:37:17', 'img/tamly3.jpg', 'Đời người giống như trò chơi, mỗi bước đều phải cân nhắc xem đi như thế nào, đi về đâu, phải kết hợp nhiều yếu tố lại chúng ta mới có thể đưa ra được lựa chọn. Mà trong quá trình chọn lựa này các yếu tố khiến ta phải cân nhắc và những đường đi khác nhau sẽ ảnh hưởng trực tiếp đến kết quả.\r\n\r\nCuốn sách Lý thuyết trò chơi là bách khoa toàn thư về tâm lý học, về tẩy não và chống lại tẩy não, thao túng và chống lại thao túng, thống trị và chống lại thống trị. Cuốn sách giới thiệu công thức chiến thắng cho những “trò chơi” đấu trí giữa người với người trong cuộc sống hằng ngày; phân tách các khái niệm lý thuyết trò chơi vốn mơ hồ trở thành ngôn ngữ dễ hiểu và kết nối liền mạch với nghệ thuật tâm lý học; cho phép bạn nắm vững những bí ẩn của trò chơi tâm lý trong thời gian ngắn nhất.\r\n\r\nNhững kỹ năng trong Lý thuyết trò chơi có thể giúp chúng ta đọc thấu hoạt động tâm lý người khác, và từ đó chiếm thế chủ động trong trò chơi đấu trí giữa những người xung quanh.', 1, 'active', 0.00),
(140, 'Thiên Tài Bên Trái, Kẻ Điên Bên Phải', 180000.00, '2024-11-25 22:38:01', 'img/tamly5.jpg', 'Hỡi những con người đang oằn mình trong cuộc sống, bạn biết gì về thế giới của mình? Là vô vàn thứ lý thuyết được các bậc vĩ nhân kiểm chứng, là luật lệ, là cả nghìn thứ sự thật bọc trong cái lốt hiển nhiên, hay những triết lý cứng nhắc của cuộc đời?\r\n\r\nLại đây, vượt qua thứ nhận thức tẻ nhạt bị đóng kín bằng con mắt trần gian, khai mở toàn bộ suy nghĩ, để dòng máu trong bạn sục sôi trước những điều kỳ vĩ, phá vỡ mọi quy tắc. Thế giới sẽ gọi bạn là kẻ điên, nhưng vậy thì có sao? Ranh giới duy nhất giữa kẻ điên và thiên tài chẳng qua là một sợi chỉ mỏng manh: Thiên tài chứng minh được thế giới của mình, còn kẻ điên chưa kịp làm điều đó. Chọn trở thành một kẻ điên để vẫy vùng giữa nhân gian loạn thế hay khóa hết chúng lại, sống mãi một cuộc đời bình thường khiến bạn cảm thấy hạnh phúc hơn?\r\n\r\nThiên tài bên trái, kẻ điên bên phải là cuốn sách dành cho những người điên rồ, những kẻ gây rối, những người chống đối, những mảnh ghép hình tròn trong những ô vuông không vừa vặn… những người nhìn mọi thứ khác biệt, không quan tâm đến quy tắc. Bạn có thể đồng ý, có thể phản đối, có thể vinh danh hay lăng mạ họ, nhưng điều duy nhất bạn không thể làm là phủ nhận sự tồn tại của họ. Đó là những người luôn tạo ra sự thay đổi trong khi hầu hết con người chỉ sống rập khuôn như một cái máy. Đa số đều nghĩ họ thật điên rồ nhưng nếu nhìn ở góc khác, ta lại thấy họ thiên tài. Bởi chỉ những người đủ điên nghĩ rằng họ có thể thay đổi thế giới mới là những người làm được điều đó. \r\n\r\nChào mừng đến với thế giới của những kẻ điên.', 1, 'active', 0.00),
(141, 'Tâm Lý Học Tội Phạm', 100000.00, '2024-11-25 22:42:56', 'img/tamly10.jpg', 'Tội phạm, nhất là những vụ án mạng, luôn là một chủ đề thu hút sự quan tâm của công chúng, khơi gợi sự hiếu kỳ của bất cứ ai. Một khi đã bắt đầu theo dõi vụ án, hẳn bạn không thể không quan tâm tới kết cục, đặc biệt là cách thức và động cơ của kẻ sát nhân, từ những vụ án phạm vi hẹp cho đến những vụ án làm rúng động cả thế giới.\r\n\r\nLấy 36 vụ án CÓ THẬT kinh điển nhất trong hồ sơ tội phạm của FBI, “Tâm lý học tội phạm - phác họa chân dung kẻ phạm tội” mang đến cái nhìn toàn cảnh của các chuyên gia về chân dung tâm lý tội phạm. Trả lời cho câu hỏi: Làm thế nào phân tích được tâm lý và hành vi tội phạm, từ đó khôi phục sự thật thông qua các manh mối, từ hiện trường vụ án, thời gian, dấu tích,… để tìm ra kẻ sát nhân thực sự. \r\n\r\nĐằng sau máu và nước mắt là các câu chuyện rợn tóc gáy về tội ác, góc khuất xã hội và những màn đấu trí đầy gay cấn giữa điều tra viên và kẻ phạm tội. Trong số đó có những con quỷ ăn thịt người; những cô gái xinh đẹp nhưng xảo quyệt; và cả cách trả thù đầy man rợ của các nhà khoa học,… Một số đã sa vào lưới pháp luật ngay khi chúng vừa ra tay, nhưng cũng có những kẻ cứ vậy ngủ yên hơn hai mươi năm. \r\n\r\nBằng giọng văn sắc bén, “Tâm lý học tội phạm - phác họa chân dung kẻ phạm tội” hứa hẹn dẫn dắt người đọc đi qua các cung bậc cảm xúc từ tò mò, ngạc nhiên đến sợ hãi, hoang mang tận cùng. Chúng ta sẽ lần tìm về quá khứ để từng bước gỡ những nút thắt chưa được giải, khiến ta \"ngạt thở\" đọc tới tận trang cuối cùng. \r\n\r\nHy vọng cuốn sách sẽ giúp bạn có cái nhìn sâu sắc, rõ ràng hơn về bộ môn tâm lý học tội phạm và có thể rèn luyện thêm sự tư duy, nhạy bén.', 1, 'active', 0.00),
(142, 'Đứa Trẻ Hiểu Chuyện Thường Không Có Kẹo Ăn', 120000.00, '2024-11-25 22:43:53', 'img/tamly6.jpg', '“Đứa trẻ hiểu chuyện thường không có kẹo ăn” – Cuốn sách dành cho những thời thơ ấu đầy vết thương.\r\n\r\nTrên đời này có một điều rất kỳ diệu, đó là bậc phụ huynh nào cũng mong muốn con mình trở nên hoàn hảo theo một hình mẫu giống hệt nhau.\r\n\r\nLanh lẹ, khôn khéo, dễ thương, luôn nhìn cha mẹ với gương mặt tươi cười trong sáng.\r\n\r\nKhi người lớn yêu cầu chúng làm gì đó, chúng sẽ vui vẻ làm theo. Không phàn nàn, không oán trách, không cáu gắt, lại càng không phản kháng cãi cự.\r\n\r\nNhững khi cha mẹ mệt mỏi hay chán chường, chúng sẽ rúc vào lòng cha mẹ như một chú chim nhỏ, giúp họ giải tỏa ưu tư phiền muộn.\r\n\r\nThậm chí ngay cả khi cha mẹ cáu giận, đối xử bất công với chúng, chúng cũng phải nhanh chóng tha thứ, dịu dàng an ủi ngược lại cha mẹ.\r\n\r\nChúng chẳng khác nào một con búp bê phó mặc hoàn toàn cho người khác sắp xếp. Thà bản thân chịu thiệt cũng không để cha mẹ buồn lòng.\r\n\r\nNhưng bạn biết không, đằng sau những đứa trẻ hiểu chuyện ngoan ngoãn trong mơ ấy, hóa ra lại toàn là sự tổn thương. Chúng không muốn tổn thương người khác, vì vậy chúng lựa chọn tổn thương chính mình.\r\n\r\nMà chúng làm tất cả những điều đó chỉ đơn giản là vì yêu thương cha mẹ mình mà thôi.\r\n\r\nNếu bạn cũng từng là một đứa trẻ như thế, từng phải hạ thấp bản thân, từng buộc phải nhường nhịn người khác, từng phải học cách nhận biết sắc mặt từ khi còn quá nhỏ… thì nhất định đừng bỏ qua cuốn sách “Đứa trẻ hiểu chuyện thường không có kẹo ăn” của tác giả Nguyên Anh.\r\n\r\nVới tư cách cố vấn cấp hai quốc gia, Nguyên Anh đã từng là người tìm cách chữa lành vết thương cho hàng nghìn tâm hồn mang theo tổn thương thời thơ ấu. Từng câu, từng chữ bà viết nên đều xuất phát từ những câu chuyện hoàn toàn có thật.\r\n\r\nCó thể sau khi đọc xong, những vết thương của bạn vẫn sẽ chẳng thể lành lại vĩnh viễn, nhưng chỉ cần bạn cảm thấy ổn hơn một chút, như vậy là đủ rồi.', 1, 'discount', 150000.00),
(143, 'Hiểu Về Bản Chất Con Người - Lý Luận Của Bậc Thầy Tâm Thần Học', 105000.00, '2024-11-25 22:45:11', 'img/tamly7.jpg', 'Khi không thể tìm kiếm được hạnh phúc, chúng ta thường có xu hướng tin rằng cuộc sống con người được sắp đặt bởi số phận. Có những người sinh ra đã ở vạch đích; còn cuộc sống chúng ta thì chỉ toàn là biến cố, số phận định sẵn ta sẽ có một cuộc sống vất vả. Có thật sự là như vậy không?\r\n\r\nKỳ thực, đây là cách con người cảm thấy bất lực và ‘đầu hàng’ trước hoàn cảnh. Đối với Alfred Adler - Chuyên gia tâm thần học hàng đầu nước Anh, người được mệnh danh là một trong “ba người khổng lồ của tâm lý học hiện đại” - lại chủ trương “cuộc đời ta là do ta lựa chọn”. Học thuyết tâm lý học cá nhân của ông đã chỉ ra khuôn mẫu hành vi mới chính là thứ khiến một cá nhân không thể cảm thấy hạnh phúc. Chúng ta thường đi theo một khuôn mẫu hành vi nhất định nhằm theo đuổi vị thế được tạo dựng từ cảm nhận xã hội.\r\n\r\nĐể thay đổi và điều chỉnh những quan điểm sai lệch về khuôn mẫu hành vi, chúng ta cần phải có kiến thức về bản chất con người. Cuốn sách “HIỂU VỀ BẢN CHẤT CON NGƯỜI - LÝ LUẬN CỦA BẬC THẦY TÂM THẦN HỌC” sẽ giúp chúng ta làm quen với những nguyên tắc cơ bản của tâm lý học cá nhân và hướng dẫn cách áp dụng các nguyên tắc này vào các mối quan hệ hàng ngày và việc tổ chức đời sống cá nhân.\r\n\r\nCuốn sách gồm 2 phần:\r\n\r\n- Phần I sẽ đi sâu vào phân tích hành vi con người, cách mà một cá nhân hành động hoặc phản ứng để đối phó với các tình huống kích thích từ bên ngoài hoặc bên trong,\r\n\r\n- Phần II bàn luận về đặc tính khi xem xét mối quan hệ giữa một cá nhân và môi trường sống, hay còn gọi chung là nghiên cứu về khoa học tính cách.\r\n\r\nCuốn sách cũng chỉ ra những đặc điểm tính cách không xuất phát từ yếu tố di truyền mà phát triển dựa theo khuôn mẫu của sự phát triển tinh thần, từ đó định hướng mục tiêu cá nhân. Quy luật này đóng vai trò quan trọng với bất cứ cá nhân nào muốn tự quyết định số phận của mình, thay vì trở thành nạn nhân của những khuynh hướng bi quan.\r\n\r\nĐiều kiện tối thiểu để đạt được hạnh phúc chính là biết mình và hiểu mình. Hy vọng cuốn sách có thể giúp bạn tìm thấy một tư tưởng mới, tự quyết định lấy “số phận” của bản thân cho dù có ở trong hoàn cảnh khó khăn tăm tối đến mức nào.', 1, 'active', 0.00),
(144, 'How Psychology Works - Hiểu Hết Về Tâm Lý Học', 210000.00, '2024-11-25 22:46:19', 'img/tamly8.jpg', 'Ám sợ là gì, ám sợ có thực sự đáng sợ không? Rối loạn tâm lý là gì, làm thế nào để thoát khỏi tình trạng suy nhược và xáo trộn đó? Trầm cảm là gì, vì sao con người hiện đại thường xuyên gặp và chống chọi với tình trạng u uất, mệt mỏi và tuyệt vọng này?\r\n\r\nTìm hiểu về các vấn đề tâm trí của con người luôn đầy sức hấp dẫn và lôi cuốn, vì vậy mà tâm lý học ra đời, hình thành và phát triển rất nhiều các học thuyết và trường phái. Cuốn sách này dẫn dắt bạn đọc qua hành trình tìm hiểu các học thuyết và trường phái đó, về cách các nhà tâm lý diễn giải hành xử và tâm trí con người. Tại sao chúng ta có những hành vi, suy nghĩ và cảm xúc như vậy, chúng diễn ra và kết thúc như thế nào, chúng ảnh hưởng lâu dài, gián đoạn hay ngắn ngủỉ đến đời sống của chúng ta ra sao, làm thế nào để chúng ta thoát khỏi những tác động tiêu cực của chúng?\r\n\r\nCuốn sách có cấu trúc khoa học, trình bày dễ hiểu, súc tích, thiết kế và minh họa đẹp mắt này sẽ mang đến cho bạn những hiểu biết về các học thuyết tâm lý và các phương pháp trị liệu, từ các vấn đề cá nhân đến những ứng dụng thực tế.', 1, 'discount', 300000.00),
(145, 'Bạn Là Bác Sĩ Tâm Lý Của Chính Mình', 75000.00, '2024-11-25 22:47:02', 'img/tamly9.jpg', 'Cuộc đời là một hành trình dài và hành trình để trưởng thành về tinh thần cũng vậy. Trên quãng đường này sẽ xuất hiện không ít khó khăn hay thậm chí có những lúc chúng ta sụp đổ và để cảm xúc tiêu cực điều khiển chính mình. Tuy nhiên, chỉ cần nhận thức được một điều rằng: Bạn là người phải chịu trách nhiệm với những cảm xúc bên trong mình và khi gặp phải vấn đề tâm lý, dù người khác có giúp đỡ nhiều ra sao, nếu bạn không thay đổi góc nhìn, không luyện tập để tâm trí trở nên mạnh mẽ hơn thì tất cả đều là vô ích.\r\n\r\nĐây chính là thông điệp được tác giả Lý Hoành Phu truyền tải xuyên suốt cuốn sách “Bạn là bác sĩ tâm lý của chính mình”. Cuốn sách tập trung vào chủ đề làm thế nào để vượt qua các cảm xúc tiêu cực khác nhau một cách hiệu quả. Tác giả giải thích bản chất của những cảm xúc bên trong con người, từ đó đưa ra các lời khuyên và phương pháp giúp điều tiết cảm xúc, thoát khỏi các hội chứng rối loạn ám ảnh cưỡng chế, rối loạn lo âu và trầm cảm,… Đặc biệt, phương án luyện tập chuyển hóa cảm xúc trong 7 ngày được tác giả tổng hợp cho phép mọi người nhận thức rõ ràng rằng những cảm xúc tiêu cực khác nhau nảy sinh từ bên trong chỉ là biểu hiện của việc chúng ta không thực sự hiểu con người thật của mình.\r\n\r\nVới lối diễn đạt đơn giản, dễ hiểu, tin rằng cuốn sách sẽ có tác dụng giải tỏa tốt cho những người sống dưới áp lực tinh thần cao và mỗi bạn đọc đều có thể dễ dàng điều chỉnh, loại bỏ những cảm xúc tiêu cực và đạt được một cuộc sống như ý muốn.', 1, 'active', 0.00);

-- --------------------------------------------------------

--
-- Cấu trúc bảng cho bảng `users`
--

CREATE TABLE `users` (
  `id` int(10) UNSIGNED NOT NULL,
  `name` varchar(255) NOT NULL,
  `email` varchar(255) NOT NULL,
  `pass` varchar(255) NOT NULL,
  `created_at` timestamp NULL DEFAULT NULL,
  `updated_at` timestamp NULL DEFAULT NULL,
  `locked` tinyint(1) DEFAULT 0
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;

--
-- Đang đổ dữ liệu cho bảng `users`
--

INSERT INTO `users` (`id`, `name`, `email`, `pass`, `created_at`, `updated_at`, `locked`) VALUES
(1234, 'Thiet', 'tn0303vnvn@gmail.com', 'Thiet123@', '2024-11-25 12:19:39', NULL, 1),
(1235, 'minhtam123', 'minhtam123@gmail.com', '$2y$10$iHgjre2Sap5iDK8um3XwwOCGEfXN1E8tL6XT9U77t1wBXAkO0/bqi', '2024-11-25 10:01:49', '2024-11-25 10:01:59', 0);

--
-- Chỉ mục cho các bảng đã đổ
--

--
-- Chỉ mục cho bảng `contacts`
--
ALTER TABLE `contacts`
  ADD PRIMARY KEY (`id`),
  ADD KEY `contacts_user_id_foreign` (`user_id`);

--
-- Chỉ mục cho bảng `info`
--
ALTER TABLE `info`
  ADD PRIMARY KEY (`id`),
  ADD KEY `user_id` (`user_id`);

--
-- Chỉ mục cho bảng `orders`
--
ALTER TABLE `orders`
  ADD PRIMARY KEY (`id`),
  ADD KEY `fk_user_id` (`user_id`);

--
-- Chỉ mục cho bảng `order_items`
--
ALTER TABLE `order_items`
  ADD PRIMARY KEY (`id`),
  ADD KEY `order_id` (`order_id`),
  ADD KEY `product_id` (`product_id`);

--
-- Chỉ mục cho bảng `products`
--
ALTER TABLE `products`
  ADD PRIMARY KEY (`id`);

--
-- Chỉ mục cho bảng `users`
--
ALTER TABLE `users`
  ADD PRIMARY KEY (`id`),
  ADD UNIQUE KEY `users_email_unique` (`email`);

--
-- AUTO_INCREMENT cho các bảng đã đổ
--

--
-- AUTO_INCREMENT cho bảng `contacts`
--
ALTER TABLE `contacts`
  MODIFY `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=2;

--
-- AUTO_INCREMENT cho bảng `info`
--
ALTER TABLE `info`
  MODIFY `id` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=3;

--
-- AUTO_INCREMENT cho bảng `orders`
--
ALTER TABLE `orders`
  MODIFY `id` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=2;

--
-- AUTO_INCREMENT cho bảng `order_items`
--
ALTER TABLE `order_items`
  MODIFY `id` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=3;

--
-- AUTO_INCREMENT cho bảng `products`
--
ALTER TABLE `products`
  MODIFY `id` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=146;

--
-- AUTO_INCREMENT cho bảng `users`
--
ALTER TABLE `users`
  MODIFY `id` int(10) UNSIGNED NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=1236;

--
-- Các ràng buộc cho các bảng đã đổ
--

--
-- Các ràng buộc cho bảng `contacts`
--
ALTER TABLE `contacts`
  ADD CONSTRAINT `contacts_user_id_foreign` FOREIGN KEY (`user_id`) REFERENCES `users` (`id`) ON DELETE CASCADE;

--
-- Các ràng buộc cho bảng `info`
--
ALTER TABLE `info`
  ADD CONSTRAINT `info_ibfk_1` FOREIGN KEY (`user_id`) REFERENCES `users` (`id`) ON DELETE CASCADE;

--
-- Các ràng buộc cho bảng `orders`
--
ALTER TABLE `orders`
  ADD CONSTRAINT `fk_user_id` FOREIGN KEY (`user_id`) REFERENCES `users` (`id`) ON DELETE SET NULL;

--
-- Các ràng buộc cho bảng `order_items`
--
ALTER TABLE `order_items`
  ADD CONSTRAINT `fk_product` FOREIGN KEY (`product_id`) REFERENCES `products` (`id`) ON DELETE CASCADE,
  ADD CONSTRAINT `order_items_ibfk_1` FOREIGN KEY (`order_id`) REFERENCES `orders` (`id`) ON DELETE CASCADE;
COMMIT;

/*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
/*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
/*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;
