# Uniswap-V3---theory

## Cơ chế:
- Khác với Uniswap V2 thì Uniswap V3 cho phép LPs cung cấp thanh khoản trên một khoảng giá cụ thể
  Ví dụ: cung cấp `x ETH` và `y USDC` trong phạm vi giá `ETH` từ `1500$` đến `1800$`
- ticks: là các **điểm** rời rạc trên đường cong giá, chẳng hạn điểm giá `1600$` hay `1650$`
- bands: là khoảng giá nhỏ giữa các ticks chẳng hạn từ `1500$` đến `1800$`, chia thành 5 bands tức là chia khoảng đó thành 5 phần bằng nhau với chọn các ticks là các điểm chia
  => [1500; 1560], [1560; 1620], [1620; 1680], [1680;1740], [1740; 1800]
- Ticks spacing : chinh là độ dài mỗi band (band_width)


- Trong V3, thì các LPs được phép cung cấp thanh khoản trên một khoảng giá cụ thể và được chọn số lượng band trong khoảng giá đó
- Lượng assets họ đặt vào sẽ được chia đều cho các band
- Nhận fee: Giả sử họ đặt khoảng giá `[A; B]`
  - Nếu giá hiện tại lớn hơn B (`P_cur > B`) hoặc nhỏ hơn A (`P_cur < A`) thì tức là toàn bộ số thanh khoản của bạn đã được chuyển về hết 1 loại token.
  - Ngược lai nếu `A < P_cur < B` thì thanh khoan của LPs vẫn còn cả 2 loại token và lúc này họ nhận được fee theo shares
  - Xét trong các band nhỏ trong khoảng giá đó, nếu giá hiện tại nằm ngoài khoảng band nào thì band đó chỉ còn 1 loại token.
 
