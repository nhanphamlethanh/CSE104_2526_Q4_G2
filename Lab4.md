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
    