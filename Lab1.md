### **EIMONE** 
Đổi tiền
Có b đồng
Đổi thành các mệnh giá: 20, 10, 5, 1
Muốn đổi được số tờ tiền ít nhất có thể.

Ý tưởng: Xét và đổi thành mệnh giá từ lớn đến bé. 
(greedy algorithm - thuật toán tham lam)

Hướng dẫn: 

Cách 1: sử dụng if-else
- gọi số tiền còn lại là:
	int left = b;
- If left >= 20:
	- Tính số tờ 20 đồng có thể đổi được
	  int num_20 = left / 20; (72/20=3)
	- Cập nhật số tiền còn lại:
	     left = left - num_20*20;
	hoặc left -= num_20*20;
	hoặc left = left % 20; (72 % 20 = 12)
	- In ra màn hình: mệnh giá + số tờ đổi được:
	  if (num_20 > 0)
		sysout(20 + " " + num_20);
- If left >= 10:


Cách 2: dùng array
- Khai báo 1 array chứa các mệnh giá tiền theo thứ tự:
int[] d = {20, 10, 5, 1};
int left = b;
- Duyệt vòng lặp for, chạy 4 lần tương ứng với 4 mệnh giá tiền:
for (int i=0; i<d.length; i++)
    int num = left / d[i];
    if (num > 0)
        sysout(d[i] + " " + num);
    left = left % d[i];


VD:
b = 72
- Xét mệnh giá 20: 
	- đổi được 3 tờ 20
	- còn lại 72 - 20*3 = 12
- Xét mệnh giá 10:
	- đổi được 1 tờ 10
	- còn lại: 2
- Xét mệnh giá 5:
	- không đổi tờ nào



### **EIPOINT**
Quy đổi điểm môn học:
- Input: điểm dạng số
- Output: điểm dạng chữ

Ý tưởng:
- Nhập vào điểm số:
    int score = sc.nextInt();
- Tạo 2 mảng:
    - Mảng chưá điểm dạng số:
        int[] num = {90, 85, ...};
    - Mảng chứa điểm dạng chữ:
        String[] cha = {"A", "A-", ...};
- Duyệt vòng lặp for, kiểm tra score thuộc ngưỡng nào => in ra điểm dạng chữ ở ngưỡng đó:
    for (int i=0; i<num.length; i++)
        if (score >= num[i]) 
            sysout(cha[i]);
            break;



### **EIUTHU**
Cho 2 chuỗi ký tự S1, S2
Phần đầu của S2 sẽ trùng lặp với phần cuối của S1.
Yêu cầu: tìm độ dài ngắn nhất có thể của bức thư.

Công thức:
    shortest_length = S1.length() + S2.length() - overlap

VD:
S1 = trunghoccosotran
S2 = trandainghia
=> overlap = 4 ("tran")

S1.length() = 16
S2.length() = 12

=> Số ký tự tối đa có thể bị trùng lặp:
    maxOverlap = Math.min(S1.length(), S2.length());

Gợi ý:
- Dùng phương thức .substring() để tách 1 phần ký tự từ 1 chuỗi ký tự
- Dùng phương thức .equals() để so sánh 2 chuỗi ký tự có bằng nhau không

int overlap = 0;
Duyệt vòng lặp for, chạy "maxOverlap" lần:
for (int i=maxOverlap; i>=1; i--)
    // 1. Lấy phần đuôi của S1
    String suffixS1 = S1.substring(S1.length() - i);
    // 2. Lấy phần đầu của S2
    String prefixS2 = S2.substring(0, i);
    // So sánh 2 phần
    if (suffixS1.equals(prefixS2))
        overlap = i;
        break;
int shortest_length = S1.length() + S2.length() - overlap;
sysout(shortest_length);



### **EIEVERYN**
- Input:
    + Số nguyên m
    + Số nguyên n
    + Array A có m phần tử
- Yêu cầu: Kiểm tra xem trong array A có chứa đủ các số từ 1 tới n?

VD:
m = 4
n = 3
A = {1, 3, 2, 1}
=> output: Yes

Ý tưởng:
- Khởi tạo mảng B boolean có độ dài n+1.
=> B phải dài n+1 là để index của B kéo dài từ 0 tới n => có đủ các số từ 1 tới n mà đề bài yêu cầu phải kiểm tra.
    boolean[] B = new boolean[n+1];
- Duyệt vòng lặp, xét từng phần tử trong mảng A: kiểm tra mỗi A[i] có nằm trong khoảng từ 1 tới n hay không?
    for (int i=0; i<m; i++)
        if (A[i] >= 1 && A[i] <= n)
            B[A[i]] = true;

Xét ví dụ:
A = {1, 3, 2, 1}
boolean[] B = new boolean[3+1];
B = {}
trong vòng lặp:
i=0: A[i]=1 => B[1] = true
i=1: A[i]=3 => B[3] = true
i=2: A[i]=2 => B[2] = true
i=3: A[i]=1 => B[1] = true
sau vòng lặp, mảng B được cập nhật:
B = {,true,true,true}
index: 0 1    2    3
value: _ true true true

duyệt 1 vòng lặp khác, xét mảng B:
- Kiểm tra các phần tử từ index 1 tới n
- Nếu không có phần tử nào bằng false, có nghĩa là mảng A chứa đủ các số từ 1 tới n
=> in Yes
- Ngược lại: in No
boolean hasAll = true; //có đủ tất cả các số từ 1 tới n không?
for (int i=1; i<B.length; i++)
    if (B[i] != true)
        hasAll = false;
        break;
if (hasAll)
    sysout("Yes")
else
    sysout("No");


### **EIUTRIGLE**
- Cho mảng A có N số nguyên dương.
- Đếm số tam giác có thể hợp thành được từ 3 phần tử bất kỳ của mảng.

VD:
N = 5
A = {1 4 3 6 2}
output = 2 => có 2 tam giác được hợp thành.

Giá trị của mỗi phần tử là độ dài của 1 cạnh.
Giả sử: biết độ dài 3 cạnh là a b c. 3 cạnh này sẽ tạo thành 1 tam giác nếu:
    a + b > c
và  a + c > b
và  b + c > a

Nếu biết được: a < b < c => c là cạnh lớn nhất
=> chỉ cần xét 1 điều kiện: a + b > c
=> từ mảng A ban đầu => sắp xếp lại theo thứ tự từ bé đến lớn:
    Arrays.sort(A)
A = {1 4 3 6 2}
sortedA = {1, 2, 3, 4, 6}

Ý tưởng:
- sau khi sắp xếp mảng A
- cố định cạnh lớn nhất (cạnh c)
- lần lượt xét từng cặp cạnh a, b và kiểm tra điều kiện (a + b > c?)

=> trong sortedA, cạnh lớn nhất là phần tử nào? => A[n-1]

VD:
Xét trường hợp c đầu tiên: c = sortedA[n-1] = 6
=> cặp a b đầu tiên: a = 1 (phần tử sortedA[0]), b = 4 (phần tử sortedA[n-2])
    a + b < c => bỏ qua
    => cặp a b tiếp theo: a = 2 (phần tử sortedA[1]), b = 4 (giữ nguyên)
        a + b = c => bỏ qua
        => cặp a b tiếp theo: a = 3 (phần tử sortedA[2]), b = 4 (giữ nguyên)
            a + b > c => + tam giác

int count = 0 => đếm số tam giác
VD 2:
sortedA = {1, 2, 3, 4, 5, 6, 8, 9}
index: 0 1 2 3 4 5 6 7
value: 1 2 3 4 5 6 8 9
- Xét c = 9:
    - Xét a = 1; b = 8:
        a + b = c => bỏ qua
    => tăng a, giữ b:
    - Xét a = 2; b = 8:
        a + b > c => thỏa mãn
        count += (index_b - index_a) => index_b = 6; index_a = 1 => 5 tam giác được hình thành
    => giữ a, giảm b:
    - Xét a = 2; b = 6:
        a +b < c => bỏ qua
    => tăng a, giữ b:
    - Xét a = 3; b = 6:
        a +b = c => không thỏa mãn
    => tăng a, giữ b:
    - Xét a = 4; b = 6:
        a + b > c => thỏa mãn
        count += (index_b - index_a) => index_b = 5; index_a = 3 => + 2 tam giác
    => giữ a, giảm b:
    - Xét a = 4; b = 5:
        a + b = c => không thỏa mãn:
    => tăng a, giữ b:
    => index_a = index_b => dừng lại
- Xét c = 8:
...

int count = 0;

for (int index_c=n-1; index_c>=2; index_c--)
    int index_a = 0;
    int index_b = index_c - 1;

    while (index_a < index_b)
        if (sortedA[index_a] + sortedA[index_b] > sortedA[index_c])
            count += (index_b - index_a);
            index_b--;
        else
            index_a++;


### **EISNAIL**

Một ngày bò được (A-B) mét.

Giả sử: buổi sáng ngày cuối, ốc sên bò đúng chính xác A mét.
=> các ngày trước đó, ốc sên bò bao nhiêu mét? => (V - A) mét

=> số fullDay (một ngày đủ sáng + đêm) ốc sên trải qua là?
    int fullDay = Math.ceil((V-A) / (A-B))

=> tổng số ngày là?
    int result = fullDay + 1; // 1 là buổi sáng ngày cuối cùng.


### **EIUFING**
- Nhận vào 1 số nguyên dương N
- Hỏi N thuộc vị trí nào trên bàn tay?

Công thức: result = N % 18
String[] finger = {}
String[] hand = {}
int result = N % 18;
sysout("Ngon " + finger[result-1] + " cua ban tay " + hand[result-1])