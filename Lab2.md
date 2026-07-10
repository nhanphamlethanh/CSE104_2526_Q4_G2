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