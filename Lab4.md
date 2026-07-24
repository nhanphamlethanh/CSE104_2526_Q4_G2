### **EISALARY2**
Tính lương theo giờ cho nhân viên thời vụ.

Input:
- n: số nhân viên
- n dòng --> mỗi dòng gồm 6 số:
    - 5 số đầu tiên: số giờ làm việc trong 5 ngày
    - số cuối: hourly wage (lương theo giờ của nhân viên đó)
Output:
- n dòng: tương ứng với lương của n nhân viên
- lương trung bình trong office hour
- lương trung bình trong overtime hour

Ý tưởng:
1. Tính lương mỗi nhân viên
    - Biết: working hour per day
    - Nếu working_hour > 8:
        wage_in_day = 8*hourly_wage + (working_hour - 8) * (hourly_wage*1.5)
    - Ngược lại:
        wage_in_day = working_hour*hourly_wage
    => wage = wage_in_day1 + wage_in_day2 + wage_in_day3 ... + wage_in_day5
2. Tính average_office_wage
    average_office_wage = total_office_wage / total_office_hour
    total_office_wage = 
    total_office_hour = 

3. Tính average_overtime_wage


VD: n = 3
- Emp 1: hourly_wage = 5
    - Day 1: working_hour = 1       
        => office_hour = 1
           overtime_hour = 0
        => office_wage = office_hour*hourly_wage
           overtime_wage = overtime_hour*hourly_wage*1.5
        => wage = office_wage + overtime_wage
        => 
            + total_wage += wage = 5
            + total_office_hour += office_hour
            + total_office_wage += office_wage
            + total_overtime_hour += overtime_hour
            + total_overtime_wage += overtime_wage

    - Day 2: working_hour = 2
        => office_hour = 2
           overtime_hour = 0
        => wage = 2*5 + 0*(5*1.5) = 10  
        => total_wage += wage = 15
    - Day 3: working_hour = 3
        => office_hour = 3
           overtime_hour = 0
        => wage = 3*5 + 0*(5*1.5) = 15  
        => total_wage += wage = 30
    - Day 4: working_hour = 10
        => office_hour = 8
           overtime_hour = 2
        => wage = 8*5 + 2*(5*1.5) = 55 
        => total_wage += wage = 85
    - Day 5: working_hour = 2
        => office_hour = 2
           overtime_hour = 0
        => wage = 2*5 + 0*(5*1.5) = 10
        => total_wage += wage = 95

Tổng quát:

total_office_hour: tổng số giờ làm việc chính của toàn bộ nhân viên
total_office_wage: tổng số lương trong giờ hành chính của toàn bộ nhân viên
total_overtime_hour: tổng số giờ làm thêm của tonaf bộ nhân viên
total_overtime_wage: tổng số lương ngoài giờ của toàn bộ nhân viên

for each employee:
    input:
        int[] working hour
        double hourly_wage
    total_wage: tổng lương của nhân viên đang xét

    for each day:
        // Tính giờ làm việc trong ngày
        office_hour = Math.min(working_hour, 8)
        overtime_hour = Math.max(0, working_hour-8)

        // Tính lương trong ngày
        office_wage = office_hour*hourly_wage
        overtime_wage = overtime_hour*hourly_wage*1.5
        wage = office_wage + overtime_wage
        total_wage += wage
        
        // Cập nhật biến tổng
        total_office_hour += office_hour
        total_office_wage += office_wage
        total_overtime_hour += overtime_hour
        total_overtime_wage += overtime_wage

    sysout(total_wage)

double average_office_wage = (total_office_hour > 0) ? (total_office_wage / total_office_hour) : 0;
double average_overtime_wage = (total_overtime_hour > 0) ? (total_overtime_wage / total_overtime_hour) : 0;
    


### **EIGROSS**
Tính số thuế phải trả (tax).
Biết:
    - Lương sau thuế (net salary)
    - tax rate: 10%

VD: gross = 10_000_000
Suy công thức:
    tax = gross * tax_rate = 1_000_000
    net = gross - tax = 9_000_000 => đây là phần lương thực nhận
=> gross = net + tax
    biết: net
    cần tính: tax
    => tax = gross * tax_rate
       tax = (net + tax) * 10%
    => tax = 0.1 * net + 0.1 * tax
    => 0.9 * tax = 0.1 * net
    => tax = net / 9

Cách 2:
gross = net + tax
tax = gross * 10%
=> gross = net + gross*10%
=> net = gross * 90%
=> net chiếm 9 phần, tax chiếm 1
=> tax bằng 1/9 net



### **EIGROSS2**
Biết:
    - net
    - tax rate tại các level
    - personal relief = 11_000_000
Yêu cầu: tính gross

net = gross - tax

Nếu gross = 15_000_000
=> phần lương sẽ bị áp thuế là?
    taxable = gross - personal_relief = 4_000_000
- xét level 1:
    tax = 4_000_000 * 5% = 200_000
- xét level 2:

=> tax = 200_000 => net = gross - tax = 14_800_000

Biết net => tính gross
=> phần lương đã bị tính thuế:
    taxed = net - 11_000_000 = 14_800_000 - 11_000_000 = 3_800_000
=> cần tính số thuế đã đóng (tax) từ taxed

Tại level 1:
    min = 0
    maximum_tax = 5_000_000 * 5% = 250_000
    => net thuộc ngưỡng 1:
        net = gross - tax = 5_000_000 - 250_000 = 4_750_000
    => giới hạn trên của ngưỡng 1:
        max = min + 4_750_000 = 4_750_000
Level 2:
    min = 4_750_000
    maximum_tax = 5_000_000 * 10% = 500_000
    net = 5_000_000 - 500_000 = 4_500_000
    max = 4_750_000 + 4_500_000 = 9_250_000

0 --> 4_750_000 --> 9_250_000

level 1:
    tax = 3_800_000 / (100 - 5) * 5 = 200_000
    


### **EIUMARKUP**
VD: products = 200
- 100 món đầu tiên:
    cost = 200
    => pay = 100*cost = 20_000
- 100 món còn lại:
    cost = 199
    => pay = 100*199 = 19_900
=> total_pay = 20_000 + 19_900 = 39_900

VD: N = 250

Ý tưởng:
- Input:
    N: số sản phẩm
- Output: 
    pay: số tiền phải trả

Biết giá khởi điểm:
    cost = 200

Nếu số sản phẩm còn lại (N) > 100:
    // 1. Tính số tiền cần trả cho 100 món đó và cộng vào pay
    pay += 100*cost;
    // 2. Cập nhật số sản phẩm còn lại
    N -= 100; // trừ đi 100 sản phẩm vừa được tính
    // 3. Cập nhật giá cho 100 sp tiếp theo
    if (cost > 180)
        cost--;

// tính phần sp còn lại (N <= 100)
pay += N * cost;
    






Giải:
long N = sc.nextLong();
long tempN = N;
long cost = 200;
long pay = 0;

while (tempN > 100)
    pay += 100*cost;
    tempN -= 100;
    if (cost > 180)
        cost--;
pay += N * cost;



while (cost > 180 && tempN > 100)
    pay += cost*100;
    tempN -= 100;
    cost--;
pay += tempN * cost;

VD: N = 2500
tempN = 2500
cost = 200



### **EIVCHR1**

- nhận vào N
- tính số tiền được giảm:
    long discount = Math.min(N / 100 * 30 , 50_000);
- số tiền phải trả
    long pay = N - discount;

### **EIVCHR2**
Yêu cầu: tính số tiền phải trả (ít nhất có thể)
=> cần được giảm giá nhiều nhất có thể
=> tìm sản phẩm có giá cao nhất và áp voucher vào sản phẩm đó.

? Tìm sản phẩm có giá cao nhất?

long max_price = 0;
int N = sc.nextInt();
long pay = 0;

for (int i=0; i<N; i++)
    long price = sc.nextLong();
    if (price > max_price)
        max_price = price;
    pay += price;

pay -= max_price;
sysout(pay);


### **EIVCHR3**
Arrays.sort()


int N = sc.nextInt();
int M = sc.nextInt();
long pay = 0;
long[] prices = new long[N];

for (int i=0; i<N; i++)
    long prices[i] = sc.nextLong();
    pay += prices[i];

Arrays.sort(prices);

Cách 1:
for (int i=0; i < Math.min(N,M); i++)
    pay -= Math.min(50_000, prices[N-1-i]/100*30);

Cách 2:
for (int i=N-1; i >= (N - Math.min(N, M)); i--)
    pay -= Math.min(50_000, prices[i]/100*30);
(hoặc i >= Math.max(N-M, 0))

sysout(pay);

N = 10
M = 7

0 1 2 3 4 5 6 7 8 9
3 = 10 - 7 (N - M)

M = 12
0 = 10 - 12

