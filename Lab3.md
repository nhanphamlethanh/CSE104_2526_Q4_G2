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
    => dùng biến previousLimit