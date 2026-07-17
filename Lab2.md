### **EIUMADIS**
- Cho mảng có n số nguyên
- Tìm giá trị lớn nhất của a_j - a_i. 
- Với 0 <= i <= j < n.
=> 
- i nằm trong khoảng từ 0 tới n-1.
- j nằm trong khoảng từ i tới n-1 => vì j >= i

VD:
n = 5
A = {2 4 1 5 3}
index: 0 1 2 3 4 
value: 2 4 1 5 3

Trường hợp j = i: A-j - A_i = 0

Gọi biến lưu giá trị cần tìm: giá trị lớn nhất của A_j - A_i là maxDiff.
    long maxDiff = 0;

Trường hợp j > i:
- Xét i = 0:
    - Xét j = 1:
        - Có A[j] - A[i] = 4 - 2 = 2

=> với mỗi j bất kỳ:
- VD: j = 3 => A[j] = 5
- Cần tìm A[j] - A[i] lớn nhất có thể => cần một A[i] nhỏ nhất có thể.

=> Gọi biến lưu giá trị A[i] nhỏ nhất có thể là min:
    long min = A[0];

=> Duyệt vòng lặp, xét lần lượt từng trường hợp j:
    for (int j = 1; j<n ; j++)
        //1. Tính khoảng cách a_j và a_i:
        long diff = A[j] - min;
        //2. So sánh diff và maxDiff, cập nhật maxDiff khi diff > maxDiff:
        if (diff > maxDiff)
            maxDiff = diff;
        //3. So sánh A[j] và min, cập nhật min nếu A[j] < min:
        if (A[j] < min):
            min = A[j];
    Kết thúc vòng lặp.

VD:
A = {2 4 1 5 3}
index: 0 1 2 3 4 
value: 2 4 1 5 3

maxDiff = 0;
min = A[0] = 2

vòng lặp for:
- Xét j = 1: A[j] = 4
    diff = A[j] - min = 4 - 2 = 2
    diff > maxDiff (=0) => maxDiff = diff = 2
    A[j] = 4 > min => bỏ qua
- Xét j = 2: A[j] = 1
    diff = 1 - 2 = -1
    diff < maxDiff => bỏ qua
    A[j] = 1 < min = 2 => min = A[j] = 1
- Xét j = 3: A[j] = 5
    diff = 5 - 1 = 4
    diff = 4 > maxDiff 2 => maxDiff = diff = 4
    A[j] = 5 > min => bỏ qua
- Xét j = 4: A[j] = 3
    diff = 3 - 1 = 2
    diff < maxDiff => bỏ qua
    A[j] > min => bỏ qua
Kết thúc.
=> có được maxDiff = 4




### **EIUBIRTH**
Mua quà. Có 2 loại quà:
- Màu xanh: X đồng
- Màu đỏ: Y đồng
- Phí đổi: Z đồng
Cần mua:
- B món màu xanh
- R món màu đỏ
Yêu cầu: tính số tiền ít nhất có thể.

VD:
- 5 món màu xanh
- 7 món màu đỏ
- X = 2
- Y = 6
- Z = 3

Ý tưởng:
- Để mua được B món màu xanh:
    - TH1: mua trực tiếp B món màu xanh
        costB = B * X = 5 * 2 = 10
    - TH2: mua B món màu đỏ và đổi thành màu xanh
        costB = B * Y + B * Z = B * (Y + Z) = 5 * (6 + 3) = 45
    => chọn phương án 1.
- Để mua được R món đỏ:
    - TH1: mua trực tiếp
        costR = R * Y = 7 * 6 = 42
    - TH2: mua R món màu xanh và đổi lại thành đỏ
        costR = R * X + R * Z = R * (X + Z) = 7 * (2 + 3) = 35
    => chọn phương án 2.

=> Hướng dẫn:
- Với mỗi loại quà, so sánh 2 trường hợp:
    + Nếu mua trực tiếp: giá mỗi món là?
    + Nếu mua màu kia và đổi lại: giá mỗi món là?
- Cần tính tổng tiền ít nhất có thể để mua 2 loại quà.

- Input:
B 
R
X
Y
Z
- Tính toán:
    1. Tính giá tiền tối ưu nhất cho mỗi món màu xanh
        - TH1: mua trực tiếp
            costB = X
        - Th2: mua đỏ và đổi lại
            costB = Y + Z
        costB = Math.min(X, (Y+Z));
    2. Tính giá tiền tối ưu nhất cho mỗi món màu đỏ
        costR = Math.min(Y, (X+Z));
    3. Tính tổng tiền:
        totalCost = B * costB + R * costR;


### **EIUCUBES**
Xây kim tự tháp.
- Có n viên gạch
- Yêu cầu: tính xem xây được bao nhiêu tầng?
- Biết số viên gạch cần cho mỗi tầng như sau:
    - Layer 1: 1
    - Layer 2: 1 + 2
    - Layer 3: 1 + 2 + 3
    - Layer 4: 1 + 2 + 3 + 4
    - ...
    - Layer k: 1 + 2 + 3 + ... + (k-1) + k
=> công thức tính số gạch cần cho layer k:
    số viên gạch cho layer k = số viên gạch cho layer (k-1) + k

VD: k = 4
k-1 = 3
số viên gạch cho layer 3 = 1 + 2 + 3 = 6
số viên gạch cho layer 4 = 6 + 4 = 10

VD: n = 25
- Xét layer 1:
    - Số viên gạch cần: 1
    - Số viên gạch đang có: 25 > 1 => đủ => xây layer 1
    - Số viên gạch còn lại: 24
- Xét layer 2:
    - Số viên gạch cần: 1 + 2
    - Số viên gạch đang có: 24 > 3 => đủ => xây layer 2
    - Số viên gạch còn lại: 21
- Xét layer 3:
    - Số viên gạch cần: 6
    - Số viên gạch đang có: 21 > 6 => đủ => xây layer 3
    - Số viên gạch còn lại: 15
- Xét layer 4:
    - Số viên gạch cần: 10
    - Số viên gạch đang có: 15 > 10 => đủ => xây layer 4
    - Số viên gạch còn lại: 5
- Xét layer 5:
    - Số viên gạch cần: 10 + 5 = 15
    - Số viên gạch đang có: 5 < 15 => không đủ cho layer 5 
=> số layer xây được là: 4

Tổng quát hóa:
- Input:
    n: số viên gạch ban đầu
    left_bricks: số viên gạch còn lại
        int left_bricks = n;
    layer: tầng đang xét
        int layer = 1;
    needed_bricks: số gạch cần cho layer
        int needed_bricks = 1;
    built_layers: số tầng đã xây
        int built_layers = 0;
- Vòng lặp: 
    while (left_bricks >= needed_bricks)
        // Điều kiện thỏa mãn => cập nhật số tầng xây được
        built_layers++;

        //tính số viên gạch còn lại
        left_bricks -= needed_bricks;

        //cập nhật layer tiếp theo cần xét
        layer++; 

        //tính số viên gạch cần cho layer tiếp theo
        needed_bricks = needed_bricks + layer;

    Kết thúc vòng lặp.



### **EIUCUBES2**
- Có k loại gạch. Xây được tương ứng k kim tự tháp.
- Biết số lượng gạch ở mỗi loại.
- Tính chiều cao của mỗi tháp.

Giả sử:
- Xét loại gạch i
- Số lượng gạch của loại i là n_i
- Biết:
    1 <= n_i <= 10^18

ý tưởng: sử dụng binary search
- low = 0
- high = 2_000_000
- mid => tương ứng với chiều cao của mỗi kim tự tháp.

Tìm công thức tính số gạch cần cho 1 kim tự tháp có chiều cao là H.

    - Công thức tính số gạch cần cho layer h:
        bricks for layer h = 1 + 2 + 3 +... + (h-1) + h
    => rút gọn công thức:
        h*(h+1)/2

    layer 1: 1
    layer 2: 1 + 2
    layer 3: 1 + 2 + 3
    ...
    layer h: h*(h+1)/2
    => tổng số gạch cho toàn bộ kim tự tháp là?
        - Gọi i là biến đếm layer. với i chạy từ 1 tới h
$$totalBricks = \frac{1}{2} \sum_{i=1}^{h}(i*(i+1))$$ 

$$A1 = \sum_{i=1}^{h}(i^2)$$ 
$$A2 = \sum_{i=1}^{h}(i)$$ 

=>

A1 = h(h+1)(2h+1)/6

A2 = (1+h)*h/2

=>

totalBricks = 1/2 * (A1 + A2)

totalBricks = 1/2 * (h(h+1)(2h+1)/6 + (1+h)*h/2) 

totalBricks = h(h+1)(h+2) / 6

long height = 0;

while (low <= high)
    long mid = low + (high-low)/2;

    // mid tương đương với chiều cao của kim tự tháp (h)
    long h = mid;

    long neededBricksforH = h(h+1)/2;

    if (neededBricksforH / 3 <= n / (h+2))
        height = mid;
        low = mid + 1;
    else 
        high = mid - 1;

Rã công thức totalBricks để tránh tràn số.
    totalBricks = h(h+1)(h+2) / 6
                = (h(h+1)/2) * ((h+2)/3)
    => nhìn thấy: h(h+1)/2 => công thức tính số gạch cần cho layer thứ h.
    => totalBricks = neededBricksforH * ((h+2)/3)
    => phép so sánh totalBricks <= n trở thành:
        neededBricksforH * ((h+2)/3) <= n
        neededBricksforH / 3 <= n / (h+2)