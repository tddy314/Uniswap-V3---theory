# Uniswap-V3---theory

## Cơ chế:
- Khác với Uniswap V2 thì Uniswap V3 cho phép LPs cung cấp thanh khoản trên một khoảng giá cụ thể
  Ví dụ: cung cấp `x ETH` và `y USDC` trong phạm vi giá `ETH` từ `1500$` đến `1800$`
- ticks: là các **điểm** rời rạc trên đường cong giá, chẳng hạn điểm giá `1600$` hay `1650$`
- bands: là khoảng giá nhỏ giữa các ticks chẳng hạn từ `1500$` đến `1800$`, chia thành 5 bands tức là chia khoảng đó thành 5 phần bằng nhau với chọn các ticks là các điểm chia
  => [1500; 1560], [1560; 1620], [1620; 1680], [1680;1740], [1740; 1800]
- Ticks spacing : chinh là độ dài mỗi band (band_width)

Trong Uniswap V3, các tick không được chọn sẵn một cách cụ thể, nhưng chúng tuân theo một quy tắc toán học cố định. Cụ thể:

Tick Spacing:

Mỗi pool có một tick spacing cố định được đặt khi pool được tạo.
Tick spacing xác định khoảng cách tối thiểu giữa hai tick hợp lệ. Ví dụ, nếu tick spacing là 10, thì các tick hợp lệ sẽ là:
.
.
.
,
−
20
,
−
10
,
0
,
10
,
20
,
30
,
.
.
.
...,−20,−10,0,10,20,30,...
Điều này giúp giới hạn số lượng tick để tối ưu hóa hiệu suất.
Ticks đại diện cho mức giá:

Ticks trong Uniswap V3 không phải là giá trực tiếp mà là các logarithmic price increments.
Giá tương ứng với một tick 
𝑖
i được tính theo công thức:
𝑃
𝑖
=
1.0001
𝑖
P 
i
​
 =1.0001 
i
 
Vì vậy, các ticks tạo thành một lưới giá logarit thay vì tuyến tính.
Liquidity Providers (LPs) chọn range tùy ý:

LP có thể cung cấp thanh khoản trong bất kỳ khoảng giá nào bằng cách chọn hai tick: tick thấp (i_l) và tick cao (i_u).
Họ chỉ cung cấp thanh khoản khi giá nằm trong phạm vi đã chọn. Khi giá vượt ra ngoài phạm vi này, thanh khoản của họ sẽ không được sử dụng.
Tóm lại, các tick không phải do người dùng hay hệ thống chọn thủ công mà được tính toán dựa trên một quy luật logarit với khoảng cách được xác định bởi tick spacing của pool.


- Lượng assets họ đặt vào sẽ được chia đều cho các band
- Nhận fee: Giả sử họ đặt khoảng giá `[A; B]`
  - Nếu giá hiện tại lớn hơn B (`P_cur > B`) hoặc nhỏ hơn A (`P_cur < A`) thì tức là toàn bộ số thanh khoản của bạn đã được chuyển về hết 1 loại token.
  - Ngược lai nếu `A < P_cur < B` thì thanh khoan của LPs vẫn còn cả 2 loại token và lúc này họ nhận được fee theo shares
  - Xét trong các band nhỏ trong khoảng giá đó, nếu giá hiện tại nằm ngoài khoảng band nào thì band đó chỉ còn 1 loại token.
 
## Công thức
 
