### **DISCOU**
Cửa hàng ABC áp dụng chiết khấu cho khách hàng. Chiết khấu được áp dụng theo từng bậc khác nhau dựa vào hóa đơn mua hàng. Cụ thể:

- Từ 1_000 đến 2_000_000:           không giảm giá          level 0
- Từ 2_000_000 đến 10_000_000:      giảm 3%                 level 1
- Từ 10_000_000 đến 50_000_000:     giảm 5%                 level 2
- Từ 50_000_000 đến 100_000_000:    giảm 7%                 level 3
- Từ 100_000_000 đến 200_000_000:   giảm 10%                level 4
- Từ 200_000_000 đến 500_000_000:   giảm 12%                level 5
- Từ 500_000_000 trở lên:           giảm 15%                level 6

VD: bill = 20_000_000
- Xét level 1:
    - Số tiền được xét chiết khấu là:
        amount = 10 - 2 = 8tr
    - Số tiền giảm ở ngưỡng này:
        discount = amount / 100 * 3 = 240_000
- Xét level 2:
    - Số tiền được xét chiết khấu là:
        amount = 
    - Số tiền giảm ở ngưỡng này:
        discount = 

=> Tại một level bất kỳ:
    - Số tiền được xét chiết khấu là:
        + TH1: amount đúng bằng số tiền tối đa được chiết khấu tại ngưỡng đó
            - Xảy ra khi: bill >= giá trị max của ngưỡng đó:
            VD: bill = 20_000_000
                tại level 1: bill > max (10_000_000)
        + TH2: amount nhỏ hơn
            - Xảy ra khi: bill < giá trị max của ngưỡng đó
            VD: bill = 6_000_000
                tại level 1: bill < max (10_000_000)
    => công thức tính số tiền được xét chiết khấu là:
        - Xét level 1:
            If (bill >= 10_000_000)
                amount = 10_000_000 - 2_000_000;
            else
                amount = bill - 2_000_000;
        => rút gọn:
            amount = Math.min(bill, 10_000_000) - 2_000_000;
        - Xét level 2:
            amount = Math.min(bill, 50_000_000) - 10_000_000;
        ...
        - Xét level 6:
            amount = bill - 500_000_000;

Hướng dẫn:
Cách 1: if-else

long bill = sc.nextLong();
long total_discount = 0;

if (bill <= 2_000_000)
    sysout(bill);
    return;

if (bill > 2_000_000)
    long amount = Math.min(bill, 10_000_000) - 2_000_000;
    long discount = amount / 100 * 3;
    total_discount += discount;
if (bill > 10_000_000)
    long amount = Math.min(bill, 50_000_000) - 10_000_000;
    long discount = amount / 100 * 5;
    total_discount += discount;
if (bill > 50_000_000)
    long amount = Math.min(bill, 100_000_000) - 50_000_000;
    long discount = amount / 100 * 7;
    total_discount += discount;
if (bill > 100_000_000)
    long amount = Math.min(bill, 200_000_000) - 100_000_000;
    long discount = amount / 100 * 10;
    total_discount += discount;
if (bill > 200_000_000)
    long amount = Math.min(bill, 500_000_000) - 200_000_000;
    long discount = amount / 100 * 12;
    total_discount += discount;
if (bill > 500_000_000)
    long amount = bill - 500_000_000;
    long discount = amount / 100 * 15;
    total_discount += discount;

long pay = bill - total_discount;
sysout(pay);

Cách 2: dùng mảng 
- Thiết kế 2 mảng:
    - Mảng 1: lưu giá trị giới hạn tại các ngưỡng
    - Mảng 2: lưu % chiết khấu tại các ngưỡng
=> limit dài hơn rate

long[] limit = {0, 2_000_000, 10_000_000, 50_000_000, 100_000_000, 200_000_000, 500_000_000, Long.MAX_VALUE};
long[] rate = {0, 3, 5, 7, 10, 12, 15};

for (int i=1; i<limit.length; i++)
    if (bill > limit[i-1])
        long amount = Math.min(bill, limit[i]) - limit[i-1];
        long discount = amount / 100 * rate[i-1];
        total_discount += discount;

long pay = bill - total_discount;
sysout(pay);

VD: bill = 600_000_000
Xét vòng lặp for:
i=1:
    amount = 2_000_000 - 0;
    discount = 0;
    total_discount = 0;
    => i=1: xét level 0
i=2:
    amount = 10_000_000 - 2_000_000;
    discount = 8_000_000 / 100 *3;
    total_discount = 240_000;
    => xét level 1:

Cách 3: dùng 2 mảng có độ dài bằng nhau

long[] limit = {2_000_000, 10_000_000, 50_000_000, 100_000_000, 200_000_000, 500_000_000, Long.MAX_VALUE};
long[] rate = {0, 3, 5, 7, 10, 12, 15};
long previousLimit = 0;

for (int i=0; i<limit.length; i++)
    if (bill > previousLimit)
        long amount = Math.min(bill, limit[i]) - previousLimit;
        long discount = amount / 100 * rate[i];
        total_discount += discount;
        previousLimit = limit[i];
    else 
        break;

i=0:
    limit[i] = 2_000_000
    limit[i-1] => không tồn tại
    => thay thế bằng biến previousLimit

=> bài toán lũy tiến

### **EIUCHRMS**
- Input:
    n: số hóa đơn
    n integers: giá trị của n hóa đơn
- Output:
    tổng thu nhập của cửa hàng
    => total_income = tổng giá trị các hóa đơn sau chiết khấu

Các ngưỡng:
- Level 1: <= 2_000_000
    discount_rate = 3%
- Level 2: <= 5_000_000
    discount_rate = 4%
- Level 3: <= 10_000_000
    discount_rate = 5%
- Level 4: <= 20_000_000
    discount_rate = 6%
- Level 5: <= 50_000_000
    discount_rate = 7%
- Level 6: <= 100_000_000
    discount_rate = 8%
- Level 7: <= 200_000_000
    discount_rate = 9%
- Level 8: > 200_000_000
    discount_rate = 10%

VD:
n = 5
bill_1 = 10_000
bill_2 = 1_000_000
bill_3 = 3_000_000
bill_4 = 5_000_000
bill_5 = 100_000_000

Xét lần lượt từng hóa đơn:
- Xét bill_1 = 10_000:
    - Số % chiết khấu:
        discount_rate = 3%
    - Số tiền được chiết khấu:
        discount_amount = 10_000 / 100 * 3 = 300
    - Số tiền khách hàng cần phải trả:
        actual_pay = 10_000 - 300 = 9_700
- Xét bill_2 = 1_000_000:
    - Số % chiết khấu:
        discount_rate = 3%
    - Số tiền được chiết khấu:
        discount_amount = 1_000_000 / 100 * 3 = 30_000
    - Số tiền khách hàng cần phải trả:
        actual_pay = 1_000_000 - 30_000 = 970_000
- Xét bill_3 = 3_000_000:
    - Số % chiết khấu:
        discount_rate = 4%
    - Số tiền được chiết khấu:
        discount_amount = 3_000_000 / 100 * 4 = 120_000
    - Số tiền khách hàng cần phải trả:
        actual_pay = 2_880_000
- Xét bill_4 = 5_000_000:
    - Số % chiết khấu:
        discount_rate = 4%
    - Số tiền được chiết khấu:
        discount_amount = 5_000_000 / 100 * 4 = 200_000
    - Số tiền khách hàng cần phải trả:
        actual_pay = 4_800_000
- Xét bill_5 = 100_000_000:
    - Số % chiết khấu:
        discount_rate = 8%
    - Số tiền được chiết khấu:
        discount_amount = 100_000_000 / 100 * 8 = 8_000_000
    - Số tiền khách hàng cần phải trả:
        actual_pay = 92_000_000

=> total_income = 9_700 + 970_000 + 2_880_000 + 4_800_000 + 92_000_000

=> Không phải bài toán lũy tiến

Hướng dẫn: if-else

long total_income = 0;
for (int i=0; i<n; i++)
    long bill = sc.nextLong();
    if (bill <= 2_000_000)
        long actual_pay = bill - bill/100*3;
        total_income += actual_pay;
    else if (bill <= 5_000_000)
        long actual_pay = bill - bill/100*4;
        total_income += actual_pay;
    else if (bill <= 10_000_000)
        long actual_pay = bill - bill/100*5;
        total_income += actual_pay;
    tương tự các level còn lại.



### **EIMEMCARD**
VD: n = 5
item_1 =    500_000
item_2 =  2_000_000
item_3 =  6_000_000
item_4 = 50_000_000
item_5 =  3_000_000

Xét lần lượt từng lần mua hàng.
- Xét lần 1:
    item_1 = 500_000
    => discount = 0 (chưa được xét hạng member)
    => sau khi thanh toán, khách hàng có được xét hạng? => không 
- Xét lần 2:
    item_2 =  2_000_000
    => discount = 0
    => sau khi thanh toán => xét hạng starter
- Xét lần 3:
    item_3 =  6_000_000
    => discount = 6_000_000 / 100 * 2 = 120_000
    => sau khi thanh toán, khách hàng có được nâng hạng? => không
- Xét lần 4:
    item_4 = 50_000_000
    => discount = 50_000_000 *2% = 1_000_000
    => sau khi thanh toán, xét nâng hạng: Diamond
- Xét lần 5:
    item_5 =  3_000_000
    => discount = 3_000_000 * 5% = 150_000
    => sau khi thanh toán, không xét nâng hạng.

Hướng dẫn:
int n = sc.nextInt();
int rate = 0;
long total_pay = 0;
for (int i=0; i<n; i++)
    long price = sc.nextLong();
    long discount = price / 100 * rate;
    System.out.print(discount + " ");

    total_pay += price;

    if (total_pay >= 200_000_000)
        rate = 7;
    else if (total_pay >= 50_000_000)
        rate = 5;
    else if (total_pay >= 20_000_000)
        rate = 3;
    else if (total_pay >= 1_000_000)
        rate = 2;
    
   


    
