# BÀI LÀM – ÔN TẬP NGÀY 2

- **Họ tên:**đặng bá chung 
- **Lớp:**cntt1 
- **Link repository:**
- **Hệ điều hành (Windows/macOS):**windown 

## Bài 1. Lọc log thủ công

### Lệnh đã chạy

```shell
PS C:\Users\ADMIN\Downloads\starter-kit\starter-kit\trung-tam-tieng-anh> Get-Content logs/access.log | Select-String "ERROR" > logs/error_report.txt
>> Get-Content logs/error_report.txt

2025-10-18 08:17:59 [ERROR] Khong tim thay trang /lich-thi (404)
2025-10-18 08:25:55 [ERROR] Het thoi gian cho (timeout)
2025-10-18 08:33:51 [ERROR] Ket noi may chu du lieu that bai
2025-10-18 08:37:19 [ERROR] Ket noi may chu du lieu that bai
2025-10-18 08:49:43 [ERROR] Het thoi gian cho (timeout)
2025-10-18 08:53:11 [ERROR] Het thoi gian cho (timeout
```

### 2 dòng lỗi đầu tiên trong error_report.txt

```text
2025-10-18 08:17:59 [ERROR] Khong tim thay trang /lich-thi (404).
2025-10-18 09:05:12 [ERROR] Khong the tai anh dai dien nguoi dung.

```

## Bài 2. Đếm bằng pipeline

### Lệnh

```shell
PS C:\Users\ADMIN\Downloads\starter-kit\starter-kit\trung-tam-tieng-anh> Get-Content logs/access.log | Select-String "WARNING" | Measure-Object


Count    : 4
Average  :
Sum      :
Maximum  :
Minimum  :
Property :



PS C:\Users\ADMIN\Downloads\starter-kit\starter-kit\trung-tam-tieng-anh> Get-Content logs/payment.log | Select-String "ERROR" | Measure-Object


Count    : 3
Average  :
Sum      :
Maximum  :
Minimum  :
Property :
### Kết quả đếm (Windows: giá trị Count; macOS: con số in ra)

```text
WARNING trong access.log:5
ERROR trong payment.log:3
```

## Bài 3. Chạy script auto_warning (.ps1 hoặc .sh)

### Lệnh chạy (Windows: nếu dùng Phụ lục 2 thì ghi cả 2 lệnh)

```shell
PS C:\Users\ADMIN\Downloads\starter-kit\starter-kit\trung-tam-tieng-anh> # Script: auto_warning.ps1
>> # Tac gia: Nguyen Van A
>> # Ngay tao: 21/10/2026
>>
>> Write-Host "Dang loc canh bao thanh toan..."
>> "=== CANH BAO THANH TOAN ===" > logs/warning_report.txt
>> Get-Content logs/payment.log | Select-String "WARNING" >> logs/warning_report.txt
>> Write-Host "Hoan thanh!"
Dang loc canh bao thanh toan...
Hoan thanh!

```

### Nội dung file logs/warning_report.txt

```text
S C:\Users\ADMIN\Downloads\starter-kit\starter-kit\trung-tam-tieng-anh> === CANH BAO THANH TOAN ===
>> 2025-10-18 10:12:00 [WARNING] Cong thanh toan pha huyen phan hoi cham.
>> 2025-10-18 11:45:22 [WARNING] Giao dich trung lap tu nguoi dung 102.
>> 2025-10-18 14:30:15 [WARNING] Tai khoan khong du so du de thanh toan.
At line:2 char:12
+ 2025-10-18 10:12:00 [WARNING] Cong thanh toan pha huyen phan hoi cham ...
+            ~~~~~~~~
Unexpected token '10:12:00' in expression or statement.
At line:3 char:12
+ 2025-10-18 11:45:22 [WARNING] Giao dich trung lap tu nguoi dung 102.
+            ~~~~~~~~
Unexpected token '11:45:22' in expression or statement.
At line:4 char:12
+ 2025-10-18 14:30:15 [WARNING] Tai khoan khong du so du de thanh toan.
+            ~~~~~~~~
Unexpected token '14:30:15' in expression or statement.
    + CategoryInfo          : ParserError: (:) [], ParentContainsErrorRecordException
    + FullyQualifiedErrorId : UnexpectedToken 
```

## Bài 4. Báo cáo tổng hợp

### Các lệnh đã chạy

```shell

PS C:\Users\ADMIN\Downloads\starter-kit\starter-kit\trung-tam-tieng-anh> "=== TONG HOP ACCESS LOG ===" > logs/tong_hop_ngay2.txt
>> Get-Content logs/access.log | Select-String "ERROR" >> logs/tong_hop_ngay2.txt
>> Get-Content logs/payment.log | Select-String "WARNING" | Measure-Object >> logs/tong_hop_ngay2.txt

```

### Nội dung file logs/tong_hop_ngay2.txt

```text
>> Get-Content logs/payment.log | Select-String "WARNING" | Measure-Object >> logs/tong_hop_ngay2.txt
PS C:\Users\ADMIN\Downloads\starter-kit\starter-kit\trung-tam-tieng-anh> === TONG HOP ACCESS LOG ===
>> 2025-10-18 08:17:59 [ERROR] Khong tim thay trang /lich-thi (404).
>> 2025-10-18 09:05:12 [ERROR] Khong the tai anh dai dien nguoi dung.
>> 2025-10-18 15:20:44 [ERROR] Loi ket noi co so du lieu tam thoi.
>> 3

```

## Bài 5. Câu hỏi ngắn

- **a)**   a) Lệnh > và >> khác nhau thế nào?
• Toán tử > dùng để ghi đè (hoặc tạo mới file nếu chưa có, xóa sạch nội dung cũ).
• Toán tử >> dùng để ghi nối tiếp (thêm nội dung mới vào cuối file hiện có mà không làm mất nội dung cũ).
  
- **b)** Bài 4, nếu lệnh thứ hai dùng > thay cho >>, nội dung file tong_hop_ngay2.txt sẽ thay đổi ra sao?
• Nội dung tiêu đề === TONG HOP ACCESS LOG === ở dòng thứ nhất sẽ bị xóa hoàn toàn và bị đè đè bởi các dòng lỗi ERROR

• - **c)** c) Vì sao trong script nên dùng đường dẫn tương đối logs/payment.log thay vì đường dẫn tuyệt đối?
o Dùng đường dẫn tương đối giúp script hoạt động linh hoạt trên mọi máy tính/thư mục khác nhau khi tải về hoặc đưa lên môi trường server. Đường dẫn tuyệt đối sẽ bị lỗi vì phụ thuộc cố định vào tên người dùng và thư mục của một máy tính duy nhất.


## Tự chấm (điền sau khi có đáp án)

- **Điểm tự chấm:** ..../100
- **Lỗi mình đã mắc và cách sửa:**

